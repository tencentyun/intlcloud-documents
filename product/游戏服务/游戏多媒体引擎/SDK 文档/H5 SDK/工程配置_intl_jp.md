## 概要
Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。H5開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここではH5開発のための準備作業を紹介します。

## GME H5 SDKがサポートするプラットフォーム
| OSプラットフォーム  | プラウザ/webview  | バージョン要件  |  備考|
| ------------------------- | -------- | ---------------------- |------- |
| iOS          | Safari （Safariのみサポートする） | 11.1.2 | Apple Safariは偶然起きたbugがあるため、とりあえず製品化計画を止めて、Apple社はそれを解決した後に使用するようにお勧めます|
| Android      | TBS （WeChatとモバイルQQのデフォルトWebview） | 43600                | WeChatとモバイルQQのデフォルトで内蔵されたプラウザカーネルはTBSです。[TBS概要](http://x5.tencent.com/) |
| Android      | Chrome | 60+               | H264対応必要  |
| Mac          | Chrome | 47+                |      |
| Mac          | Safari | 11+                |      |
| Windows(PC)  | Chrome | 52+                |      |
| Windows(PC)  | [QQプラウザ](https://browser.qq.com/) | 10.2 | &nbsp;     |


## SDKの準備
SDKは以下の方法で入手できます。

### 1. [ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連のSample CodeとSDKをダウンロードしてください。


### 2. 画面でH5バージョンのSDKリソースを見つけます。


### 3. 【ダウンロード】ボタンを押します。


## 準備作業

### 1. ポート番号を開放します

ネットワークにファイアウォールがあれば、次のポートの開放を確認してください。

| プロトコル | ポート番号            |
| ---- | ----------------- |
| TCP  | 8687              |
| UDP  | 8000、8800、443 |

CDNでSDKを取り込みます。
### 2. ページでWebRTCAPI.min.jsを取り込みます

```html
<script src="https://sqimg.qq.com/expert_qq/webrtc/3.0/WebRTCAPI.min.js"></script>
```

### 3. H5認証の設定を行います


## 認証設定

### 署名ステップ
GMEを使用するには、認証情報に署名する必要があります。認証の手順は以下の通りです。

### プログラムのダウンロード
このリンクをクリックすると、弊社が用意したauthBufferサンプルプログラムをダウンロードできます。このプログラムによって指定したsdkappidの認証情報の署名をつけることができます。

### 適切な変更
signdemoディレクトリに移動し、config.jsファイルを変更します。config.jsファイルを開き、まずデフォルト構成を削除し、コードが削除された箇所にappidMap関数を呼び出します。パラメータはTencent Cloudバックグラウンドで申請したSDKAppidおよび対応する認証keyです。

```
const AuthBufferConfig = function () {
    this.appidMap = {};
    this.appidMap["1400089356"] = "1cfbfd2a1a03a53e";
};
//1400089356をTencent Cloudバックグラウンドで申請したsdkAppidに、1cfbfd2a1a03a53eを対応するsdkAppidの認証keyに置き換えます。
```

>!  AuthKeyはsdkAppidに対応する必要があります

### npmパッケージをインストールして実行
authBufferサンプルプログラムディレクトリに移動し、以下の文を実行して関連依存をインストールします。
```
npm i
```
そしてスクリプトnode index.jsを実行し、署名サービスを開始します。

>!  async構文を使用するため、Ver.8以降のnodeバージョンを確保してください。コマンドラインからnode -vを実行してバージョンを表示します。


### テスト
コマンドラインから以下のコマンドでテストできます（システム内にcurlコマンドが含まれることを確認）。
```
//生成されたuserSig：
curl "http://127.0.0.1:10005/" --data "sdkappid=1400089356&roomid=1234123&openid=1234567
（検証より生成されたuserSigは同様にWebサイトにアクセスできますが、検証するには検証対応のSDKappIDも必要があります。デフォルトで1400089356に対応）
```

戻り参照：

```
{"userSig":"AqhHE7QHLFYPfV/zfyrdRYHfuUn6eOA8g/J6GMjVy//Shr5ByJPTi8hzR2KyXMvn","errorCode":0}
```

