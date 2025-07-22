# Agile Simulator ゲームシステム設計書

## 1. システムアーキテクチャ

### 1.1 全体構成
```
┌─────────────────────────────────────────────────┐
│                  Game Manager                    │
├─────────────┬─────────────┬────────────────────┤
│ Scene       │ Game Logic  │ Data               │
│ Manager     │ Controller  │ Manager            │
├─────────────┼─────────────┼────────────────────┤
│ UI System   │ Puzzle      │ Save/Load          │
│             │ System      │ System             │
└─────────────┴─────────────┴────────────────────┘
```

### 1.2 主要コンポーネント

#### GameManager
- ゲーム全体の状態管理
- シーン遷移の制御
- イベントシステムの管理

#### SceneManager
- メニュー、ゲームプレイ、結果画面の切り替え
- シーン間のデータ受け渡し

#### GameLogicController
- スプリントの進行管理
- スコア計算
- 勝利/敗北判定

## 2. データ構造

### 2.1 プロジェクトデータ
```json
{
  "projectId": "string",
  "name": "string",
  "client": "string",
  "duration": "number (スプリント数)",
  "budget": "number",
  "requirements": [
    {
      "id": "string",
      "type": "must|should|nice-to-have",
      "storyPoints": "number",
      "description": "string"
    }
  ]
}
```

### 2.2 チームメンバーデータ
```json
{
  "memberId": "string",
  "name": "string",
  "role": "engineer",
  "level": "number (1-5)",
  "experience": "number",
  "motivation": "number (0-100)",
  "skills": {
    "speed": "number",
    "quality": "number",
    "collaboration": "number"
  },
  "traits": ["string"],
  "currentTask": "taskId|null"
}
```

### 2.3 タスクデータ
```json
{
  "taskId": "string",
  "requirementId": "string",
  "type": "frontend|backend",
  "storyPoints": "number",
  "requiredRole": "engineer",
  "difficulty": "easy|medium|hard",
  "status": "todo|in-progress|done|blocked",
  "assignedTo": "memberId|null",
  "progress": "number (0-100)",
  "bugs": "number"
}
```

### 2.4 スプリントデータ
```json
{
  "sprintNumber": "number",
  "capacity": "number (total story points)",
  "plannedTasks": ["taskId"],
  "completedTasks": ["taskId"],
  "velocity": "number",
  "events": [
    {
      "day": "number",
      "type": "string",
      "impact": "object"
    }
  ]
}
```

## 3. ゲームフロー詳細

### 3.1 ゲーム開始フロー
```
1. タイトル画面
   ├─ 新規ゲーム → プロジェクト選択
   ├─ 続きから → セーブデータ選択
   └─ 設定 → 各種設定

2. プロジェクト選択
   └─ 3つのプロジェクトから選択
       └─ チーム編成画面へ

3. チーム編成
   └─ 予算内でメンバーを雇用
       └─ ゲームプレイ開始
```

### 3.2 スプリントサイクル
```
1. スプリント計画 (Sprint Planning)
   - バックログからタスクを選択
   - チームキャパシティの確認
   - タスクの見積もり

2. デイリー実行 (Daily Execution)
   Day 1-10:
   - タスク割り当て
   - パズル実行
   - 進捗更新

3. スプリントレビュー (Sprint Review)
   - 完成タスクの確認
   - 顧客フィードバック
   - バグ報告

4. レトロスペクティブ (Retrospective)
   - チーム振り返り
   - 改善アクション選択
   - 次スプリントへ
```

## 4. パズルシステム詳細設計

### 4.1 エンジニアパズル（フロー接続型）

#### 基本ルール
- グリッド上にスタート地点とゴール地点が配置
- パイプパーツを配置してフローを完成させる
- 制限時間内に完成させる

