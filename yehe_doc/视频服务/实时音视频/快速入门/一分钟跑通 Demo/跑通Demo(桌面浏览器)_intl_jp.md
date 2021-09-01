ここでは、主にTencent Cloud　TRTCデスクトップブラウザSDK Demoを素早く実行する方法をご紹介します。

## サポートするプラットフォーム

WebRTCのテクノロジーはGoogleが初めて提唱し、現在、デスクトップ版Chromeブラウザ、デスクトップ版Edgeブラウザ、デスクトップ版Firefoxブラウザ、デスクトップ版Safariブラウザ及びモバイル版Safariブラウザでは比較的万全なサポートが提供されています。その他のプラットフォーム（Androidプラットフォームブラウザなど）のサポート状況は未だ不十分です。
- お客様のユースケースが主に教育シーンである場合、教師用端末はより安定性の高い[Electron](https://intl.cloud.tencent.com/document/product/647/35097) ソリューションを使用することをお勧めします。このソリューションは、大小のデュアルチャネル画面、より柔軟性の高い画面共有ソリューション及び脆弱なネットワークに対する高い回復力をサポートしています。



<table>
<tr>
<th>OS</th>
<th width="22%">ブラウザタイプ</th><th>ブラウザの最低<br>バージョン要件</th><th width="16%">受信（再生）</th><th width="16%">送信（マイク・オン）</th><th>画面共有</th><th>SDK バージョン要件</th>
</tr><tr>
<td>Mac OS</td>
<td>デスクトップ版Safariブラウザ</td>
<td>11+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Safari13+ バージョンが必要）</td>
<td>-</td>
</tr>
<tr>
<td>Mac OS</td>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Chrome72+ バージョンが必要）</td>
<td>-</td>
</tr>
<tr>
<td>Mac OS</td>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Firefox66+ バージョンが必要）</td>
<td>v4.7.0+</td>
</tr>
<tr>
<td>Mac OS</td>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>v4.7.0+</td>
</tr>
<tr>
<td>Windows</td>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Chrome72+ バージョンが必要）</td>
<td>-</td>
</tr>
<tr>
<td>Windows</td>
<td>デスクトップ版QQブラウザ（クイックコア）</td>
<td>10.4+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>-</td>
</tr>
<tr>
<td>Windows</td>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Firefox66+ バージョンが必要）</td>
<td>v4.7.0+</td>
</tr>
<tr>
<td>Windows</td>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>v4.7.0+</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>モバイル版Safariブラウザ</td>
<td>11+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>-</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat Embedded Webページ</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>-</td>
</tr>
<tr>
<td>Android</td>
<td>モバイル版QQブラウザ</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>-</td>
</tr>
<tr>
<td>Android</td>
<td>モバイル版UCブラウザ</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>-</td>
</tr>
<tr>
<td>Android</td>
<td>WeChat Embedded Webページ（TBS コア）</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>-</td>
</tr>
<tr>
<td>Android</td>
<td>WeChat Embedded Webページ（XWEB コア）</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>-</td>
</tr>
</table>

>! 
>- ユーザーはブラウザで [WebRTC能力テスト](https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/web/demo/env-detect/index.html) ページを開き、 WebRTCを完全にサポートしているかテストすることができます。例：WeChat公式アカウントなどのブラウザ環境。
>- H.264 版の権限の制限によって、HuaweiシステムのChromeブラウザおよびChrome WebViewをコアとするブラウザでは、 TRTCデスクトップブラウザSDKの正常動作をサポートしていません。

<span id="requirements"></span>
## 環境要件
- 最新バージョンのChromeブラウザを使用してください。
- TRTCデスクトップブラウザSDKは以下のポートに依存してデータ伝送を行います。それをファイアウォールのホワイトリストに追加して設定を完了してから、 [公式サイトDemo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) にアクセス、体験して、設定が有効かを検査することができます。
 - TCPポート：8687
 - UDPポート：8000、8080、8800、843、443、16285
 - ドメイン名：qcloud.rtc.qq.com

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)および[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了していること。実名認証を行っていないユーザーは、中国国内のTRTCサービスを購入できません。

## 操作手順

[](id:step1)

### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：TestTRTC）を入力し、【作成】をクリックします。

[](id:step2)
### 手順2：SDKおよびDemoのソースコードをダウンロード
1. 実際の業務のニーズにもとづき、SDKおよびセットのDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。

[](id:step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に入り、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Web/TRTCSimpleDemo/js/debug/GenerateTestUserSig.js` ファイルを見つけて開きます。
3. `GenerateTestUserSig.js`のファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれは作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

>!
>-ここで言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：Demoの動作
Chromeブラウザを使用してDemoルートディレクトリの`index.html` ファイルを開けば、Demoを実行できます。

>!
> - 通常の場合は、体験Demoは、サーバーにデプロイし、`https://ドメイン名/xxx`経由でアクセスするか、または直接ローカルにサーバーを構築して、`localhost:ポート経由で`アクセスする必要があります。
> - 現在、デスクトップのChromeブラウザはTRTCデスクトップブラウザSDKをサポートしており、関連特性は比較的万全です。従って、Chromeブラウザを使用して体験することをお勧めします。

Demoの動作画面は図のとおりです。
- 【ルーム追加】をクリックして、オーディオビデオ通話ルームを追加し、ローカルのオーディオビデオストリームをデプロイします。
 複数ページを開き、各画面で【ルーム追加】をクリックすることができます。正常状態では、複数画面を見てリアルタイムなオーディオビデオ通話をシミュレーションできます。
- カメラアイコンをクリックすると、カメラデバイスを選択できます。
- マイクのアイコンをクリックしてマイクデバイスを選択できます。

>?WebRTCは、カメラとマイクを使用して、オーディオとビデオを収集する必要があります。体験中、Chromeブラウザから関連プロンプトが表示されることがありますが、その場合、【許可】をクリックします。


## よくあるご質問
### 1. キーをクエリーするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか。
TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。アップグレードしなくても、[旧バージョンアルゴリズム ECDSA-SHA256]（https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムに切り替えます。

アップグレード/切替の操作：
 1. [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、目的とするアプリケーションのある行の【アプリケーション情報】をクリックします。
 3．【クイックマスター】タブを選択して【ステップ2 UserSigを発行するためのキーを取得】エリアの【ここをクリックしてアップグレード】、【非対称暗号化】または【HMAC-SHA256】をクリックします。
  - アップグレード：
  - 旧バージョンアルゴリズムのECDSA-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. クライアントエラーの発生：“RtcError: no valid ice candidate found”の対処方法は。
このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、[環境要件]（#requirements）ファイアウォールのコンフィグレーションを確認してください。

### 3. クライアントエラーの発生："RtcError: ICE/DTLS Transport connection failed" または “RtcError: DTLS Transport connection timeout”の対処方法は。
このエラーが発生した場合、TRTCデスクトップブラウザSDKがメディア伝送チャネルの確立に失敗したことを意味しますので、[環境要件]（#requirements）ファイアウォールのコンフィグレーションを確認してください。

### 4.10006 errorが発生したときの対処方法は。
"「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」"が発生した場合、Tencent Real-Time Communicationアプリケーションのサーバー状態が使用可能かどうかご確認ください。
[Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/rav)にログインし、新規作成したアプリケーションをクリックし、【アカウント情報】をクリックすると、アカウント情報画面でサービス状態を確認することができます。
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)