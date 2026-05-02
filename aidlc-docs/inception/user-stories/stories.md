# User Stories

## Story US-000: T-AI-DA に自分のことを教える

As a T-AI-DA を初めて使うユーザー,
I want 自分の好み、予算、生活圏を登録したい,
so that T-AI-DA が自分に合った一択の判断を返せるようになる。

### Acceptance Criteria

- Given ユーザーが T-AI-DA を初めて起動した, when セットアップ画面が表示される, then 食の好み、予算感、生活圏の入力を促す。
- Given 最小限の好みと予算が登録されている, when 初回の生活プランを生成する, then 不足情報を補完しながら一択のプランを提示する。
- Given 登録情報が不足している, when 判断を依頼する, then T-AI-DA は不足している情報を短く問い、補完した上で一択回答を返す。
- Given 登録情報を変更したい, when ユーザーが設定を更新する, then 次回以降の判断に反映される。

### Linked Requirements

- FR-007
- DCR-003
- DCR-005
- NFR-004

## Story US-001: 朝の生活プランを受け取る

As a 一人暮らしの決断疲れビジネスパーソン,
I want T-AI-DA に朝の生活プランを一択で決めてもらいたい,
so that 出勤前に食事、服装、移動、夜の過ごし方で迷わず行動できる。

### Acceptance Criteria

- Given ユーザーの予定、天気、好み、予算が登録されている, when 朝の生活プラン生成の定刻になる, then T-AI-DA はその日の低リスクな生活プランを提示する。
- Given 複数候補が存在する, when T-AI-DA がプランを提示する, then 比較リストではなく一つの推奨案を主表示する。
- Given プランに買い物や移動が含まれる, when T-AI-DA が結果を表示する, then 準備に必要なリスト、店舗候補、ルート候補を添える。
- Given 判断が医療、法務、高額購入などに関わる, when プラン生成時に検出する, then 自動決定せず対象外または承認必須として扱う。

### Linked Requirements

- FR-001
- FR-004
- FR-005
- NFR-001

## Story US-002: 食事を一択で決めてもらう

As a 仕事後に食事を考えたくないユーザー,
I want T-AI-DA に今日の食事を決めてもらいたい,
so that メニューや店を比較せずに夕食へ移れる。

### Acceptance Criteria

- Given 食の好み、予算、現在地または生活圏が登録されている, when 食事判断を依頼する, then T-AI-DA は一つの食事案を返す。
- Given 推奨案が返されている, when ユーザーが理由を確認する, then 好み、予算、天気、時間帯に基づく短い理由を表示する。
- Given 外食または購入が必要な案である, when T-AI-DA が結果を表示する, then 店舗候補、移動候補、注文リンク候補などの準備支援を添える。

### Linked Requirements

- FR-002
- FR-004
- NFR-002

## Story US-003: 服装を決めてもらう

As a 朝に服装で迷うユーザー,
I want T-AI-DA に天気と予定に合う服装を決めてもらいたい,
so that 朝の小さな判断を減らせる。

### Acceptance Criteria

- Given 天気、予定、好みが登録されている, when 朝の生活プランを生成する, then T-AI-DA は服装方針を一つ提示する。
- Given 気温差や雨の可能性がある, when T-AI-DA が服装を提示する, then 傘や羽織りなど低リスクな準備物も添える。
- Given 予定情報が不足している, when T-AI-DA が服装を提示する, then 不足を明示した上で安全側の一般案を提示する。

### Linked Requirements

- FR-001
- FR-004
- DCR-001
- DCR-002

## Story US-004: 買い物候補と準備リストを受け取る

As a 生活用品や食材の買い物を先延ばしにしがちなユーザー,
I want T-AI-DA に買い物候補と準備リストを出してほしい,
so that 自分で比較せずに必要な準備を進められる。

### Acceptance Criteria

- Given 予算、好み、生活圏が登録されている, when T-AI-DA が買い物を含む生活プランを生成する, then T-AI-DA は低リスクな買い物候補を提示する。
- Given 買い物候補が提示された, when 金額や影響が高リスク条件に該当する, then 自動決定せず承認要求または対象外にする。
- Given 買い物候補が低リスクである, when T-AI-DA が結果を表示する, then 買い物リスト、店舗候補、注文リンク候補を添える。

