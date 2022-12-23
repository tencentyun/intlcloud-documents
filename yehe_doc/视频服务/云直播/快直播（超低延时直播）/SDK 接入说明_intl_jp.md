ライブイベントブロードキャスト(LEB)は、超低遅延の再生シナリオでの標準ライブブロードキャストの拡張です。従来のライブブロードキャストプロトコルよりも低遅延で、視聴者にミリ秒レベルの最高**ライブブロードキャストの視聴**体験を提供します。
ライブイベントストリーミングサービスをご利用になる前に、[ライブイベントストリーミングのサービス料金](https://intl.cloud.tencent.com/document/product/267/39969)をご覧いただき、誤解を避けるために、課金項目と価格を確認しておくことをお勧めします。

>! ライブイベントストリーミングはWebRTCプロトコルの低遅延特性を使用しているため、デフォルトではBフレームをサポートせず、かつオーディオコーデックはopusコーデックとしています。ライブイベントストリーミングのストリーム再生が可能なことを保証するため、プッシュ時に、Bフレームがある場合またはオーディオコーデックがopusでない場合は、CSSバックエンドが自動的にトランスコーディングを開始してBフレームを削除し、opusエンコードに変換します。これにより[標準トランスコード料金](https://intl.cloud.tencent.com/document/product/267/39604)が発生します。

[](id:app)
## APP導入
### 導入の説明
iOS、Androidのアプリの場合、ライブブロードキャストSDKを統合することで、App端末でのCSSプッシュ/再生機能を実装できます。

- **App端末のCSSプッシュ**：カメラ画面のキャプチャまたはスマホ画面のキャプチャをサポートし、RTMPプロトコルによって迅速にCSSサービス上にプッシュ可能です。詳細については、[カメラプッシュ](https://www.tencentcloud.com/document/product/1071/38157) および[スクリーンキャプチャプッシュ](https://www.tencentcloud.com/document/product/1071/41878)をご参照ください。
- **App端末CSS再生**：WebRTC再生プロトコルをサポートし、ライブイベントストリーミングサービスと組み合わせて低遅延ライブストリーミング体験を素早く構築します。詳細については、[ライブイベントストリーミングプル](https://www.tencentcloud.com/document/product/1071/41875)をご参照ください。

>? ライブブロードキャストSDKはCSS、IM、TRTCなどのサービスの力を借りることで、多人数オーディオビデオの低遅延な相互接続・相互通信を実現することが可能です。多人数コラボ配信によるインタラクティブな効果を実現し、コラボ配信に参加しない視聴者もCSSのサービスを介して視聴することができます。詳細については、[CSSコラボ配信インタラクション](https://www.tencentcloud.com/document/product/1071/42210)をご参照ください。

### Demo体験
ビデオクラウドツールキットは、Tencent Cloudがオープンソース化したオーディオとビデオサービスの完全なソリューションです。ビデオクラウドツールキットを使用すれば、ライブイベントブロードキャストのミリ秒レベルの低遅延プル機能を体験できます。
<table>
  <tr>
    <th align="center">開発端末</th>
    <th align="center">体験版インストール</th>
    <th><div align="center">プッシュデ(Android)</div></th>
    <th><div align="center">再生デモ(Android)</div></th>
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
    <td style="text-align:center">メンテナンス中</td>
  </tr>
</table>

[](id:web)
## Webへのアクセス
### 導入の説明
ウェブサイトでCSSプッシュと再生を行う必要がある場合は、次の方式によるアクセスを推奨します：

- **Web端末CSSプッシュ**：ブラウザの一般的なWebRTCの規格をベースに設計とカプセル化を行い、コードスニペットを導入することで、ブラウザの中でCSSプッシュを実現させます。詳細については、[WebRTCプッシュ](https://intl.cloud.tencent.com/document/product/267/41620)をご参照ください。
>! 
>- WebRTCプッシュの時は、オーディオコーデック方式はopusによるコーデックとなります。標準ライブストリーミングの再生プロトコル(RTMP、FLV、HLS)を使用して再生を行う場合は、正常な視聴を確保するため、CSSバックエンドはオーディオコーデックを自動的に開始してaacに変換し、これによりオーディオトランスコード料金が発生します。詳細については、[オーディオトランスコード料金の説明](https://intl.cloud.tencent.com/document/product/267/39604#a_trans)をご参照ください。（ライブイベントストリーミングのみをご使用の場合、オーディオトランスコードは開始されません）
>- WebRTCプロトコルを使用してストリームをプッシュします。各プッシュドメイン名は、デフォルトで**1000パス同時**プッシュ数に制限されています。このプッシュ制限を超える必要がある場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してお申し出ください。

- **Web端末CSS再生**：プレーヤーSDKの[TCPlayer](https://www.tencentcloud.com/document/product/266/33977)を選択することを推奨します。スマホブラウザとPCブラウザでの**ライブイベントストリーミングWebRTCプロトコル**によるCSSストリームの再生をサポートしています。従来のライブストリーミングプロトコルに比べて、更に遅延が少なく、ミリ秒クラスの究極のライブストリーミング視聴体験を視聴者にご提供いたします。
>! WebRTCをサポートしていないブラウザ環境では、プレーヤーに渡されたWebRTCアドレスは、メディア再生をより適切にサポートするために自動的にプロトコル変換されます。デフォルトでは、モバイル端末はHLSに、PC端末はFLVに変換されます。

### Demo体験

- **Web端末CSSプッシュ**：**CSSコンソール**>[Webプッシュツール](https://console.cloud.tencent.com/live/tools/webpush)により、Web端末プッシュ機能をテストします。
- **Web端末CSSプル**：[TCPlayer](https://tcplayer.vcube.tencent.com/)ツールを使用して再生を体験いただけます。
>?
>- Web端末CSSプッシュとプルはいずれも標準WebRTCプロトコルを使用します。Web端末プッシュ時はBフレームを含まず、またオーディオコーデックはOPUSオーディオ形式のため、オーディオトランスコードおよびBフレームトランスコード料金は発生しません。
>- WebRTC Live Demoは複数の解像度をサポートし、CSSコンソールの**機能設定**>[**CSSトランスコード**](https://console.cloud.tencent.com/live/config/transcode)でハイビジョン-HD、標準-SDのトランスコードテンプレートを設定し、トランスコードテンプレート付きのWebRTCストリームアドレスをDemo中の該当する項目に入力した後、再生をテストできます（この機能のテストが不要な場合は、DemoにWebRTCオリジナルストリームを入力します）。
>- CSSトランスコードの操作ガイドとトランスコード料金の内容については、ドキュメント[CSSトランスコード](https://intl.cloud.tencent.com/document/product/267/31071)をご参照ください。

[](id:obs)
## OBS WebRTCプロトコルプッシュへのアクセス
WebRTCプロトコルプッシュは、主にビデオクラウドのライブイベントブロードキャスト（超低遅延ライブブロードキャスト）のプッシュに使用され、キャプチャされたオーディオとビデオ画面またはビデオファイルを、WebRTCプロトコルを介してライブブロードキャストサーバーにプッシュする役割を担います。下記の内容では主に、OBSツールを使用してWebRTCプロトコルプッシュ機能を実現する方法について説明します。

### 注意事項
- 現在、OBS用のバージョンは、26以降のバージョンが必要です。
- WebRTCプロトコルプッシュは現在、OBS用のWindowsプラグインのみです。MacにWebRTCストリーミングを実装する場合は、[Webアクセス](https://intl.cloud.tencent.com/document/product/267/42131)を使用できます。

[](id:set)
### OBSプラグインの設定
1. **プラグインデータを設定します**。
	1. [OBSプラグイン](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20220509.zip)をダウンロードし、dataファイルの中の2つの`services.json`および`package.json`ファイルを、対応する**data > obs-plugins > rtmp-services**ディレクトリに移動して上書きします。（`obs-studio`はデフォルトではCドライブにインストールされており、対応するディレクトリは`C:\Program Files\obs-studio\data\obs-plugins\rtmp-services`です。実際の状況に応じて設定してください。）
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
	2. これら2つのJSONファイルを`C：\Users\<コンピュータ名>\AppData\Roaming\obs-studio\plugin_config\rtmp-services`ディレクトリにコピーして上書きします。（`<コンピュータ名>`は実際の状況に応じて記入してください）。
2. **プラグイン動的ライブラリを設定します**。
`obs-plugins\64bit`のdllファイルを、対応する**obs-studio** > **obs-plugins** > **64bit**ディレクトリに移動します。（`obs-studio`はデフォルトではCドライブにインストールされており、対応するディレクトリは`C:\Program Files\obs-studio\obs-plugins\64bit`です。実際の状況に応じて設定してください。）<br>
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
## プッシュリンクの設定
[](id:push)
1. **WebRTCプッシュアドレスを発行します**。
  1. Tencent Cloudライブブロードキャストコンソールにログインし、**ライブブロードキャストツールボックス**>**[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**でプッシュアドレスを発行します。具体的な操作については、[アドレスジェネレーター](https://intl.cloud.tencent.com/document/product/267/31084)をご参照ください。
  2. 発行したアドレスのプレフィックス`rtmp`を`webrtc`に変更します。具体的な使用説明については、[自身でのライブストリーミングURLの結合](https://intl.cloud.tencent.com/document/product/267/38393) をご参照ください。

 ![](https://qcloudimg.tencent-cloud.cn/raw/e4e8118922b8f4be309e33f740152006.png)    
2. **OBSプッシュサービスを設定します**。[](id:set_obs)
  1. OBSを開いて、1番下のツールバーの**コントロール**>**設定**ボタンから設定画面に入ることができます。
  2. **プッシュ**をクリックしてストリーム設定タブに入り、サービスタイプは`Tenent webrtc`、サーバーは`Default`を選択し、ストリームキーに上記で発行した[WebRTCプッシュアドレス](#push)を入力し、その後で`&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream`を結合します。
**ストリームキーの例：**
```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```
下図に示すように：
![](https://qcloudimg.tencent-cloud.cn/raw/8035e95d3f62e62dcb3c33db2e5560d6.png)     

[](id:play)
### ライブイベントストリーミングのプル再生
ライブイベントストリーミングSDKを統合してプル再生を行います。具体的には[ライブイベントストリーミングプル](www.tencentcloud.com/document/product/1071/41875)をご参照ください。
