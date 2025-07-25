# Agile Simulator MVP要件定義書

## 1. ゲーム概要

### 1.1 コンセプト
「Agile Simulator」は、アジャイル開発の実践を学べる経営シミュレーション×パズルゲームです。
プレイヤーはソフトウェア開発チームのリーダーとして、スクラム開発を通じてプロジェクトを成功に導きます。

### 1.2 ターゲットユーザー
- アジャイル開発に興味がある学生・新人エンジニア
- スクラムの実践を楽しく学びたい開発者
- チームマネジメントに興味があるゲーマー

## 2. ゲームメカニクス

### 2.1 コアループ
1. **プロジェクト受注フェーズ**
  - 3つのプロジェクト提案から1つを選択
  - 難易度、報酬、期限が異なる

2. **チーム編成フェーズ**
  - 予算内でチームメンバーを雇用
  - エンジニアのみ（MVPでは単一職種）

3. **スプリント実行フェーズ**（2週間を1スプリントとして表現）
  - スプリント計画：バックログからタスクを選択
  - デイリー実行：各メンバーにタスクを割り当て、パズルで解決
  - スプリントレビュー：完成した機能を確認

4. **プロジェクト完了フェーズ**
  - 顧客満足度の評価
  - 報酬の獲得
  - チーム経験値の獲得

### 2.2 パズルシステム

#### エンジニアパズル（コーディング）
- **基本メカニクス**：パイプつなぎ型パズル
- **表現**：データフローを正しく接続して機能を実装
- **難易度要素**：
  - 簡単：単純な一本道
  - 中級：分岐や条件付きフロー
  - 難関：複数の入出力、エラー処理
- **成功条件**：すべての入力が正しい出力に到達


### 2.3 チームメンバーシステム

#### メンバーステータス
- **スキルレベル**（1-5）：パズルの初期ヒント数に影響
- **経験値**：タスク完了で上昇、レベルアップでスキル向上
- **モチベーション**（0-100）：パズル解決速度に影響
- **特性**：
  - 「集中型」：難しいタスクで能力UP
  - 「協調型」：ペアワーク時にボーナス
  - 「スピード型」：簡単なタスクを高速処理

#### モチベーション管理
- 成功体験で上昇（+10〜20）
- 失敗や過労で低下（-10〜30）
- チームイベントで回復（振り返り会、勉強会）

## 3. プロジェクト進行システム

### 3.1 バックログ管理
- **ユーザーストーリー**：顧客要求を表現
  - 例：「ユーザーとして、商品を検索したい」
- **タスク分解**：ストーリーを具体的なタスクに
  - フロントエンド実装
  - バックエンド実装

### 3.2 ベロシティとスプリント計画
- チームの1スプリントで処理可能なポイント数
- 過去の実績から自動計算
- プレイヤーは計画時に無理のない範囲でタスクを選択

### 3.3 イベントシステム
**定期イベント**
- スプリントレビュー：完成機能のデモ
- レトロスペクティブ：チーム改善の機会

## 4. 勝利条件と評価

### 4.1 プロジェクト成功条件
- 期限内に必須機能をすべて完成
- 品質基準（バグ率5%以下）を満たす
- 予算内で完了

### 4.2 評価指標
- **顧客満足度**（★1-5）
  - 機能の完成度
  - 品質
  - 納期順守
- **チーム満足度**（0-100）
  - 平均モチベーション
  - スキル成長度
  - 残業時間

### 4.3 スコアリング
- 基本スコア = 顧客満足度 × 1000
- ボーナス = チーム満足度 × 10
- ペナルティ = バグ数 × -50

## 6. UI/UX要件

### 6.1 メイン画面構成
- **オフィス画面**：チームメンバーの配置、状態確認
- **バックログ画面**：タスクの一覧、優先順位設定
- **パズル画面**：エンジニアパズルを実行
- **ダッシュボード**：進捗、ベロシティ、満足度を可視化

### 6.2 操作性
- ドラッグ&ドロップでタスク割り当て
- ワンクリックでメンバー状態確認
- キーボードショートカット対応

## 7. 技術要件（MVP）

### 7.1 対応プラットフォーム
- PC（Windows/Mac/Linux）
- Webブラウザ対応

### 7.2 最小システム要件
- 解像度：1280×720以上
- メモリ：2GB以上
- 安定したインターネット接続（オンラインランキング用）

## 8. MVP開発スコープ

### 含むもの
- エンジニア職種とパズル
- シンプルなプロジェクト進行
- 基本的なチーム管理機能
- ローカルセーブ機能

### 含まないもの（将来の拡張）
- オンライン対戦/協力プレイ
- 詳細なカスタマイズ機能
- 追加の開発手法（カンバン、XP）
- モバイル対応
- MOD対応

