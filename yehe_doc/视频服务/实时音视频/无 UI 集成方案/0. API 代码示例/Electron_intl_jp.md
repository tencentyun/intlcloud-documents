ここでは、主にTencent CloudのTRTC-API-Example（Electron）を素早く実行する方法をご紹介します。

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行っていることが必要です。

## 操作手順
[](id:step1)
### ステップ1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援** > [**Demoクイックスタート**](https://console.cloud.tencent.com/trtc/quickstart)を選択します。
2. **アプリケーションの作成**をクリックし、`TestTRTC`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合、**既存のアプリケーションを選択**をクリックします。
3. 実際の業務ニーズに応じてタグを追加または編集し、**作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)
>?
>-アプリケーション名には、数字、中国語と英語の文字、アンダーラインのみを含めることができ、15文字以内とします。
タグはTencent Cloudのさまざまなリソースを識別して管理するために使用されます。たとえば、企業に複数の事業部門があり、各部門に1つ以上のTRTCアプリケーションがある場合、企業はTRTCアプリケーションにタグを追加することで部門情報にマークを付けることができます。タグは入力必須ではありません。実際のビジネスニーズに応じてタグを追加または編集できます。

[](id:step2)
### ステップ2：SDKおよびTRTC-API-Exampleソースコードのダウンロード

1. TRTC-API-Exampleのソースコードです。
```shell script
git clone https://github.com/tencentyun/TRTCSDK
cd Electron/TRTC-API-Example
```

[](id:step3)
### ステップ3：TRTC-API-Exampleプロジェクトファイルの設定

1. `Electron/TRTC-API-Example/assets/debug/gen-test-user-sig.js`ファイルを見つけて開きます。
3. `gen-test-user-sig.js` ファイルの関連パラメータを設定します。
	<ul><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
	<li/>SECRETKEY：デフォルトは '' です。実際のキー情報を設定してください。</ul>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png">

>!
>- ここで言及したUserSigの発行方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのTRTC-API-Exampleクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### ステップ4：コンパイル実行

```shell
npm install
cd src/app/render/main-page
npm install

cd ../../..
npm run start
```

## よくあるご質問
### 1. キーを照会するとき、公開鍵および秘密鍵の情報しか取得できませんが、キーはどうしたら取得できますか。
TRTC SDK 6.6バージョン（2019年08月）では、新しい署名アルゴリズムのHMAC-SHA256の使用を開始しました。それ以前に作成されたアプリケーションの場合、新しい暗号化鍵を取得するために、署名アルゴリズムをアップグレードする必要があります。アップグレードしない場合でも、[旧バージョンアルゴリズム ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムを切り替えます。

アップグレード/切替の操作：
 1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで**アプリケーション管理**を選択し、ターゲットアプリケーションのある行の**アプリケーション情報**をクリックします。
 3. **クイックマスター**タブを選択して**ステップ2 UserSigを発行するためのキーを取得**エリアの**ここをクリックしてアップグレード**、**非対称暗号化**または**HMAC-SHA256**をクリックします。
  - アップグレード：

  - 旧バージョンアルゴリズムのECDSA-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/a8737123c1e3cc0f7eb34901ed2629f7.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/701fcde1a562bf9fbbb0d426948e311e.png)

### 2. ファイアウォールにはどのような制限がありますか。
SDKがUDPプロトコルを使用してオーディオビデオ伝送を行っているため、UDPをブロックするオフィスネットワークでは使用できません。類似した問題がおありの際は、 [企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照の上、問題原因を調べ解決してください。