### Linked Requirements

- FR-004
- FR-005
- NFR-001

## Story US-005: 即決ボタンで迷いを投げる

As a 小さな迷いで手が止まるユーザー,
I want 即決ボタンに質問を投げたい,
so that T-AI-DA が一択で決めてくれる。

### Acceptance Criteria

- Given ユーザーが低リスクな質問を入力する, when 即決ボタンを押す, then T-AI-DA は一つの決定と短い理由を返す。
- Given 入力が曖昧である, when 登録済みの好み・予定・予算から補完できる, then T-AI-DA はそれらを使って一択回答を返す。
- Given 入力が高リスク領域に該当する, when 即決ボタンを押す, then T-AI-DA は自動決定せず、理由と制限を説明する。

### Linked Requirements

- FR-002
- FR-005
- NFR-002

## Story US-006: 怠惰レベルが上がる

As a T-AI-DA に任せることに慣れてきたユーザー,
I want 低リスクな判断の委譲度を段階的に上げたい,
so that 使うほど自分で決める量を減らせる。

### Acceptance Criteria

- Given ユーザーが提案を承認、却下、修正した履歴がある, when T-AI-DA が次の判断を行う, then その軽量フィードバックを怠惰レベルの判断材料にする。
- Given 怠惰レベルが低い, when 判断を提示する, then 提案モードとしてユーザーが選ぶ余地を残す。
- Given 怠惰レベルが上がっている, when 低リスク領域の判断を行う, then 半自動モードまたは低リスク自動決定モードとして提示する。
- Given 怠惰レベルが変化した, when 次の判断を提示する, then 現在のレベルと委譲範囲の変化を短いメッセージでユーザーに通知する。
- Given 高リスク領域である, when 怠惰レベルが高い, then 自動決定に移行しない。

### Linked Requirements

- FR-003
- FR-006
- DCR-006
- NFR-001
- NFR-002

## Story US-007: 高リスク判断で承認を求められる

As a 安全に甘やかされたいユーザー,
I want T-AI-DA が危ない判断を勝手に決めないでほしい,
so that 便利さと責任境界を両立できる。

### Acceptance Criteria

- Given 入力または生成案が医療、法務、雇用、契約、高額購入、重大な人間関係に該当する, when T-AI-DA が評価する, then 自動決定しない。
- Given 高リスク判断が検出された, when T-AI-DA がユーザーに結果を返す, then 何が制限対象かを短く説明する。
- Given 承認フローが導入されている（将来拡張）, when 承認が必要な判断である, then ユーザーの明示承認なしに実行準備を進めない。

### Linked Requirements

- FR-005
- NFR-001
- NFR-002

## Story US-008: 低リスクな準備支援を受ける

As a 判断後の準備も面倒なユーザー,
I want T-AI-DA に次の行動の準備まで整えてほしい,
so that 決定から行動までの摩擦を減らせる。

### Acceptance Criteria

- Given T-AI-DA が低リスクな判断を返した, when 準備支援が可能である, then 買い物リスト、店舗候補、ルート候補、注文リンク候補を提示する。
- Given 準備支援が外部サービス連携を必要とする, when MVP では該当サービスが未連携である, then 実行ではなく候補提示に留める。
- Given 準備候補が複数ある, when T-AI-DA が結果を表示する, then 主推奨を一つに絞り、補助情報として理由を添える。

### Linked Requirements

- FR-004
- NFR-005
- DCR-004

## Story Map Summary

| Story | Primary Persona | Key Components |
| --- | --- | --- |
| US-000 | 全ペルソナ | User Context |
| US-001 | 佐藤 悠真 | Decision Orchestrator, User Context, Preparation Assistant |
| US-002 | 佐藤 悠真 | Decision Orchestrator, T-AI-DA Persona, Preparation Assistant |
| US-003 | 佐藤 悠真 | User Context, Decision Orchestrator |
| US-004 | 田中 美咲 | Preparation Assistant, Safety Guardrails |
| US-005 | 佐藤 悠真 | Decision Orchestrator, Safety Guardrails |
| US-006 | 佐藤 悠真 | Laziness Level, User Context |
| US-007 | 全ペルソナ | Safety Guardrails |
| US-008 | 佐藤 悠真 | Preparation Assistant, Notification and Delivery |
