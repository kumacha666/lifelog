# LifeLog — 開発コンテキスト

## アプリ概要
日常の細かな記録を毎日つけるライフログ＋ライフコーチ PWA。

## 設計思想
- **カテゴリ駆動**：コーディネート・食事・サプリなど、ユーザーが自分でカテゴリを定義する
- **アイテム事前登録**：持ち物リストを登録しておき、記録時はタップで選ぶだけ
- **最小限でも成立**：アイテムなしでもチェックイン記録が可能、多機能にも対応
- **ローカルファースト**：データは localStorage に保存、サーバー不要
- **PWA**：スマホのホーム画面に追加してアプリとして使用可能

## カテゴリタイプと特徴
- `fashion`：バリエーション率・未使用アイテム提案・最多使用アイテム
- `food`：カロリー記録・平均カロリー評価・食品多様性
- `supplement`：連続記録ストリーク・30日ドット表示
- `exercise`：時間・距離・歩数の記録
- `body`：体重・体脂肪率の記録
- `purchase`：金額記録・月間支出集計
- `custom`：自由記録

## 技術構成
- シングルファイル HTML（index.html）+ manifest.json + sw.js
- フレームワーク不使用、バニラ JS
- データ構造：`{ cats: [], logs: { "YYYY-MM-DD": { catId: { v, kcal, yen, min, km, steps, wt, fat, note } } }, shopping: [] }`
- localStorage キー：`lifelog_v2`
- カレンダー表示：HTML `<table>` + `table-layout: fixed`（CSS Gridは互換性問題あり）

## ホスティング・計測
- GitHub Pages：`https://kumacha666.github.io/lifelog/`
- Google Analytics 4：測定ID `G-1WL6P6ZEXV`

## フィードバック
- Google フォーム：`https://docs.google.com/forms/d/e/1FAIpQLSd8h6BKgB77_rI-b0S7XBJ7vFqDjd3yvxNIYoT-MAaNpSWq0g/viewform`
- フォーム作成用GASスクリプト：`tools/create-feedback-form.gs`（clasp対応）

## ユーザーの環境
- スマホ（Android Chrome）でダークモード使用
- PCではEdge・Chromeで動作確認済み

## 開発ワークフロー
- ブランチ：機能ごとにブランチを切る
- PR：作成後、Claudeがsquash mergeでmainにマージ（ユーザー承認済み）
- デプロイ：mainへのマージで GitHub Pages に自動デプロイ

## オンボーディング
- 初回チュートリアル：インタラクティブ形式（ステップ1〜4）
- お買い物リストTipsカード：初回表示 + ?ボタンで再表示
- カテゴリ編集画面のアイテム登録Tips：同上
- localStorage キー：`lifelog_tut_done`, `lifelog_shop_tip_done`, `lifelog_item_tip_done`

## 既知の課題・対応済み
- ダークモードでチップの文字・背景が見づらい → dark mode CSS override で対応済み
- カレンダー表示崩れ（CSS Grid + aspect-ratio問題）→ HTML tableに変更で解決済み
- チュートリアル中にモーダルを開くとオーバーレイが残る → openCatEdit / openLog でクリア処理追加済み
- アイテムなしカテゴリで保存が無反応 → 空ログ（チェックイン記録）を許可で解決済み

## リポジトリ構成（プロジェクト横断）
- `kumacha666/ai-workspace` (private)：ブレスト・設計・非公開作業
- `kumacha666/apps` (public)：今後の公開アプリ置き場
- `kumacha666/lifelog` (public)：本アプリ（既存のまま維持）
- セッション開始時は ai-workspace + apps（+ 必要に応じて個別リポジトリ）を接続
