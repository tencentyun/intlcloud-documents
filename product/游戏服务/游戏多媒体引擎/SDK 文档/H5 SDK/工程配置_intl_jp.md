H5開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでH5開発のための準備作業を紹介します。

## H5 SDKがサポートするプラットフォーム
<table>
   <tr>
      <td>OSプラットフォーム</td>
      <td>ブラウザ/webview</td>
      <td>バージョン要件</td>
      <td>備考</td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>Safari</td>
      <td>11.1.2</td>
      <td>Apple Safariは偶然起きたバグがあるため、とりあえず製品化計画を止めて、Apple社はそれを解決した後に使用するようにお勧めします。</td>
   </tr>
   <tr>
      <td rowspan="2">Android</td>
      <td>TBS（WeChatとモバイルQQのデフォルトWebview）</td>
      <td>43600</td>
      <td>WeChatとモバイルQQのデフォルトの内蔵ブラウザカーネルは<a href="https://x5.tencent.com/">TBS</a></td>です
   </tr>
   <tr>
      <td>Chrome</td>
      <td>60+</td>
      <td>H264対応が必須</td>
   </tr>
   <tr>
      <td rowspan="2">Mac</td>
      <td>Chrome</td>
      <td>47+</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Safari</td>
      <td>11+</td>
      <td>-</td>
   </tr>
   <tr>
      <td rowspan="2">Windows(PC)</td>
      <td>Chrome</td>
      <td>52+</td>
      <td>-</td>
   </tr>
   <tr>
      <td><a href="https://browser.qq.com/">QQブラウザ</a></td>
      <td>10.2</td>
      <td>-</td>
   </tr>
</table>

## SDKの準備
SDKは以下の方法で入手できます。
1. [ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)を参照して関連のSample CodeとSDKをダウンロードしてください。
2. インターフェースでH5バージョンのSDKリソースを検索します。
3. ページで[ダウンロード]をクリックして操作を完了します。


## 準備作業
### 1. ポート番号の開放
ネットワークにファイアウォールがあれば、次のポートの開放を確認してください。

| プロトコル | ポート番号            |
| ---- | ----------------- |
| TCP  | 8687              |
| UDP  | 8000、8800、443 |

CDNでSDKを取り込みます。

### 2. WebRTCAPI.min.jsの取り込み

```
html
<script src="https://sqimg.qq.com/expert_qq/webrtc/3.0/WebRTCAPI.min.js"></script>
```

### 3. H5認証の設定
#### プログラムのダウンロード
弊社が用意した用意されたauthBufferサンプルプログラムを[ダウンロード](https://main.qcloudimg.com/raw/b1d8e4d8e7321fd67250069d07bf2016.zip)してください。このプログラムによって指定したsdkappidの認証情報の署名をつけることができます。

#### 適切な変更
signdemoディレクトリに移動し、config.jsファイルを変更します。config.jsファイルを開き、まずデフォルト構成を削除し、コードが削除された箇所にappidMap関数を呼び出します。パラメータはTencent Cloudコンソールで申請したSDKAppidおよび対応する認証keyです。

```
const AuthBufferConfig = function () {
    this.appidMap = {};
    this.appidMap["1400089356"] = "1cfbfd2a1a03a53e";
};
//1400089356をTencent Cloudコンソールで申請したsdkAppidに、1cfbfd2a1a03a53eを対応するsdkAppidの認証keyに置き換えます。
```

>!AuthKeyはsdkAppidに対応する必要があります

#### npmパッケージをインストールして実行
authBufferサンプルプログラムディレクトリに移動し、以下の文を実行して関連依存をインストールします。

```
npm i
```

そしてスクリプトnode index.jsを実行し、署名サービスを開始します。

>!async構文を使用するため、Ver.8以降のnodeバージョンを確保してください。コマンドラインからnode -vを実行してバージョンを表示します。


#### テスト
コマンドラインから以下のコマンドでテストできます（システム内にcurlコマンドが含まれることを確認）。

```
//生成されたuserSig：
curl "http://127.0.0.1:10005/" --data "sdkappid=1400089356&roomid=1234123&openid=1234567"
```

#### 戻り参照

```
{"userSig":"AqhHE7QHLFYPfV/zfyrdRYHfuUn6eOA8g/J6GMjVy//Shr5ByJPTi8hzR2KyXMvn","errorCode":0}
```
