# プロフィール画像の更新

`profile/stats.svg`、`profile/top-langs.svg`、`profile/trophy.svg` は
`.github/workflows/update-profile.yml` で生成します。
README は保存済みの画像を参照するため、生成元の障害で画像が消えることはありません。

- 毎日 06:17 JST に更新します。GitHub 側の混雑で実行時刻が遅れる場合があります。
- 手動更新は GitHub の Actions → Update profile cards → Run workflow から実行します。
- ワークフローファイルまたは `.node-version` を変更したブランチへの push でも実行します。
- 3画像の生成・Node.jsバージョン検証・SVG検証がすべて成功した場合だけ、実行ブランチへコミットします。
- 失敗時は Actions のログを確認してください。保存済みの画像は前回の状態を維持します。
- 認証には GitHub が発行する `GITHUB_TOKEN` を使います。個人アクセストークンの登録は不要です。
- Action はコミットSHA、統計生成ライブラリはバージョン番号で固定しています。更新時はブランチで生成結果を確認してください。

## Node.js の更新

カード生成用の Node.js は `.node-version` で管理します。
先に指定版をランナーのツールキャッシュへ追加し、統計生成 Action 内部の `24.x` 指定がキャッシュの最新修正版を選ぶようにします。
生成後は、実行した Node.js が `.node-version` と同じメジャー版で、指定版以上であることを検証します。
Action 実行用の内蔵 Node.js は GitHub 管理ランナーの更新対象です。

1. `.node-version` を修正版へ更新してブランチへ push します。
2. Actions の `Generate stats` と `Generate top languages` のログで、修正版が選択されたことを確認します。
3. `Validate Node.js and generated SVGs` の成功と、生成された3画像を確認します。

## 生成元

- 統計・使用言語: https://github.com/stats-organization/github-readme-stats-action
- トロフィー: https://github.com/ryo-ma/github-profile-trophy

活動グラフは既存の外部画像を継続利用しています。

## 閲覧カウンターとZenn

リンク先の正本は README.md です。

- 閲覧カウンターは [Hits](https://github.com/silentsoft/hits) の外部SVGを使います。閲覧時の取得で計測するため、画像更新ワークフローには含めません。
- 2026-10-20、Komarev の画像が GitHub の画像プロキシ（Camo）経由で404になることを確認し、Hitsへ切り替えました。[配信元の障害報告](https://github.com/antonkomarev/github-profile-views-counter/issues/122)もあります。
- 移行時に Komarev から取得できた累計3,631回を `extraCount` に設定しています。これは固定の引き継ぎ値です。通常の更新で変更したり、現在の累計を再加算したりしないでください。
- カウンターは画像の取得回数が基準で、ユニーク訪問者数ではありません。GitHub の画像キャッシュにより、再読み込みのたびに増えるとは限りません。
- Zenn は `tab=articles` を指定して記事一覧へ直接リンクします。旧 `/tecsoc/articles` はプロフィールの Overview へリダイレクトされます。記事数バッジは表示しません。

### 変更時・表示不具合時の確認

1. README の Zenn リンクから記事一覧が開き、一覧内の記事を開けることを確認します。PC幅とモバイル幅の両方で確認してください。
2. カウンターは配信元へのアクセスだけでなく、GitHub が描画した画像の `camo.githubusercontent.com` URLでも HTTP 200 と数値入りSVGが返ることを確認します。
3. カウンターが表示されない場合は、配信元と Camo の応答を切り分けます。キャッシュの復旧は [GitHub の手順](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-anonymized-urls)に従います。配信元を変更する場合は、取得できた累計を引き継ぎ、GitHub経由の画像表示まで再確認します。
