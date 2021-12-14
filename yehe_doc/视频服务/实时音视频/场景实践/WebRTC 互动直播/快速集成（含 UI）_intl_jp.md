## まえがき
ライブストリーミングイベント用のプッシュプルストリーミングアプリケーションを探している場合、講義を行いながらPPTを共有するというニーズを満たしたい場合、さまざまな遅延度要件のライブストリーミングシーンに対応したい場合、ライブストリーミング中にオンライン視聴者とインタラクティブに交流したい場合に、Tencent Cloud高速プッシュプルストリーミングシナリオ化ソリューションがそれらのニーズの解決に役立ちます。

市場のプッシュプルストリーミングシナリオの一般的なソリューションを活用し、UIを含むプッシュプルストリーミングソリューション[TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher)と[TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer)を提供しています。TUIPusherとTUIPlayer機能のデモンストレーションについては、下図をご参照ください。また、TUIPusher & TUIPlayer機能をより迅速にご体験いただくため、ユーザー管理システムとルーム管理システムを組み合わせた[TUIPusher体験リンク](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html)および[TUIPlayer体験リンク](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html)を提供しています。
![TUIPusherデモンストレーション](https://qcloudimg.tencent-cloud.cn/raw/eb315dd6d5c2dd2dfb1e1984b7bab656.png)
![TUIPlayerデモンストレーション](https://qcloudimg.tencent-cloud.cn/raw/6490fdf7db4980db3a98b4b103fb52f1.png)


## 機能の説明
### TUIPusherプッシュコンポーネント
- マイクとスピーカーからのストリームの収集とプッシュをサポート
  - 必要に応じてビデオパラメータ（フレームレート、解像度、ビットレート）を設定
  - 美顔の起動とビデオ美顔パラメータの設定をサポート
- 画面共有ストリームの収集とプッシュをサポート
- Tencent Real-Time Communicationバックエンドへのプッシュ、Tencent Cloud CDNへのプッシュをサポート
- オンラインチャットルームをサポートし、オンライン視聴者とのインタラクティブなチャットを実現
- 視聴者リストの取得、オンライン視聴者のミュート操作の実行をサポート

### TUIPlayerプルコンポーネント
- オーディオビデオストリーミングと画面共有ストリーミングの同時再生をサポート
- オンラインチャットルームをサポートし、オンライン視聴者とのインタラクティブなチャットを実現
- 超低遅延ライブストリーミング（300msの遅延）、ライブイベントストリーミング（1000ms以下の遅延）、標準ライブストリーミング（超高速同時視聴をサポート）の3種類のプル回線をサポート


## アクセス方法
[](id:step1)
### 手順1：アカウントの準備
TUIPusher & TUIPlayerは、TRTCとInstant Messagingサービスをベースに開発されています。
1. [Tencent Cloudアカウントの登録](https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327)を行い、[Tencent Real-Time Communication（TRTC）](https://console.cloud.tencent.com/trtc)と[Instant Messaging](https://console.cloud.tencent.com/im)サービスをアクティブ化します。
2. [TRTCコンソール](https://console.cloud.tencent.com/trtc) で、**アプリケーション管理>アプリケーションの作成** をクリックし、新たなアプリケーションを作成します。
3. **アプリケーション管理>アプリケーション情報**でSDKAppID情報を取得します。
4. **アプリケーション管理>クイックマスター**でアプリケーションのsecretKey情報を取得します。

>!
>- TRTCアプリケーションを初めて作成するTencent Cloudアカウントは、10000分間のオーディオビデオリソース無料トライアルパッケージを受け取ることができます。
>- TRTCプリケーションを作成すると、同じSDKAppIDのIMアプリケーションが自動的に作成され、 [IMコンソール](https://console.cloud.tencent.com/im)でこのアプリケーションのパッケージ情報を設定することができます。

[](id:step2)
### 手順2：プロジェクトの準備
1. [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web)でTUIPusher & TUIPlayerコードをダウンロードします。
2. TUIPusher & TUIPlayerのためにインストールして依存します。
```bash
cd Web/TUIPusher
npm install

cd Web/TUIPlayer
npm install
```
3. sdkAppIdとsecretKeyを`TUIPusher/src/config/basic-info-config.js`、`TUIPlayer/src/config/basic-info-config.js`設定ファイルに入力します。
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. ローカル開発環境でTUIPusher＆TUIPlayerを実行します。
```bash
cd Web/TUIPusher
npm run serve

cd Web/TUIPlayer
npm run serve
```
5. `http://localhost:8080`と`http://localhost:8081`を開き、TUIPusherとTUIPlayer機能を体験することができます。
6. `TUIPusher/src/config/basic-info-config.js`、`TUIPlayer/src/config/basic-info-config.js`設定ファイル中のルーム，キャスターおよび視聴者などの情報を変更することができます。**TUIPusherとTUIPlayerのルーム情報、キャスター情報を一致させてください**。

>! 上記設定が完了すると、TUIPusher & TUIPlayerを使用して超低遅延ライブストリーミングを実行することができます。ライブイベントストリーミングと標準ライブストリーミングをサポートする必要がある場合は、引き続き[手順3：Relayed Live Streaming](#step3)をご参照ください。
>

[](id:step3)

### 手順3：Relayed live streaming

TUIPusher & TUIPlayerが実装するライブイベントストリーミングと標準ライブストリーミングは、Tencent CloudのCloud Streaming Services（CSS）サービスに依存するため、ライブイベントストリーミングと標準ライブストリーミング回線をサポートするには、Relayed Push機能を有効にする必要があります。

1. [**TRTCコンソール**](https://console.cloud.tencent.com/trtc) で現在使用中のアプリケーションのRelayed Push設定を有効にします。必要に応じてRelayed Push用指定ストリームまたはGlobal Auto-relayを起動することができます。
2. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)ページで独自の再生ドメイン名を追加します。具体的な内容は[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。
3. `TUIPlayer/src/config/basic-info-config.js`設定ファイルで再生ドメイン名を設定します。

上記設定が完了すると、TUIPusher & TUIPlayerがサポートする超低遅延ライブストリーミング、ライブイベントストリーミング、標準ライブストリーミングの全機能を体験できます。

[](id:step4)

### 手順4：本番環境アプリケーション
TUIPusher & TUIPlayerを本番環境アプリケーションに使用する場合は、TUIPusher & TUIPlayerにアクセスすることに加え、次の手順を実行する必要があります。
- ユーザーID、ユーザー名、ユーザープロフィール画像などを含む製品ユーザー情報を管理するためのユーザー管理システムを作成します。
- ライブストリーミングルームID、ライブストリーミングルーム名、ライブストリーミングルームのホスト情報などを含む製品のライブストリーミングルーム情報を管理するためのルーム管理システムを作成します。
- サーバーがUserSigを発行します。
> !
> - ここで使用するUserSigの発行方法は、クライアントが入力したsdkAppIdとsecretKeyに基づきuserSigを発行する方法です。この方法で発行されるsecretKeyは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この方法はローカルのTUIPusher & TUIPlayerクイックスタート機能デバッグの実行のみに適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、アプリケーションから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
- `TUIPusher/src/pusher.vue`、`TUIPlayer/src/player.vue`ファイルを参照し、ユーザー情報、ライブストリーミングルーム情報、SDKAppId、UserSigなどのアカウント情報をvuexのstoreに送信し、グローバルストレージを実行すると、プッシュプルストリーミングする2つのクライアントの全機能をクイックスタートすることができます。詳細な業務フローについては下図をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/d2cafd2e0f029908859f7498e9d92297.png)

## 注意事項
###  プラットフォームのサポート

| オペレーションシステム（OS） |ブラウザタイプ |ブラウザ最低バージョン要件 | TUIPlayer | TUIPusher | TUIPusher画面共有 |
| ------- | ------- | ------- | ------- | ------- | ------- |
| Mac OS | デスクトップ版Safariブラウザ | 11+ | サポート | サポート | サポート（Safari13+バージョンが必要）  |
| Mac OS   | デスクトップ版Chromeブラウザ | 56+ | サポート | サポート | サポート（Chrome72+バージョンが必要）  |
| Mac OS   | デスクトップ版Firefoxブラウザ | 56+ | サポート | サポート | サポート（Firefox66+バージョンが必要） |
| Mac OS   | デスクトップ版Edgeブラウザ | 80+ | サポート | サポート | サポート |
| Mac OS   | デスクトップ版WeChat Embedded Webページ | - | サポート      | サポートなし    | サポートなし |
| Mac OS   | デスクトップ版WeCom Embedded Webページ | - | サポート | サポートなし    | サポートなし |
| Windows  | デスクトップ版Chromeブラウザ | 56+ | サポート | サポート | サポート（Chrome72+バージョンが必要）  |
| Windows  | デスクトップ版QQブラウザ（クイックコア） | 10.4+ | サポート | サポート | サポートなし |
| Windows  | デスクトップ版Firefoxブラウザ | 56+ | サポート | サポート | サポート（Firefox66+バージョンが必要） |
| Windows  | デスクトップ版Edgeブラウザ | 80+ | サポート | サポート | サポート |
| Windows  | デスクトップ版WeChat Embedded Webページ | - | サポート | サポートなし | サポートなし |
| Windows  | デスクトップ版WeCom Embedded Webページ | - | サポート | サポートなし | サポートなし |

### ドメイン名要件
ユーザーのセキュリティ、プライバシーなどの問題を考慮し、ブラウザはHTTPSプロトコルでしかTUIPusher & TUIPlayerの全機能を正常に使用できないようにウェブページを制限しています。本番環境のユーザーがTUIPusher & TUIPlayerの全機能にスムーズにアクセスし体験できるようにするには、HTTPSプロトコルを使用してオーディオビデオアプリケーションページにアクセスしてください。
>! ローカル開発には、`http：// localhost`プロトコルを使用してアクセスできます。

URLドメイン名およびプロトコルのサポート状況については、以下の表をご参照ください。

| ユースケース | プロトコル | TUIPlayer | TUIPusher | TUIPusher画面共有 | 備考 |
| ------- | ------- | ------- | ------- | ------- | ------- |
| 本番環境     | HTTPSプロトコル        | サポートあり         | サポートあり         | サポートあり     | 推奨 |
| 本番環境     | HTTPプロトコル | サポート      | サポートなし    | サポートなし | - |
| ローカル開発環境 | `http://localhost` | サポート | サポート | サポート | 推奨 |
| ローカル開発環境 | `http://127.0.0.1`| サポート | サポート | サポート | - |
| ローカル開発環境 | `http://[ローカルマシンIP]` | サポート | サポートなし | サポートなし | - |

### ファイアウォールの制限
TUIPusher & TUIPlayerは次のポートに依存してデータ送信を実行しています。これらのポートをファイアウォールのホワイトリストに追加してください。
- TCPポート：8687
- UDPポート：8000、8080、8800、843、443、16285
- ドメイン名：qcloud.rtc.qq.com

## 結び
TUIPusherとTUIPlayerコンポーネントは継続的に最適化されており、将来的にはインタラクティブなマイク接続や弾幕などの機能が搭載される予定です。 お客さまのサポートとフィードバックが弊社の継続的な改善の原動力となります。ご要望やご質問がある場合は、適宜、フィードバックしてください。
