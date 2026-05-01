# T-AI-DA 書類審査提出物 Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** AWS Summit Japan 2026 AI-DLC ハッカソンの書類審査に提出できる、T-AI-DA の `README.md` と AI-DLC Inception フェーズ成果物一式を作成する。

**Architecture:** 審査員向けの入口は `README.md` に集約し、AI-DLC の詳細な成果物は `aidlc-docs/` 配下に配置する。書類審査基準である Intent、Unit 分解、テーマ適合、ドキュメント品質が読み取りやすいように、全ファイルで用語とストーリーを揃える。

**Tech Stack:** Markdown、AI-DLC Inception artifacts、AWS architecture narrative、PowerShell validation、Git.

---

## Scope Notes

- この計画はドキュメント生成のみを対象にする。アプリケーションコードや動作する MVP は作らない。
- 既存の未追跡ファイル `AGENTS.md` と `AWS_Summit_Japan_2026_Hackathon_参加規約.pdf` はこの計画では変更しない。
- 承認済み仕様は `docs/superpowers/specs/2026-04-30-t-ai-da-design.md` を正とする。
- 提出物は日本語で作成する。プロダクト名、Unit 名、AI-DLC 固有用語は必要に応じて英語を併記する。

## File Structure

### Create

- `README.md`
  - 審査員が最初に読む入口。コンセプト、Intent、MVP、AWS 構成、提出物リンクを短くまとめる。
- `aidlc-docs/aidlc-state.md`
  - AI-DLC のプロジェクト状態、Inception ステージ進捗、拡張設定、次ステップを記録する。
- `aidlc-docs/audit.md`
  - これまでの意思決定と承認を時系列で記録する。
- `aidlc-docs/inception/requirements/requirement-verification-questions.md`
  - これまでの質問と回答を AI-DLC の `[Answer]:` 形式で整理する。
- `aidlc-docs/inception/requirements/requirements.md`
  - Intent、機能要件、非機能要件、制約、スコープ外をまとめる。
- `aidlc-docs/inception/plans/user-stories-assessment.md`
  - User Stories を実行する判断理由を記録する。
- `aidlc-docs/inception/user-stories/personas.md`
  - 一人暮らしの決断疲れビジネスパーソンを中心にしたペルソナを定義する。
- `aidlc-docs/inception/user-stories/stories.md`
  - INVEST を意識したユーザーストーリーと受け入れ条件を定義する。
- `aidlc-docs/inception/plans/execution-plan.md`
  - Inception から Construction に進むための実行判断と Mermaid 可視化を記載する。
- `aidlc-docs/inception/plans/application-design-plan.md`
  - Application Design の実行計画と質問回答サマリを記録する。
- `aidlc-docs/inception/application-design/components.md`
  - 主要コンポーネントの責務とインターフェースを定義する。
- `aidlc-docs/inception/application-design/component-methods.md`
  - コンポーネントごとの主要メソッドを高レベルに定義する。
- `aidlc-docs/inception/application-design/services.md`
  - サービス層とオーケストレーションを定義する。
- `aidlc-docs/inception/application-design/component-dependency.md`
  - コンポーネント依存関係とデータフローを定義する。
- `aidlc-docs/inception/application-design/application-design.md`
  - Application Design の統合版。個別設計ファイルへの索引も兼ねる。
- `aidlc-docs/inception/plans/unit-of-work-plan.md`
  - Unit 分解の計画、判断基準、質問回答サマリを記録する。
- `aidlc-docs/inception/application-design/unit-of-work.md`
  - Unit of Work の定義、責務、将来の Construction 対象を記載する。
- `aidlc-docs/inception/application-design/unit-of-work-dependency.md`
  - Unit 間の依存関係を記載する。
- `aidlc-docs/inception/application-design/unit-of-work-story-map.md`
  - ユーザーストーリーと Unit の対応を記載する。

### Modify

- `docs/superpowers/specs/2026-04-30-t-ai-da-design.md`
  - 必要に応じて、実行時に発見した軽微な表記ゆれだけを修正する。内容方針は変更しない。

### Do Not Modify

- `AGENTS.md`
- `AWS_Summit_Japan_2026_Hackathon_参加規約.pdf`

---

### Task 1: README の審査員向け入口を作成する

**Files:**
- Create: `README.md`
- Reference: `docs/superpowers/specs/2026-04-30-t-ai-da-design.md`

