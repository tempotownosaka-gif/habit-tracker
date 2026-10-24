# 習慣トラッカー 引き継ぎメモ

## 目的
iPhoneのホーム画面から、サインインなしで開ける習慣トラッカー（Webアプリ）として公開する。

## ファイル構成（habit-tracker-site.zip）
- index.html … アプリ本体（HTML/CSS/JSが1ファイル）
- manifest.webmanifest, icon-192.png, icon-512.png, icon-512-maskable.png, apple-touch-icon.png … ホーム画面用（すべて相対パス）

## データの扱い
- 保存先は localStorage のキー `habit-tracker-state`（URL単位で端末内に保存。端末間の共有なし）
- 形式: `{ habits: [{ id, name, createdAt, freqType, freqCount }], logs: { "YYYY-MM-DD": { <habitId>: true } } }`
- freqType は `daily` / `weekly` / `monthly`（未設定の古いデータは daily 扱い）
- 画面下部の「記録をコピー」「記録を復元」でバックアップと復元ができる
- 形式を変える場合は、読み込み時（loadLocal）に古い形式を変換する処理を入れること

## 実装済みの機能
- 習慣の追加（毎日／週に◯回／月に◯回）
- 丸いスタンプで今日の達成をチェック、直近35日のドット表示、連続日数と期間内の達成回数
- 上部の統計（最長連続、今週のスタンプ数、今週の達成率）とひとことメッセージ
- 直近8週間の週間達成率グラフ
- 削除の二重確認（1回目で「本当に削除」に変わり、3秒で元に戻る）

## 公開の手順（未実施）
1. GitHubに空のリポジトリを作る（例: habit-tracker）
2. zipの中身をリポジトリのルートに置いて push
3. GitHub Pages を有効化（Settings → Pages → main ブランチ / root）
4. 発行されたURLをiPhoneのSafariで開き、共有 → 「ホーム画面に追加」
5. 更新するときは同じリポジトリに上書き push（URLが変わらなければ記録は残る）

## 現在の状況
- Claude側のセッションでは GitHub が未連携のため、公開まで進められていない
- 続きをやるには、claude.ai の設定で GitHub を連携し、対象リポジトリの owner/repo を伝える
