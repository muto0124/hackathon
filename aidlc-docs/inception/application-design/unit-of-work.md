# Unit of Work

## UOW-01: Decision Core

### Purpose

朝の生活プラン生成と即決ボタンの判断を統合する中核 Unit。

### Responsibilities

- ユーザー文脈、怠惰レベル、安全評価を組み合わせて一択の判断を生成する。
- 朝の生活プランと即決ボタンの結果形式を統一する。
- T-AI-DA Persona と Preparation Assistant に渡す判断結果を整える。

### Related Components

- Decision Orchestrator
- T-AI-DA Persona
- Morning Plan Service
- Instant Decision Service

### Related Requirements

- FR-001
- FR-002
- NFR-002
- NFR-003

### Construction Candidate

最初の MVP プロトタイプでは、固定サンプル文脈を入力し、朝の生活プランと即決結果を生成する。

## UOW-02: Context and Preference Memory

### Purpose

判断に必要な天気、予定、好み、位置情報、予算、軽量フィードバック履歴を扱う Unit。

### Responsibilities

- MVP に必要なユーザー文脈を読み込む。
- 承認、却下、修正、判断履歴を保存する。
- Decision Core と Laziness Level に正規化済み文脈を渡す。

### Related Components

- User Context
- Amazon DynamoDB candidate

### Related Requirements

- DCR-001
- DCR-002
- DCR-003
- DCR-004
- DCR-005
- DCR-006
- NFR-004

### Construction Candidate

ユーザー設定と判断履歴を DynamoDB 風のデータモデルとして定義し、最初はローカルまたはモックデータで扱う。

## UOW-03: Laziness Level and Delegation Control

### Purpose

提案型、半自動型、低リスク自動決定型の委譲度を制御する Unit。

### Responsibilities

- 軽量フィードバック履歴から怠惰レベルを判定する。
- 判断領域ごとに委譲モードを返す。
- Safety Guardrails の結果を上書きしない。

### Related Components

- Laziness Level
- Laziness Progression Service

### Related Requirements

- FR-003
- DCR-006
- NFR-001

### Construction Candidate

承認、却下、修正の簡易スコアリングにより、委譲モードを返す最小ロジックを作る。

## UOW-04: Safety Guardrails

### Purpose

高リスク判断を検出し、T-AI-DA が自動決定してよい範囲を制限する Unit。

### Responsibilities

- 医療、法務、雇用、契約、高額購入、重大な人間関係の判断を検出する。
- 自動決定可、承認必須、対象外を返す。
- 低リスク自動化と安全境界を両立する。

### Related Components

- Safety Guardrails
- Safety Evaluation Service

### Related Requirements

- FR-005
- NFR-001
- NFR-004

### Construction Candidate

初期 MVP ではルールベースの分類を用い、危険語句や金額閾値で承認必須または対象外に振り分ける。

| 分類 | 判定例 |
| --- | --- |
| 対象外（自動決定しない） | 手術・診断・服薬・解雇・契約解除・離婚・訴訟・借入 などのキーワードを含む |
| 承認必須 | 単品 30,000 円以上、または月間累計 100,000 円以上の購入 |
| 自動決定可 | 食事・服装・生活用品（1,000 円未満）・夜の過ごし方 など |

キーワードリストと金額閾値は将来 Amazon Bedrock Guardrails または Lambda ルールセットに移行できる構成にする。

## UOW-05: Preparation and Recommendation Delivery

### Purpose

判断後の準備支援を生成し、行動に移しやすい形で届ける Unit。

### Responsibilities

- 買い物リスト、店舗候補、ルート候補、注文リンク候補を生成する。
- 複数候補を主推奨一つと補助情報に整理する。
- MVP では購入や予約の実行を行わず、準備候補提示に留める。

### Related Components

- Preparation Assistant
- Preparation Service
- Notification and Delivery

### Related Requirements

- FR-004
- NFR-005
- DCR-004

### Construction Candidate

固定候補または外部 API モックを使って、判断結果に紐づく準備情報を生成する。

## UOW-06: User Experience Surface

### Purpose

朝の生活プランと即決ボタンの結果を、審査員が理解しやすい体験として提示する Unit。

### Responsibilities

- T-AI-DA の過保護で少し皮肉な人格を画面またはメッセージに反映する。
- 判断、理由、準備支援、安全制限を分かりやすく表示する。
- README や将来のデモに接続しやすい UX 表現を提供する。

### Related Components

- T-AI-DA Persona
- Notification and Delivery

### Related Requirements

- FR-001
- FR-002
- NFR-002

### Construction Candidate

最初は静的画面または簡易 Web UI とし、朝の生活プランと即決結果を表示する。