- [ ] **Step 1: README の構成を固定する**

`README.md` に次の見出しをこの順番で入れる。

```markdown
# T-AI-DA（タイダ）

## 一言で
## なぜ作るのか
## 対象ユーザー
## MVP 体験
## 怠惰レベル
## AWS アーキテクチャ案
## AI-DLC Inception 成果物
## 審査基準への対応
## 今後の展開
```

- [ ] **Step 2: コンセプトと Intent を書く**

`## 一言で` には次の趣旨を含める。

```markdown
T-AI-DA は、日常の小さな意思決定に疲れた一人暮らしのビジネスパーソンを、AI が徹底的に甘やかす意思決定代行サービスです。
```

`## なぜ作るのか` には、決断疲れ、選択肢過多、退勤後の認知負荷を明記する。

- [ ] **Step 3: MVP 体験を書く**

`## MVP 体験` に、朝の生活プラン生成と即決ボタンを書く。

```markdown
1. 朝の生活プラン生成
2. 即決ボタン
```

各項目には、T-AI-DA が一択で決めること、準備支援まで行うことを含める。

- [ ] **Step 4: AWS アーキテクチャ案を書く**

`## AWS アーキテクチャ案` に以下を含める。

- Amazon Bedrock: 意思決定生成と人格応答
- AWS Lambda: 意思決定オーケストレーション
- Amazon API Gateway: API エントリポイント
- Amazon DynamoDB: ユーザー設定、怠惰レベル、意思決定履歴
- Amazon EventBridge Scheduler: 朝の生活プラン生成トリガー
- Amazon S3: ドキュメント、静的アセット、将来の UI 配信候補
- Amazon CloudWatch: ログ、監視、意思決定実行状況の観測

- [ ] **Step 5: AI-DLC 成果物リンクを書く**

`## AI-DLC Inception 成果物` に、この計画で作成する `aidlc-docs/` 配下の主要ファイルへの相対リンクを置く。

- [ ] **Step 6: README を確認する**

Run: `Get-Content -LiteralPath 'README.md' -TotalCount 80`

Expected: 見出しが順番通りに表示され、T-AI-DA の一文説明、MVP、AWS 構成、成果物リンクが確認できる。

- [ ] **Step 7: README 作成をコミットする**

```bash
git add README.md
git commit -m "docs: add T-AI-DA overview README"
```

---

### Task 2: AI-DLC 状態管理と監査ログを作成する

**Files:**
- Create: `aidlc-docs/aidlc-state.md`
- Create: `aidlc-docs/audit.md`

- [ ] **Step 1: `aidlc-state.md` を作成する**

以下の見出しを含める。

```markdown
# AI-DLC State Tracking

## Project Information
## Workspace State
## Code Location Rules
## Extension Configuration
## Stage Progress
## Current Status
## Next Recommended Step
```

`Project Type` は `Greenfield`、`Current Stage` は `INCEPTION - Units Generation Complete` とする。

- [ ] **Step 2: `audit.md` を作成する**

以下の意思決定を時系列で記録する。

- ハッカソン要件の確認
- コンセプトを「意思決定代行 IT サービス」に決定
- MVP を「朝の生活プラン + 即決ボタン」に決定
- 名称を `T-AI-DA` に決定
- 安全境界を低リスク領域中心に決定
- 提出パッケージ構成を承認

- [ ] **Step 3: 状態管理ファイルを確認する**

Run: `Get-Content -LiteralPath 'aidlc-docs/aidlc-state.md' -TotalCount 80`

Expected: Greenfield、Inception ステージ進捗、Unit Generation 完了相当の状態が確認できる。

- [ ] **Step 4: 監査ログを確認する**

Run: `Get-Content -LiteralPath 'aidlc-docs/audit.md' -TotalCount 120`

Expected: 主要な意思決定とユーザー承認が記録されている。

- [ ] **Step 5: 状態管理と監査ログをコミットする**

```bash
git add aidlc-docs/aidlc-state.md aidlc-docs/audit.md
git commit -m "docs: add AI-DLC state and audit trail"
```

---

### Task 3: Requirements Analysis 成果物を作成する

**Files:**
- Create: `aidlc-docs/inception/requirements/requirement-verification-questions.md`
- Create: `aidlc-docs/inception/requirements/requirements.md`

- [ ] **Step 1: 質問回答ファイルを作成する**

