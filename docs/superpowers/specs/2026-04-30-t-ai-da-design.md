# T-AI-DA 設計メモ

## 目的

AWS Summit Japan 2026 AI-DLC ハッカソンの書類審査に向けて、提出用ドキュメント一式の設計方針を定義する。

提出物は公開 GitHub リポジトリとし、審査員向けの `README.md` と、AI-DLC の Inception フェーズ成果物を含める。

## プロダクトコンセプト

T-AI-DA は、日常の小さな意思決定に疲れた一人暮らしのビジネスパーソンに向けた、AWS ベースの意思決定代行サービスである。

名称は「怠惰（Taida）」と「AI」を組み合わせたもの。コンセプトは、人を徹底的に甘やかし、日々の小さな意思決定を奪うことにある。サービスは朝の「今日の生活プラン」生成から始まり、必要に応じて使える「即決ボタン」を提供する。

最終ビジョンは、日常生活、消費、ライフスタイル、健康関連ルーティン、人間関係まで、低リスクな意思決定を段階的に代行する「人生 OS」である。一方で MVP は、低リスクな日常判断に範囲を絞る。

## 対象ユーザー

主要ペルソナは、一人暮らしのビジネスパーソンである。

仕事で認知リソースを使い切っており、退勤後や休日に「何を食べるか」「何を着るか」「何を買うか」「何をするか」を考えたくないユーザーを対象にする。

## 中核体験

T-AI-DA は MVP として、主に 2 つの体験を提供する。

1. 朝の生活プラン生成
   - 食事、服装、移動、買い物準備、夜の過ごし方を決める。
   - 比較候補の一覧ではなく、実行しやすい一択の推奨プランを提示する。

2. 即決ボタン
   - 「何を食べるか」「買うべきか」「空き時間をどう使うか」といった小さな迷いを扱う。
   - 短い理由と準備手順を添えて、一つの決定を返す。

プロダクトの人格は「過保護だが少し皮肉な執事」とする。ユーザーを安心させながら、静かに意思決定筋を弱らせていく。

## 怠惰レベルモデル

サービスは、段階的な意思決定委譲モデルを採用する。

1. 提案モード
   - T-AI-DA が判断候補を提示し、ユーザーが選ぶ。

2. 半自動モード
   - T-AI-DA が標準で決定するが、ユーザーは差し戻しや修正ができる。

3. 低リスク自動決定モード
   - 安全な日常領域では、T-AI-DA が決定し、次の行動準備まで行う。

この進行は「怠惰レベル」として表現する。T-AI-DA が便利になるほどユーザーが決める必要がなくなる、というハッカソンテーマをプロダクト機能そのものに変換する。

## スコープとガードレール

MVP の対象範囲:

- 食事
- 服装
- 日々の予定提案
- 買い物候補
- 週末や夜の過ごし方
- 買い物リスト、店舗候補、ルート、注文リンクなどの準備支援

将来的な対象範囲:

- 購買履歴
- カレンダーと健康ログ
- ライフスタイル最適化
- 厳格な制限付きの人間関係関連提案

対象外、または明示的な承認が必要な意思決定:

- 高額購入
- 医療診断や治療判断
- 法務、契約、雇用、退職、別れに関する判断
- 金融、健康、法律、人間関係に重大な影響を与える判断

## 提出パッケージ

リポジトリは 2 層構造にする。

1. 審査員向け README
   - プロダクトの一文説明
   - 対象ユーザーと課題
   - ビジネス意図
   - テーマ適合性
   - MVP 体験
   - AWS アーキテクチャ概要
   - AI-DLC 成果物へのリンク

2. `aidlc-docs/` 配下の AI-DLC 成果物
   - `aidlc-docs/aidlc-state.md`
   - `aidlc-docs/audit.md`
   - `aidlc-docs/inception/requirements/requirements.md`
   - `aidlc-docs/inception/requirements/requirement-verification-questions.md`
   - `aidlc-docs/inception/user-stories/personas.md`
   - `aidlc-docs/inception/user-stories/stories.md`
   - `aidlc-docs/inception/plans/execution-plan.md`
   - `aidlc-docs/inception/application-design/application-design.md`
   - `aidlc-docs/inception/application-design/components.md`
   - `aidlc-docs/inception/application-design/component-methods.md`
   - `aidlc-docs/inception/application-design/services.md`
   - `aidlc-docs/inception/application-design/component-dependency.md`
   - `aidlc-docs/inception/application-design/unit-of-work.md`
   - `aidlc-docs/inception/application-design/unit-of-work-dependency.md`
   - `aidlc-docs/inception/application-design/unit-of-work-story-map.md`

## 初期 Unit 分解

1. Decision Orchestrator
   - 朝の生活プランと即決判断を組み立てる。

2. User Context
   - 天気、予定、好み、位置情報、予算など、MVP に必要な文脈を管理する。

3. T-AI-DA Persona
   - 過保護だが少し皮肉な執事としての応答体験を生成する。

4. Laziness Level
   - 提案型、半自動型、低リスク自動決定型への移行を制御する。

5. Safety Guardrails
   - 高リスクな意思決定領域を検出し、承認要求または拒否へ誘導する。

6. Preparation Assistant
   - 買い物リスト、店舗候補、ルート、注文リンクを生成する。

## 審査戦略

ドキュメントパッケージは、書類審査基準に意図的に対応させる。

- ビジネス意図（Intent）の明確さ
  - 「決断疲れ」を中核課題として示し、T-AI-DA を明確な意思決定代行システムとして表現する。

- Unit 分解の適切さ
  - Unit を明示し、それぞれの責務とユーザーストーリーを接続する。

- 創造性とテーマ適合性
  - 「怠惰レベル」を中核のプロダクトメカニクスとして提示する。

- ドキュメントの品質
  - `README.md` は審査員が短時間で把握しやすい構成にし、AI-DLC 成果物は追跡可能で一貫した構造にする。

## 承認状況

ユーザーは以下を承認済み。

- プロダクト方針: 怠惰レベルが上がる意思決定 OS
- 名称: T-AI-DA
- MVP スコープ: 朝の生活プランと即決ボタン
- 対象ユーザー: 一人暮らしの決断疲れビジネスパーソン
- ガードレール方針: MVP は低リスク領域に限定し、将来拡張も制約付きで行う
- 提出パッケージ構成
