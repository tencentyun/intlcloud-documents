H5を使う開発者たちがTencent Cloud Gaming Multimedia Engineの製品APIのデバッグ・アクセスを手軽に実行できるように、H5での開発に向ける準備作業について説明させていただきます。

##  H5 SDKがサポートするプラットフォーム
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
      <td>Apple Safariにはまだ偶に不具合が出ていますので、製品化計画ではSafariを先に避けて、Appleが不具合を解決した後に使用してください。</td>
   </tr>
   <tr>
      <td rowspan="2">Android</td>
      <td>TBS（WeChatと携帯電話QQのデフォルトWebview）</td>
      <td>43600</td>
      <td>WeChatと携帯電話QQのビルトインデフォルトブラウザーのコアは<a href="https://x5.tencent.com/">TBS</a>です。</td>
   </tr>
   <tr>
      <td>Chrome</td>
      <td>60+</td>
      <td>H264対応必要</td>
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
      <td><a href="https://browser.qq.com/">QQブラウザー</a></td>
      <td>10.2</td>
      <td>-</td>
   </tr>
</table>

## SDK準備
SDKは、以下の手順で入手できます。
1. [ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)ページを開いてください。
2. インターフェースでH5向けのSDKリソースを見付けてください。
3. 画面で【ダウンロード】をクリックして、操作を完了してください。


## 準備作業
### 1. ポート番号の開放
所属のネットワークにファイアウォールが有る場合は、以下のポートが開放されていることを確認してください。

| プロトコル | ポート番号            |
| ---- | ----------------- |
| TCP  | 8687              |
| UDP  | 8000 、 8800 、 443 |

CDNを使ってSDKをインポートします。

### 2. WebRTCAPI.min.jsのインポート

```
html
<script src="https://sqimg.qq.com/expert_qq/webrtc/3.0/WebRTCAPI.min.js"></script>
```

###  3. H5認証の設定
#### プログラムのダウンロード
用意されている指定されたsdkappidの認証情報の署名を行うauthBufferサンプルプログラムを[ダウンロード](https://main.qcloudimg.com/raw/b1d8e4d8e7321fd67250069d07bf2016.zip)してください。

#### 対応の変更
signdemoディレクトリに入り、config.jsファイルを変更してください。config.jsファイルを開いて、デフォルトコンフィグレーションを先に削除し、コードを削除した箇所に、Tencent Cloudのバックグラウンドで申請したSDKAppidと対応の認証keyをパラメータとして、appidMap関数を呼び出します。

```
const AuthBufferConfig = function () {
    this.appidMap = {};
    this.appidMap["1400089356"] = "1cfbfd2a1a03a53e";
};
//1400089356をTencent Cloudのバックグラウンドで申請したSDKAppidに入れ替え、1cfbfd2a1a03a53eをsdkAppidに対応する認証keyに入れ替えます
```

>AuthKeyはお持ちのsdkAppidと対応する必要があります。

#### npmパッケージのインストールと実行
authBufferサンプルプログラムのディレクトリに入り、関連依存ファイルをインストールするように、以下のコマンドを実行します。

```
npm i
```

次に、スクリプトnode index.jsを実行し、署名サービスを起動します。

>async構文を使用しているため、nodeのバージョンが8以上であることを確認してください。 コマンドラインでnode -vを実行してバージョンを確認してください。


#### テスト
コマンドラインから、以下のコマンドを利用してテストを実施することができます（システムにcurl指令があることを確保しておいてください）。

```
//userSigの生成:
curl "http://127.0.0.1:10005/" --data "sdkappid=1400089356&roomid=1234123&openid=1234567"
```

#### 参考の戻り値
署名プログラムを実行すると、認証情報が返されます、参考として、戻り値は以下です。

```
{"userSig":"AqhHE7QHLFYPfV/zfyrdRYHfuUn6eOA8g/J6GMjVy//Shr5ByJPTi8hzR2KyXMvn","errorCode":0}
```
