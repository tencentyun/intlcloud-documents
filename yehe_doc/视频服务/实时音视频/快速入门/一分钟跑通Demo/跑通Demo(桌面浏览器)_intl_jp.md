ここでは、主にTencent Cloud　TRTCデスクトップブラウザSDK Demoを速く動作させる方法を紹介します。

## サポートするプラットフォーム

WebRTCのテクノロジーはGoogleが初めて提唱し、現在、デスクトップ版Chromeブラウザ、デスクトップ版Safariブラウザ及びモバイル版Safariブラウザでは比較的万全なサポートが提供されています。その他のプラットフォーム（Androidプラットフォームブラウザなど）のサポート状況は未だ不十分です。

- お客様のユースケースが主に教育シーンである場合、教師用端末はより安定性の高い[Electron](https://intl.cloud.tencent.com/document/product/647/35097) ソリューションを使用することをお勧めします。このソリューションは、大小のデュアルチャネル画面、より柔軟性の高い画面共有ソリューション及び脆弱なネットワークに対する高い回復力をサポートしています。

| OS |ブラウザタイプ | ブラウザ最低バージョン要件 | 受信（再生）| 発送（マイク・オン）| 画面共有 |
|:-------:|:-------:|:-------:|:-------:|:-------:| :-------:|
| Mac OS  | デスクトップ版Safariブラウザ |  11+ | サポート | サポート | サポートなし|
| Mac OS  | デスクトップ版 Chrome ブラウザ |  56+ | サポート | サポート | サポート（Chrome72+ バージョンが必要） |
| Windows  | デスクトップ版 Chrome ブラウザ|  56+ | サポート | サポート | サポート（Chrome72+ バージョンが必要） |
| Windows  | デスクトップ版 QQ ブラウザ |  10.4 | サポート | サポート | サポートなし |
| iOS | モバイル版 Safari ブラウザ | 11.1.2 | サポート | サポート | サポートなし |
| iOS | WeChatビルトイン型ウェブページ| 12.1.4 | サポート | サポートなし | サポートなし |
| Android | モバイル版 QQ ブラウザ| - | サポートなし | サポートなし | サポートなし |
| Android | モバイル版 UC ブラウザ| - | サポートなし | サポートなし | サポートなし |
| Android | WeChatビルトイン型ウェブページ| - | サポートなし| サポートなし | サポートなし |

>! 
>- ユーザーはブラウザで [WebRTC 能力テスト](https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/web/demo/env-detect/index.html) ページを開き、 WebRTCを完全にサポートしているかテストすることができます。例：WeChat公式アカウントなどのブラウザ環境。
>- H.264 版の権限の制限によって、Huaweiシステムの Chrome ブラウザおよび Chrome WebView をコアとするブラウザでは、 TRTC デスクトップ型ブラウザ SDK の正常動作をサポートしていません。

<span id="requirements"></span>
## 環境要件
- 最新バージョンの Chrome ブラウザをご使用ください。
- TRTC デスクトップ型ブラウザ SDK は以下のポートに依存してデータ伝送を行います。それをファイアウォールのホワイトリストに追加して設定を完了してから、 [公式サイト Demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) にアクセス、体験して、設定が有効かを検査することができます。
 - TCP ポート：8687
 - UDP ポート：8000，8080，8800，843，443，16285
 - ドメイン名：qcloud.rtc.qq.com

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了済みです。

## 操作手順
<span id="step1"></span>
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestTRTC`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

<span id="step2"></span>
### 手順2：SDKおよびDemoのソースコードをダウンロード
1. マウスを該当するカードに移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Web)】をクリックして Github（または【[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/H5_latest.zip?_ga=1.195966252.185644906.1567570704)】をクリック）にジャンプし，関連するSDK および付属の Demo ソースコードをダウンロードします。
 ![](https://main.qcloudimg.com/raw/70f4f26e438e63b62b1dd55306d1c296.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

<span id="step3"></span>
### 手順3：Demoプロジェクトファイルの設定
1．[手順2]（#step2）でダウンロードしたソースコードパッケージを解凍します。
2. `Web/js/debug/GenerateTestUserSig.js`ファイルを探して開きます。
3. `GenerateTestUserSig.js`ファイルの関連パラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
	<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

>!本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：Demoの動作
Chromeブラウザを使用してDemoルートディレクトリの`index.html`ファイルを開けば、すぐにDemoを動作できます。

>!
> - 通常、Demoを体験する場合、サーバーにデプロイして `https://ドメイン名/xxx` 経由でアクセスするか、またはサーバーをローカルに直接構築して、`localhost:ポート`経由でアクセスする必要があります。
> - 現在、デスクトップのChromeブラウザはTRTCデスクトップブラウザSDKをサポートしており、関連特性は比較的万全です。従って、Chromeブラウザを使用して体験することをお勧めします。



- 【ルーム追加】をクリックして、オーディオビデオ通信ルームを追加しローカルオーディオビデオストリームをデプロイします。
 複数ページを開き、各画面で【ルーム追加】をクリックすることができます。正常状態では、複数画面を見てTencent Real-Time Communicationをシミュレーションできます。
- カメラアイコンをクリックすると、カメラデバイスを選択できます。
- マイクアイコンをクリックすると、マイクデバイスを選択できます。

>?WebRTC は、カメラとマイクを使用して、オーディオとビデオを収集する必要があります。体験中、Chromeブラウザから関連プロンプトが表示されることがありますが、その場合、【許可】をクリックします。


## よくあるご質問

### 1. キーをクエリするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか？
TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。アップグレードしなくても、[旧バージョンアルゴリズム ECDSA-SHA256]（https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムに切り替えます。

アップグレード/切替の操作：
 1. [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、目的とするアプリケーションのある行の【アプリケーション情報】をクリックします。
 3．【すぐに作業を開始】タブを選択して【ステップ2 UserSigを発行するためのキーを取得】エリアの【このアップグレードをクリック】、【非対称暗号化】または【HMAC-SHA256】をクリックします。





### 2. クライアントエラーの発生：“RtcError: no valid ice candidate found”の対処方法は？
このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、[環境要件]（#requirements）ファイアウォールのコンフィグレーションを確認してください。

### 3. クライアントエラーの発生："RtcError: ICE/DTLS Transport connection failed" または “RtcError: DTLS Transport connection timeout”の対処方法は？
このエラーが発生した場合、TRTCデスクトップブラウザSDKがメディア伝送チャネルの確立に失敗したことを意味しますので、[環境要件]（#requirements）ファイアウォールのコンフィグレーションを確認してください。

### 4. 10006 errorが発生したときの対処方法は？
 "「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」"が発生した場合、Tencent Real-Time Communicationアプリケーションのサーバー状態が使用可能かどうかご確認ください。
 [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/rav)にログインし、新規作成したアプリケーションをクリックし、【アカウント情報】をクリックすると、アカウント情報画面でサービス状態を確認することができます。
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)
