ライブイベントブロードキャスト(LEB)は、超低遅延の再生シナリオでの標準ライブブロードキャストの拡張です。従来のライブブロードキャストプロトコルよりも低遅延で、視聴者にミリ秒レベルの最高**ライブブロードキャストの視聴**体験を提供します。
ライブイベントブロードキャストサービスをご利用になる前に、[ライブイベントブロードキャストのサービス料金](https://intl.cloud.tencent.com/document/product/267/39969)をご覧いただき、誤解を避けるために、課金項目と価格を確認することをお勧めします。

> ! ライブイベントブロードキャストはWebRTCプロトコルの低遅延特性を使用しているため、デフォルトではBフレームをサポートせず、かつオーディオコーデックはopusコーデックとしています。ライブイベントブロードキャストストリーミング再生が可能なことを保証するため、プッシュ時にBフレームがある場合またはオーディオコーデックがopusでない場合は、CSSバックグラウンドが自動的にトランスコーディングを開始してBフレームを削除し、opusエンコードに変換します。これにより[標準トランスコード料金](https://intl.cloud.tencent.com/document/product/267/39604)が発生します。

[](id:app)
## Appへのアクセス
### アクセスの説明
iOS、Androidのアプリの場合、MLVB SDKを統合することで、App端末でのライブブロードキャストプッシュ/再生機能を実装できます。

- **App端末でのライブブロードキャストプッシュ**：カメラ画面のキャプチャまたはスマホ画面のキャプチャをサポートし、RTMPプロトコルによって迅速にCSSサービスにプッシュ可能です。詳細は、[カメラプッシュ](https://intl.cloud.tencent.com/document/product/1071/38157)および[スクリーンキャプチャプッシュ](https://intl.cloud.tencent.com/document/product/1071/41878)をご参照ください。
- **App端末でのライブブロードキャスト再生**：WebRTC再生プロトコルをサポートし、ライブイベントブロードキャストサービスと組み合わせて低遅延ライブブロードキャスト体験を素早く構築します。詳細については、[ライブイベントブロードキャストプル](https://intl.cloud.tencent.com/document/product/1071/41875)をご参照ください。

>? MLVB SDKはCSS、IM、TRTCなどのサービスの力を借りることで、多人数オーディオとビデオの低遅延な相互接続と相互通信を実現します。多人数マイク接続によるインタラクティブな効果を実現し、マイク接続に参加しない視聴者もライブブロードキャストサービスを介して視聴できます。詳細については、[ライブブロードキャストマイク接続インタラクション](https://intl.cloud.tencent.com/document/product/1071/42210)をご参照ください。

### Demo体験
ビデオクラウドツールキットとは、Tencent Cloudがオープンソース化したオーディオとビデオサービスの完全なソリューションです。ビデオクラウドツールキットを使用すれば、ライブイベントブロードキャストのミリ秒レベルの低遅延プル機能を体験できます。
<table>
  <tr>
    <th><div align="center">開発端末</div></th>
    <th><div align="center">体験版インストール</div></th>
    <th><div align="center">プッシュデモ（Android）</div></th>
    <th><div align="center">再生デモ（Android）</div></th>
  </tr>
  <tr>
    <td >Android</td>
    <td style="text-align:center"><img width="150" src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png"> </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200" src="https://main.qcloudimg.com/raw/dca4b24bc363d25c9ea45e60859a2f6d.png"/>
      </div>
    </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200"  src="https://main.qcloudimg.com/raw/6dd7c02dc2381d84225c2f2f286e7358.png"/>
      </div>
    </td>
  </tr>
  <tr>
      <td >iOS</td>
    <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150"></td>
  </tr>
</table>




[](id:web)
## Webへのアクセス
### アクセスの説明
ウェブサイトでライブブロードキャストプッシュと再生を行う必要がある場合は、次の方式によるアクセスを推奨します：

- **Web端末でのライブブロードキャストプッシュ**：ブラウザの一般的なWebRTC規格をベースに設計とカプセル化を行い、コードセグメントを導入することで、ブラウザでのライブブロードキャストプッシュを実現できます。詳細については、[WebRTCプッシュ](https://intl.cloud.tencent.com/document/product/267/41620)をご参照ください。
> ! 
> - WebRTCプッシュの時、オーディオコーデックはopusによるコーデックとなります。標準ライブブロードキャストの再生プロトコル（RTMP、FLV、HLS）を使用して再生を行う場合は、正常な視聴を確保するために、CSSバックグラウンドはオーディオトランスコードを自動的に開始してaacエンコードに変換し、これによりオーディオトランスコード料金が発生します。詳細については、[オーディオトランスコード料金の説明](https://intl.cloud.tencent.com/document/product/267/39604#a_trans)をご参照ください。（ライブイベントブロードキャストのみをご使用の場合、オーディオトランスコードは開始されません）
> - WebRTCプロトコルプッシュを使用して、各プッシュドメイン名は、デフォルトで**100パス並列処理**プッシュ数に制限されています。このプッシュ制限を超える必要がある場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してお申し出ください。


### Demo体験

- **Web端末ライブブロードキャストプッシュ**：**CSSコンソール**>[Webプッシュツール](https://console.cloud.tencent.com/live/tools/webpush)により、Web端末プッシュ機能をテストします。

- **Web端末ライブブロードキャストプル**：[WebRTC Live Demo](https://tcplayer.vcube.tencent.com/webrtc-demo/index.html)ツールにより、再生体験を行います。
>?
>- Web端末ライブブロードキャストプッシュとプルはいずれも標準WebRTCプロトコルを使用します。Web端末プッシュ時はBフレームを含まず、またオーディオコーデックはOPUSオーディオ形式のため、オーディオトランスコードおよびBフレームトランスコード料金は発生しません。
>- WebRTC Live Demoは複数の解像度機能をサポートします。CSSコンソールの**機能設定** >[**ライブブロードキャストトランスコード**](https://console.cloud.tencent.com/live/config/transcode)で高精細度-HD、標準-SDのトランスコードテンプレートを設定でき、トランスコードテンプレートを有するWebRTCストリーミングアドレスをDemo中の対応するカテゴリに入力した後、再生をテストします（この機能のテストが不要な場合は、DemoにWebRTCオリジナルストリーミングを1つ入力します）。
>- ライブブロードキャストトランスコードの操作ガイドとトランスコード料金の内容については、ドキュメント[ライブブロードキャストトランスコード](https://intl.cloud.tencent.com/document/product/267/31071)をご参照ください。

[](id:obs)
## OBS WebRTCプロトコルプッシュへのアクセス
WebRTCプロトコルプッシュは、主にビデオクラウドのライブイベントブロードキャスト（超低遅延ライブブロードキャスト）のプッシュに使用され、キャプチャされたオーディオとビデオ画面またはビデオファイルを、WebRTCプロトコルを介してライブブロードキャストサーバーにプッシュする役割を担います。下記の内容では主に、OBSツールを使用してWebRTCプロトコルプッシュ機能を実現する方法について説明します。

### 注意事項
- 現在、OBSバージョンは、26以降のバージョンが必要です。
- WebRTCプロトコルプッシュは現在、Windows端末のみを備えるOBSプラグインに対応します。MacにWebRTCプッシュを実装する場合は、[Webアクセス](https://intl.cloud.tencent.com/document/product/267/42131)を使用できます。

[](id:set)
### OBSプラグインの設定
1. **プラグインデータを設定します**。
[OBSプラグイン](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20210628.zip)をダウンロードし、dataファイルの中の2つの`services.json`および`package.json`ファイルを、対応する**obs-studio** > **rtmp-service** > **data**ディレクトリに移動して上書きします。（`obs-studio`はデフォルトではCドライブにインストールされており、対応するディレクトリは`C:\Program Files\obs-studio\data\obs-plugins\rtmp-services`です。実際の状況に応じて設定してください。）
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
2. **プラグインダイナミックライブラリを設定します**。
`obs-plugins\64bit`のdllおよびpdbファイルを、対応する**obs-studio** > **obs-plugins** > **64bit**ディレクトリに移動します。（`obs-studio`はデフォルトではCドライブにインストールされており、対応するディレクトリは`C:\Program Files\obs-studio\obs-plugins\64bit`です。実際の状況に応じて設定してください。）
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
## プッシュリンクの設定
[](id:push)
1. **WebRTCプッシュアドレスを発行します**。
  1. Tencent Cloudライブブロードキャストコンソールにログインし、**ライブブロードキャストツールボックス**>**[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**でプッシュアドレスを発行します。具体的な操作については、[アドレスジェネレーター](https://intl.cloud.tencent.com/document/product/267/31084)をご参照ください。
  2. 発行したアドレスのプレフィックス`rtmp`を`webrtc`に変更します。具体的な使用説明については、[ライブブロードキャストURLの自己結合](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。

    ![](https://qcloudimg.tencent-cloud.cn/raw/e4e8118922b8f4be309e33f740152006.png)    
2. **OBSプッシュサービスを設定します**。[](id:set_obs)
  1. OBSを開いて、1番下のツールバーの**コントロール**>**設定**ボタンから設定画面に入ることができます。
  2. **プッシュ**をクリックしてストリーミング設定タブに入り、サービスタイプは`Tenent webrtc`、サーバーは`Default`を選択し、ストリーミングキーに上記で発行した[WebRTCプッシュアドレス](#push)を入力し、その後で`&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream`を結合します。

**ストリーミングキーの例：**

```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx &stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```
下図のとおり：
![](https://qcloudimg.tencent-cloud.cn/raw/8035e95d3f62e62dcb3c33db2e5560d6.png)     

[](id:play)
### ライブイベントブロードキャストのプル再生
ライブイベントブロードキャストSDKを統合してプル再生を行います。詳細については、[ライブイベントブロードキャストプル](https://intl.cloud.tencent.com/document/product/1071/41875)をご参照ください。