`requirement-verification-questions.md` に、これまでの質問を AI-DLC の `[Answer]:` 形式で整理する。

必ず含める質問:

- 意思決定代行の対象領域
- MVP の入口
- サービス人格
- 意思決定代行の強さ
- 利用する文脈データ
- 対象ユーザー
- 象徴的な体験
- 実行代行の範囲
- サービス名
- 自動決定しない領域

- [ ] **Step 2: Requirements を作成する**

`requirements.md` に以下を含める。

```markdown
# Requirements

## Intent Analysis
## Business Intent
## Functional Requirements
## Non-Functional Requirements
## Data and Context Requirements
## Safety and Guardrails
## Out of Scope
## Traceability
```

- [ ] **Step 3: 機能要件を書く**

Functional Requirements には最低限次を含める。

- FR-001: 朝の生活プランを生成する
- FR-002: 即決ボタンで小さな迷いに一択回答する
- FR-003: 怠惰レベルに応じて提案型、半自動型、低リスク自動決定型を切り替える
- FR-004: 買い物リスト、店舗候補、ルート、注文リンクなどの準備支援を生成する
- FR-005: 高リスク判断を検出して制限する

- [ ] **Step 4: 非機能要件を書く**

Non-Functional Requirements には最低限次を含める。

- NFR-001: 低リスク領域を明確に制限する安全性
- NFR-002: ユーザーが理由を理解できる説明可能性
- NFR-003: 朝の利用に耐える応答速度
- NFR-004: 個人文脈データのプライバシー保護
- NFR-005: 将来の外部連携に耐える拡張性

- [ ] **Step 5: Requirements を確認する**

Run: `Select-String -LiteralPath 'aidlc-docs/inception/requirements/requirements.md' -Pattern 'FR-001','NFR-001','Safety','Intent'`

Expected: Intent、FR、NFR、安全境界の記述が検出される。

- [ ] **Step 6: Requirements 成果物をコミットする**

```bash
git add aidlc-docs/inception/requirements/requirement-verification-questions.md aidlc-docs/inception/requirements/requirements.md
git commit -m "docs: add AI-DLC requirements for T-AI-DA"
```

---

### Task 4: User Stories 成果物を作成する

**Files:**
- Create: `aidlc-docs/inception/plans/user-stories-assessment.md`
- Create: `aidlc-docs/inception/user-stories/personas.md`
- Create: `aidlc-docs/inception/user-stories/stories.md`

- [ ] **Step 1: User Stories 実行判断を書く**

`user-stories-assessment.md` に、User Stories を実行する理由を書く。

判断理由:

- 新規ユーザー向けサービスである
- 複数のユーザー体験を含む
- 受け入れ条件が審査資料の品質に直結する
- Unit 分解にストーリー対応が必要である

- [ ] **Step 2: ペルソナを作成する**

`personas.md` に最低 3 名のペルソナを書く。

- Primary: 一人暮らしの決断疲れビジネスパーソン
- Secondary: 生活管理が苦手な若手社会人
- Future: 選択肢過多に疲れた消費者

- [ ] **Step 3: ユーザーストーリーを書く**

`stories.md` に最低 8 件のストーリーを書く。

必須ストーリー:

- 朝の生活プランを受け取る
- 食事を一択で決めてもらう
- 服装を決めてもらう
- 買い物候補と準備リストを受け取る
- 即決ボタンで迷いを投げる
- 怠惰レベルが上がる
- 高リスク判断で承認を求められる
- 低リスクな準備支援を受ける

- [ ] **Step 4: 各ストーリーに受け入れ条件を書く**

各ストーリーに `Acceptance Criteria` を 3 つ以上入れる。

- [ ] **Step 5: User Stories 成果物を確認する**

Run: `Select-String -LiteralPath 'aidlc-docs/inception/user-stories/stories.md' -Pattern 'Acceptance Criteria','怠惰レベル','即決ボタン'`

Expected: Acceptance Criteria、怠惰レベル、即決ボタンが検出される。

- [ ] **Step 6: User Stories 成果物をコミットする**

```bash
git add aidlc-docs/inception/plans/user-stories-assessment.md aidlc-docs/inception/user-stories/personas.md aidlc-docs/inception/user-stories/stories.md
git commit -m "docs: add personas and user stories"
```

---

### Task 5: Workflow Planning 成果物を作成する

