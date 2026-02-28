# tweetXer 日本語版 – ツイートを一括削除

[このスクリプト](https://raw.githubusercontent.com/yupika/tweetXer/refs/heads/main/tweetXer.js)を使って、すべてのツイートを削除できます。プロフィールに表示されていないツイートも削除可能です。ただし、データエクスポートが必要です。
削除を自動化するため、アカウントがBANされる可能性があります。それも悪くない結末かもしれません。

> **オリジナル**: [lucahammer/tweetXer](https://github.com/lucahammer/tweetXer)
>
> この日本語版では、UIの完全日本語化に加え、以下の改良を含んでいます:
> - レジューム機能（中断しても続きから再開可能）
> - 429レート制限エラーの適切な処理
> - エラーハンドリングの修正（スクリプトが停止する問題の解消）
> - スキップカウンター（削除済みツイートの自動スキップ＆カウント）

## 使い方

0. Xのデータエクスポートを[リクエスト](https://x.com/settings/your_twitter_data/data)します（数日かかります）。届いたらダウンロードして解凍してください
1. Twitterアカウントにログイン
2. ブラウザの開発者コンソールを開く（F12 または cmd+option+i）
3. [スクリプト全文](https://raw.githubusercontent.com/yupika/tweetXer/main/tweetXer.js)をコンソールに貼り付けてEnter
4. 画面上部に水色のバーが表示されます
5. ファイル選択で tweet-headers.js または tweets.js を選択
6. すべてのツイートが削除されるまで待ちます（毎秒5〜10件程度）

途中で中断された場合、**自動的にレジューム機能が働きます**。次回スクリプトを実行すると「前回の進捗が見つかりました」というバナーが表示され、「続きから再開」または「破棄して最初から」を選べます。

## コピペの代わりに: ユーザースクリプト

スクリプトをコピペする代わりに、ユーザースクリプトとしてインストールできます: [greasyfork.org/en/scripts/476062-tweetxer](https://greasyfork.org/en/scripts/476062-tweetxer)（[Violentmonkey](https://addons.mozilla.org/firefox/addon/violentmonkey/)、[FireMonkey](https://addons.mozilla.org/firefox/addon/firemonkey/)、[Tampermonkey](https://addons.mozilla.org/firefox/addon/tampermonkey/) などのブラウザ拡張で動作）

スマートフォンでも使えます。

### Android

1. [Firefox Mobile](https://www.mozilla.org/firefox/browsers/mobile/) をインストール
2. [Tampermonkey アドオン](https://addons.mozilla.org/firefox/addon/tampermonkey/) をインストール
3. [Greasyfork からスクリプト](https://greasyfork.org/en/scripts/476062-tweetxer) をインストール
4. X.com を開くと水色のバーが表示されます。Xアプリを先にアンインストールする必要があるかもしれません

### iOS (iPhone/iPad)

1. Safari拡張 [Userscripts](https://apps.apple.com/app/userscripts/id1463298887) をインストール
2. SafariでUserscriptsを有効化
3. TweetXerユーザースクリプトを追加: New remote https://update.greasyfork.org/scripts/476062/TweetXer.user.js
4. X.com にアクセス
5. Userscripts拡張にX.comへのアクセスを許可

## 仕組み

信頼できないソースからこのようなスクリプトを使わないでください。このスクリプトは、ブラウザからTwitterへのリクエストを傍受し、ツイートIDをあなたの tweets.js ファイルのIDに置き換えます。これにより古いツイートにアクセスして削除できます。

## おまけ: ブックマークのエクスポート

ブックマークはTwitterデータエクスポートに含まれないため、「詳細オプション」にエクスポートボタンがあります。

## おまけ: データエクスポートなしでツイート削除

何らかの理由でデータエクスポートが使えない場合や、一部のツイートが漏れている場合は、「詳細オプション」の低速モードを使えます。プロフィール上のツイートを読み込んでから削除するため、非常に遅いです。

## おまけ: DM（ダイレクトメッセージ）の削除

DMを削除するには、tweet-headers.js の代わりに direct-message-header.js を選択します。完了したらページをリロードし、再度スクリプトを実行して direct-message-group-headers.js を選択すると、グループメッセージも削除できます。

[元エンジニアによると](https://bsky.app/profile/triketora.com/post/3lcbmqzo4uk25)、全員がDMを削除すればサーバーからも消えるそうです。

## おまけ: 全員フォロー解除

「詳細オプション」から自動的に全員のフォローを解除できます。レート制限のため、時間を空けて複数回実行する必要があるかもしれません。

## よくある問題と解決策

- **スクリプトが貼り付けられない**

  ブラウザがランダムなスクリプトの貼り付けからあなたを保護しています。「allow pasting」と入力してEnterを押し、理解した上で操作していることを確認してください。

- **Xがデータエクスポートを送ってくれない**

  [プライバシーフォーム](https://help.x.com/en/forms/privacy/request-account-info/me)からリクエストしてみてください。

- **すべてのツイートが削除されなかった**

  残っているツイートのIDがデータエクスポートに含まれているか確認してください。スクリプトはファイルに含まれるもののみ削除できます。「詳細オプション」に残りのツイートを自動削除する機能がありますが、非常に遅いです。ツイートが多い場合は再実行するか、新しいエクスポートをリクエストしてください。

- **プロフィールにツイートが表示されないのに、ツイート数が残っている**

  ほとんどの場合、凍結やBANされたアカウントのリツイートです。アカウントが復活すると再表示されることもありますが、されないこともあります。対処法はありません。

- **いいねが削除されない**

  直近の数百件のみ削除可能です。手動でも同様です。アカウント全体を削除する以外に方法はありません。

- **ブラウザがクラッシュする**

  ChromeやChromium系ブラウザで起きやすいです。特に15,000件以上のツイートを削除する場合。実行中にコンソールを閉じるとクラッシュが減ることがあります。

- **うまくいった！感謝したい**

  素晴らしい！オリジナル作者をサポート: [buymeacoffee.com/lucahammer](https://www.buymeacoffee.com/lucahammer)