#### パズル要素
```
基本パーツ:
- 直線パイプ (━, ┃)
- カーブパイプ (┏, ┓, ┗, ┛)
- 分岐パイプ (┣, ┫, ┳, ┻)

特殊パーツ（難易度により追加）:
- 条件分岐 (if文)
- ループ (for/while)
- エラーハンドリング (try-catch)
```

#### 難易度別パラメータ
- Easy: 5×5グリッド、基本パーツのみ、ヒント3つ
- Medium: 7×7グリッド、条件分岐追加、ヒント2つ
- Hard: 9×9グリッド、全パーツ使用、ヒント1つ


## 5. AI/ゲームバランス

### 5.1 難易度調整システム

#### 動的難易度調整
- プレイヤーの成功率を監視
- 3連続成功：難易度を1段階上げる
- 3連続失敗：難易度を1段階下げる

#### 難易度パラメータ
- パズルの複雑さ
- 制限時間
- ヒント数
- 報酬額

### 5.2 チームメンバーAI

#### タスク自動割り当てアルゴリズム
```
1. タスクとメンバーのマッチングスコア計算
   - スキルレベル × 役割適性
   - 現在のモチベーション
   - 特性ボーナス

2. 最適化アルゴリズム
   - 全体の生産性最大化
   - モチベーション維持
   - スキル成長機会の配分
```


## 6. UI/UX実装詳細

### 6.1 画面遷移図
```
タイトル
├─ メインメニュー
│  ├─ プロジェクト選択
│  │  └─ チーム編成
│  │      └─ ゲームプレイ
│  │          ├─ オフィス画面
│  │          ├─ バックログ画面
│  │          ├─ パズル画面
│  │          └─ ダッシュボード
│  ├─ ロード
│  └─ 設定
└─ 結果画面
    └─ メインメニューへ
```

### 6.2 主要画面レイアウト

#### オフィス画面
```
┌────────────────────────────────────────┐
│ [ステータスバー] Day 3/10 Sprint 2     │
├────────────────────────────────────────┤
│                                        │
│  [チームメンバー配置エリア]            │
│  ┌──┐ ┌──┐ ┌──┐                    │
│  │😊│ │😐│ │😓│                    │
│  └──┘ └──┘ └──┘                    │
│                                        │
├────────────────────────────────────────┤
│ [タスクトレイ] □ □ □ □ □            │
└────────────────────────────────────────┘
```

### 6.3 アニメーション仕様

#### 基本アニメーション
- UI要素のフェードイン/アウト: 0.3秒
- 画面遷移: 0.5秒
- タスク完了エフェクト: 1秒
- スコア加算: イージング付き2秒

## 7. セーブデータ構造

### 7.1 セーブデータフォーマット
```json
{
  "version": "1.0.0",
  "saveDate": "ISO 8601 datetime",
  "gameData": {
    "currentProject": "Project object",
    "currentSprint": "number",
    "currentDay": "number",
    "team": ["TeamMember objects"],
    "backlog": ["Task objects"],
    "completedTasks": ["taskId"],
    "score": "number",
    "statistics": {
      "totalVelocity": "number",
      "totalBugs": "number",
      "customerSatisfaction": "number"
    }
  }
}
```

### 7.2 オートセーブ
- スプリント終了時
- 重要な選択後
- 5分ごとの定期保存

## 8. パフォーマンス最適化

### 8.1 レンダリング最適化
- スプライトバッチング
- UIのオブジェクトプール
- 非アクティブ要素の非表示

### 8.2 メモリ管理
- 未使用アセットの解放
- テクスチャ圧縮
- 音声ファイルのストリーミング

## 9. 音響設計

### 9.1 BGM
- メニュー: 落ち着いた雰囲気
- プランニング: 思考を促す静かな曲
- 実行中: テンポの良い作業BGM
- パズル: 集中できるミニマル

### 9.2 効果音
- UI操作音
- タスク完了音
- レベルアップ音
- 警告音（期限迫る、バグ発生）