**Files:**
- Create: `aidlc-docs/inception/plans/execution-plan.md`

- [ ] **Step 1: Execution Plan の構成を書く**

`execution-plan.md` に以下を含める。

```markdown
# Execution Plan

## Detailed Analysis Summary
## Change Impact Assessment
## Risk Assessment
## Phase Determination
## Workflow Visualization
## Recommended Construction Scope
```

- [ ] **Step 2: Phase Determination を書く**

Inception の判断は次の通りにする。

- Workspace Detection: EXECUTE
- Reverse Engineering: SKIP (Greenfield)
- Requirements Analysis: EXECUTE
- User Stories: EXECUTE
- Workflow Planning: EXECUTE
- Application Design: EXECUTE
- Units Generation: EXECUTE

- [ ] **Step 3: Mermaid 可視化を書く**

`Workflow Visualization` に `flowchart TD` の Mermaid 図を書く。Mermaid には Inception の実行、Construction の次フェーズ、Operations placeholder を含める。

- [ ] **Step 4: Execution Plan を確認する**

Run: `Select-String -LiteralPath 'aidlc-docs/inception/plans/execution-plan.md' -Pattern 'flowchart TD','Units Generation','Greenfield'`

Expected: Mermaid、Units Generation、Greenfield 判断が検出される。

- [ ] **Step 5: Workflow Planning 成果物をコミットする**

```bash
git add aidlc-docs/inception/plans/execution-plan.md
git commit -m "docs: add AI-DLC execution plan"
```

---

### Task 6: Application Design 成果物を作成する

**Files:**
- Create: `aidlc-docs/inception/plans/application-design-plan.md`
- Create: `aidlc-docs/inception/application-design/components.md`
- Create: `aidlc-docs/inception/application-design/component-methods.md`
- Create: `aidlc-docs/inception/application-design/services.md`
- Create: `aidlc-docs/inception/application-design/component-dependency.md`
- Create: `aidlc-docs/inception/application-design/application-design.md`

- [ ] **Step 1: Application Design Plan を作成する**

`application-design-plan.md` に、Application Design を実行する理由と対象成果物リストを書く。

- [ ] **Step 2: Components を作成する**

`components.md` に次のコンポーネントを書く。

- Decision Orchestrator
- User Context
- T-AI-DA Persona
- Laziness Level
- Safety Guardrails
- Preparation Assistant
- Notification and Delivery

- [ ] **Step 3: Component Methods を作成する**

`component-methods.md` に主要メソッドを高レベルに書く。

例:

```markdown
### Decision Orchestrator
- `generateMorningPlan(userId, date, context)`: 朝の生活プランを生成する。
- `decideNow(userId, decisionRequest, context)`: 即決ボタンの一択判断を生成する。
```

- [ ] **Step 4: Services を作成する**

`services.md` にサービス層を定義する。

- Morning Plan Service
- Instant Decision Service
- Laziness Progression Service
- Safety Evaluation Service
- Preparation Service

- [ ] **Step 5: Component Dependency を作成する**

`component-dependency.md` に依存マトリクスとデータフローを書く。Decision Orchestrator が中心で、Safety Guardrails を必ず通る構成にする。

- [ ] **Step 6: Consolidated Application Design を作成する**

`application-design.md` に Application Design の要約と各詳細ファイルへのリンクを置く。

- [ ] **Step 7: Application Design 成果物を確認する**

Run: `Select-String -LiteralPath 'aidlc-docs/inception/application-design/components.md' -Pattern 'Decision Orchestrator','Safety Guardrails','Laziness Level'`

Expected: 中核コンポーネントが検出される。

- [ ] **Step 8: Application Design 成果物をコミットする**

```bash
git add aidlc-docs/inception/plans/application-design-plan.md aidlc-docs/inception/application-design/components.md aidlc-docs/inception/application-design/component-methods.md aidlc-docs/inception/application-design/services.md aidlc-docs/inception/application-design/component-dependency.md aidlc-docs/inception/application-design/application-design.md
git commit -m "docs: add application design artifacts"
```

---

### Task 7: Unit of Work 成果物を作成する

**Files:**
- Create: `aidlc-docs/inception/plans/unit-of-work-plan.md`
- Create: `aidlc-docs/inception/application-design/unit-of-work.md`
- Create: `aidlc-docs/inception/application-design/unit-of-work-dependency.md`
- Create: `aidlc-docs/inception/application-design/unit-of-work-story-map.md`

