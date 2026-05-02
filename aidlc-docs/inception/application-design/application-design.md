# Application Design

## Summary

T-AI-DA は、低リスクな日常判断を AI が一択で代行する AWS ベースの意思決定 OS である。MVP は朝の生活プラン生成と即決ボタンに絞り、Safety Guardrails によって高リスク判断を制限する。

## Design Goals

- 審査員が Intent、テーマ適合、AWS 構成、Unit 分解を短時間で追えること。
- Decision Orchestrator、User Context、Laziness Level、Safety Guardrails の責務が明確であること。
- Construction フェーズで MVP プロトタイプに移れる粒度であること。

## Architecture Summary

```mermaid
flowchart LR
    UI["User Interface / Notification"] --> API["Amazon API Gateway"]
    API --> ORCH["AWS Lambda<br/>Decision Orchestrator"]
    SCHED["EventBridge Scheduler"] --> ORCH
    ORCH --> BEDROCK["Amazon Bedrock"]
    ORCH --> DDB["Amazon DynamoDB<br/>Context / Laziness / History"]
    ORCH --> SAFETY["Safety Guardrails"]
    ORCH --> PREP["Preparation Assistant"]
    ORCH --> CW["Amazon CloudWatch"]
    PREP --> S3["Amazon S3 / Static Assets"]
```

## MVP コスト概算

MVP スケール（数ユーザー、朝のプラン生成 + 即決ボタン 30 回 / 日）での概算は月 **¥200–600 程度**。Amazon Bedrock（Haiku モデル）がコストドライバーで、Lambda・DynamoDB・API Gateway は無料枠内に収まる。ユーザー数が増えると Bedrock 利用量が線形に増加する。

## Interaction Flows

### 朝の生活プラン生成フロー

```mermaid
sequenceDiagram
    participant ES as EventBridge Scheduler
    participant OC as Lambda (Decision Orchestrator)
    participant UC as DynamoDB (User Context)
    participant SG as Safety Guardrails
    participant BR as Amazon Bedrock
    participant PA as Preparation Assistant
    participant ND as Notification and Delivery
    participant UI as User (API Gateway)

    ES->>OC: 朝の定刻トリガー
    OC->>UC: loadContext(userId, date)
    UC-->>OC: 天気、予定、好み、予算
    OC->>OC: calculateDelegationMode()
    OC->>SG: evaluateDecisionRisk(plan candidates)
    SG-->>OC: Allowed / 承認必須 / 対象外
    OC->>BR: 生活プラン生成（Allowed 項目のみ）
    BR-->>OC: 食事・服装・夜の過ごし方
    OC->>PA: generatePreparation(decision)
    PA-->>OC: 買い物リスト、店舗候補、ルート候補
    OC->>UC: saveDecisionHistory()
    OC->>ND: deliverDecision(userId, plan)
    UI->>ND: GET /today-plan
    ND-->>UI: 生活プラン + 準備支援
```

### 即決ボタンフロー

```mermaid
sequenceDiagram
    participant UI as User
    participant AG as API Gateway
    participant OC as Lambda (Decision Orchestrator)
    participant UC as DynamoDB (User Context)
    participant SG as Safety Guardrails
    participant BR as Amazon Bedrock

    UI->>AG: POST /decide {"query": "今夜の夕食は？"}
    AG->>OC: decideNow(userId, request)
    OC->>UC: loadContext(userId)
    UC-->>OC: 好み、予算、位置情報
    OC->>SG: evaluateDecisionRisk(request)
    alt 低リスク
        SG-->>OC: Allowed
        OC->>BR: 一択判断生成
        BR-->>OC: 判断 + 理由
        OC->>BR: 準備支援生成
        BR-->>OC: 店舗候補、注文リンク候補
        OC->>UC: saveDecisionHistory()
        OC-->>AG: 判断 + 準備支援
        AG-->>UI: 「鶏鍋にしてください。近所のスーパーで材料が揃います。」
    else 高リスク
        SG-->>OC: 承認必須 / 対象外
        OC-->>AG: 制限理由
        AG-->>UI: 「その判断は私の範疇外です。ご自身でお決めください。」
    end
```

## Detailed Artifacts

- [Components](components.md)
- [Component Methods](component-methods.md)
- [Services](services.md)
- [Component Dependency](component-dependency.md)

## Requirements Coverage

| Requirement | Design Coverage |
| --- | --- |
| FR-001 | Morning Plan Service, Decision Orchestrator |
| FR-002 | Instant Decision Service, Decision Orchestrator |
| FR-003 | Laziness Level, User Context |
| FR-004 | Preparation Assistant, Preparation Service |
| FR-005 | Safety Guardrails, Safety Evaluation Service |
| NFR-001 | Safety Dependency Rule |
| NFR-002 | T-AI-DA Persona, explanation messages |
| NFR-003 | Morning Plan Service and Instant Decision Service response flow |
| NFR-004 | User Context data boundaries |
| NFR-005 | Service separation and external API adapters |

## Next Design Step

次の Units Generation では、この Application Design を Construction で扱える Unit of Work に分解する。特に Safety Guardrails と Decision Core は独立して検証可能な単位として扱う。
