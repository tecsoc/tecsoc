# プロフィール画像の更新

`profile/stats.svg`、`profile/top-langs.svg`、`profile/trophy.svg` は
`.github/workflows/update-profile.yml` で生成します。
README は保存済みの画像を参照するため、生成元の障害で画像が消えることはありません。

- 毎日 06:17 JST に更新します。GitHub 側の混雑で実行時刻が遅れる場合があります。
- 手動更新は GitHub の Actions → Update profile cards → Run workflow から実行します。
- ワークフローファイルを変更したブランチへの push でも実行します。
- 3画像の生成・SVG検証がすべて成功した場合だけ、実行ブランチへコミットします。
- 失敗時は Actions のログを確認してください。保存済みの画像は前回の状態を維持します。
- 認証には GitHub が発行する `GITHUB_TOKEN` を使います。個人アクセストークンの登録は不要です。
- Action はコミットSHA、統計生成ライブラリはバージョン番号で固定しています。更新時はブランチで生成結果を確認してください。

## 生成元

- 統計・使用言語: https://github.com/stats-organization/github-readme-stats-action
- トロフィー: https://github.com/ryo-ma/github-profile-trophy

閲覧カウンターと活動グラフは既存の外部画像を継続利用しています。
Zenn は記事一覧へのリンクに変更しており、記事数バッジは表示しません。
