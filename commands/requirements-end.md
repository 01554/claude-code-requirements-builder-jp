# 要件収集の終了

現在の要件収集セッションを終了します。

## 手順:

1. requirements/.current-requirement を読み込む
2. アクティブな要件がない場合:
   - "終了する要件がありません" と表示
   - 終了

3. 現在のステータスを表示し、ユーザーの意図を確認:
   ```
   ⚠️ 要件を終了します: [name]
   現在のフェーズ: [phase] ([X/Y] 完了)
   
   どのように処理しますか？
   1. 現在の情報で仕様書を生成
   2. 後で続けるため未完了としてマーク
   3. キャンセルして削除
   ```

4. 選択に基づいて処理:

### オプション 1: 仕様書の生成
- 06-requirements-spec.md を作成
- 回答済みの全質問を含める
- 未回答の質問には "想定:" プレフィックスでデフォルト値を追加
- 実装のヒントを生成
- メタデータのステータスを "complete" に更新

### オプション 2: 未完了としてマーク
- メタデータのステータスを "incomplete" に更新
- "lastUpdated" タイムスタンプを追加
- 進捗のサマリーを作成
- まだ必要な項目を記録

### オプション 3: キャンセル
- 削除を確認
- 要件フォルダを削除
- .current-requirement をクリア

## 最終仕様書のフォーマット:
```markdown
# 要件仕様書: [Name]

生成日時: [timestamp]
ステータス: [X個の想定を含む完了 / 部分的]

## 概要
[問題の説明とソリューションのサマリー]

## 詳細要件

### 機能要件
[回答された質問に基づく]

### 技術要件
- 影響を受けるファイル: [パス付きリスト]
- 新規コンポーネント: [ある場合]
- データベース変更: [ある場合]

### 前提条件
[未回答の質問に使用されたデフォルト値のリスト]

### 実装メモ
[実装のための具体的なガイダンス]

### 受け入れ基準
[完了のためのテスト可能な基準]
```

5. .current-requirement をクリア
6. requirements/index.md を更新