- [ ] **Step 1: Unit of Work Plan を作成する**

`unit-of-work-plan.md` に、Unit 分解の判断基準を書く。

判断基準:

- ユーザー体験として独立して説明できる
- Construction フェーズで作業単位にできる
- Safety Guardrails との依存を明確にできる
- ストーリーとの対応が追跡できる

- [ ] **Step 2: Unit of Work を作成する**

`unit-of-work.md` に次の Unit を定義する。

- UOW-01: Decision Core
- UOW-02: Context and Preference Memory
- UOW-03: Laziness Level and Delegation Control
- UOW-04: Safety Guardrails
- UOW-05: Preparation and Recommendation Delivery
- UOW-06: User Experience Surface

- [ ] **Step 3: Unit Dependency を作成する**

`unit-of-work-dependency.md` に、Unit 間の依存関係を書く。特に UOW-01 は UOW-02、UOW-03、UOW-04 に依存し、UOW-05 と UOW-06 に結果を渡す構成にする。

- [ ] **Step 4: Unit Story Map を作成する**

`unit-of-work-story-map.md` に、Task 4 で作成した各ストーリーと UOW の対応表を書く。

- [ ] **Step 5: Unit 成果物を確認する**

Run: `Select-String -LiteralPath 'aidlc-docs/inception/application-design/unit-of-work.md' -Pattern 'UOW-01','UOW-04','Safety Guardrails'`

Expected: UOW-01、UOW-04、安全境界に関する記述が検出される。

- [ ] **Step 6: Unit 成果物をコミットする**

```bash
git add aidlc-docs/inception/plans/unit-of-work-plan.md aidlc-docs/inception/application-design/unit-of-work.md aidlc-docs/inception/application-design/unit-of-work-dependency.md aidlc-docs/inception/application-design/unit-of-work-story-map.md
git commit -m "docs: add unit of work decomposition"
```

---

### Task 8: 全体品質を検証して提出前状態に整える

**Files:**
- Verify: `README.md`
- Verify: `aidlc-docs/**/*.md`
- Verify: `docs/superpowers/specs/2026-04-30-t-ai-da-design.md`

- [ ] **Step 1: 必須ファイルの存在を確認する**

Run:

```powershell
Test-Path README.md
Test-Path aidlc-docs/aidlc-state.md
Test-Path aidlc-docs/audit.md
Test-Path aidlc-docs/inception/requirements/requirements.md
Test-Path aidlc-docs/inception/user-stories/stories.md
Test-Path aidlc-docs/inception/application-design/unit-of-work.md
```

Expected: すべて `True`。

- [ ] **Step 2: 審査基準キーワードを確認する**

Run:

```powershell
Select-String -Path README.md,aidlc-docs/**/*.md -Pattern 'Intent','Unit','怠惰レベル','T-AI-DA','Safety Guardrails'
```

Expected: README と複数の `aidlc-docs/` ファイルでキーワードが検出される。

- [ ] **Step 3: Markdown のリンクと見出しを目視確認する**

Run: `Get-Content -LiteralPath 'README.md' -TotalCount 160`

Expected: 主要リンクが相対パスで記載され、審査員向けの読み順が分かる。

- [ ] **Step 4: Git 差分を確認する**

Run: `git diff --stat`

Expected: README と `aidlc-docs/` 配下の Markdown だけが大きく増えている。`AGENTS.md` と参加規約 PDF は差分に含まれない。

- [ ] **Step 5: Whitespace を確認する**

Run: `git diff --check`

Expected: 出力なし。

- [ ] **Step 6: 最終コミットを作成する**

```bash
git add README.md aidlc-docs
git commit -m "docs: complete AI-DLC inception package"
```

---

## Completion Criteria

- `README.md` から T-AI-DA の Intent、MVP、テーマ適合、AI-DLC 成果物へのリンクが分かる。
- `aidlc-docs/` 配下に Inception フェーズ成果物が揃っている。
- Unit 分解が `unit-of-work.md`、`unit-of-work-dependency.md`、`unit-of-work-story-map.md` で追跡できる。
- Safety Guardrails が Requirements、Stories、Application Design、Unit 分解のすべてに現れる。
- `git diff --check` が通る。
- 変更がコミットされている。
