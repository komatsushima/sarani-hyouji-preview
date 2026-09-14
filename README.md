# さらに表示プレビュー

Xのポスト本文を貼ると、モバイルアプリで「さらに表示」に隠れる範囲を推定し、iPhone風の画面でプレビューする改行チェッカー。

- `index.html` 1ファイルで完結（ビルド不要、外部ライブラリなし。フォントのみ Google Fonts）
- 入力内容はブラウザの localStorage に保存され、次回開いたときに復元される

## Netlify で公開する

1. このリポジトリを GitHub にプッシュ（Private で可）
2. Netlify → **Add new site → Import an existing project → GitHub** でこのリポジトリを選ぶ
3. 設定はそのまま（`netlify.toml` が読まれる）
   - Build command: 空
   - Publish directory: `.`
4. **Deploy site**。以降は `main` に push するたびに自動で再デプロイされる

URLを社外に見せたくない場合は、Netlify の Site configuration → Access & security → **Password protection**（Pro以上）か、共有先を限定する運用で。

## 判定ロジック（概要）

- 行数ルール（モバイルのみ）: 空行・折り返しも1行として数え、10行以上なら9行目まで表示（9行目は末尾1字が「…さらに表示」に置き換わる）。折りたたみ表示では空行が詰められる。装飾行や空行が多い投稿は実機で1〜2行多く見えることがある（推定は安全側）
- 文字数ルール: 加重文字数（全角・絵文字=2、半角=1、URL=23）が280を超えると280の手前で切れる
- 両方に当てはまる場合は先に来た方。PC（ブラウザ）は文字数ルールのみ

作成：[arne 松島](https://github.com/komatsushima)
