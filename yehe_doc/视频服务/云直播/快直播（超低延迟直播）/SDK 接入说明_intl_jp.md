ライブイベントストリーミング（LEB）は、標準ライブストリーミングを超低遅延再生シナリオ向けに拡張したサービスです。従来のライブストリーミングプロトコルに比べて、更に遅延が少なく、ミリ秒クラスの究極の**ライブストリーミング視聴**体験を視聴者に提供します。

> ! ライブイベントストリーミングはWebRTCプロトコルの低遅延特性を使用しているため、デフォルトではBフレームをサポートせず、かつオーディオコーデックはopusコーデックとしています。ライブイベントストリーミングのストリーム再生が可能なことを保証するため、プッシュ時に、Bフレームがある場合またはオーディオコーデックがopusでない場合は、CSSバックエンドが自動的にトランスコーディングを開始してBフレームを削除し、opusエンコードに変換します。これにより[標準トランスコード料金](https://intl.cloud.tencent.com/document/product/267/39604)が発生します。

[](id:app)
## APPへのアクセス
iOS、Androidのアプリの場合、MLVB SDKを統合することで、App端末でのCSSプッシュ/再生機能を実装できます。

- **App端末CSSプッシュ**：カメラ画面のキャプチャまたはスマホ画面のキャプチャをサポートし、RTMPプロトコルによって迅速にCSSサービス上にプッシュ可能です。詳細については、[カメラプッシュ](https://intl.cloud.tencent.com/document/product/1071/38157) および[スクリーンキャプチャプッシュ](https://intl.cloud.tencent.com/document/product/1071/41878)をご参照ください。
- **App端末CSS再生**：WebRTC再生プロトコルをサポートし、ライブイベントストリーミングサービスと組み合わせて低遅延ライブストリーミング体験を素早く構築します。詳細については、[ライブイベントストリーミングプル](https://intl.cloud.tencent.com/document/product/1071/41875)をご参照ください。

>? MLVB SDKはCSS、IM、TRTCなどのサービスの力を借りることで、多人数オーディオビデオの低遅延な相互接続・相互通信を実現することが可能です。多人数マイク接続によるインタラクティブな効果を実現し、マイク接続に参加しない視聴者もCSSのサービスを介して視聴することができます。詳細については、[CSSマイク接続インタラクション](https://intl.cloud.tencent.com/document/product/1071/39888)をご参照ください。

[](id:web)
## Webへのアクセス
ウェブサイトでCSSプッシュと再生を行う必要がある場合は、次の方式によるアクセスを推奨します。

- **Web端末CSSプッシュ**：ブラウザの一般的なWebRTCの規格をベースに設計とカプセル化を行い、コードスニペットを導入することで、ブラウザの中でCSSプッシュを実現させます。詳細については、[WebRTCプッシュ]](https://intl.cloud.tencent.com/document/product/267/41620)をご参照ください。
> ! WebRTCプッシュの時は、オーディオコーデック方式はopusによるコーデックとなります。標準ライブストリーミングの再生プロトコル（RTMP、FLV、HLS）を使用して再生を行う場合は、正常な視聴を保証するため、CSSバックエンドはオーディオコーデックを自動的に開始してaacに変換し、これによりオーディオトランスコード料金が発生します。詳細については、[オーディオトランスコード料金の説明](https://intl.cloud.tencent.com/document/product/267/39604#a_trans)をご参照ください。（ライブイベントストリーミングのみをご使用の場合はオーディオトランスコードは発生しません）
- **Web端末CSS再生**Player+のTCPlayerLiteを選択することを推奨します。スマホブラウザとPCブラウザでの**ライブイベントストリーミングWebRTCプロトコル**によるCSSストリームの再生をサポートしています。従来のライブストリーミングプロトコルに比べて、更に遅延が少なく、ミリ秒クラスの究極のライブストリーミング視聴体験を視聴者に提供します。
> ! WebRTCをサポートしていないブラウザ環境では、プレーヤーに渡されたWebRTCアドレスは、メディア再生をより適切にサポートするために自動的にプロトコル変換されます。デフォルトでは、モバイル端末はHLSに、PC端末はFLVに変換されます。

[](id:obs)
## OBS WebRTCプロトコルプッシュへのアクセス
WebRTCプロトコルプッシュは、主にビデオクラウドのライブイベントストリーミング（超低遅延ライブストリーミング）のプッシュに使用され、収集されたオーディオビデオ画面またはビデオファイルを、WebRTCプロトコルを介してライブストリーミングサーバーにプッシュする役割を担います。下記の内容では主に、どのようにOBSツールを使用してWebRTCプロトコルプッシュ機能を実現するかについて紹介しています。

### 注意事項
現在、OBSのバージョンは26以上が必要です。

[](id:set)
### OBSプラグインの設定
1. **プラグインデータを設定します**。
[OBSプラグイン](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20210628.zip)をダウンロードし、dataファイルの中の2つの`services.json`および`package.json`ファイルを、対応する**obs-studio** > **rtmp-service** > **data**ディレクトリに移動して上書きします。（`obs-studio`はデフォルトではCドライブにインストールされており、対応するディレクトリは`C:\Program Files\obs-studio\data\obs-plugins\rtmp-services`です。実際の状況に応じて設定してください。）
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
2. **プラグイン動的ライブラリを設定します**。
`obs-plugins\64bit`のdllおよびpdbファイルを、対応する**obs-studio** > **obs-plugins** > **64bit**ディレクトリに移動します。（`obs-studio`はデフォルトではCドライブにインストールされており、対応するディレクトリは`C:\Program Files\obs-studio\obs-plugins\64bit`です。実際の状況に応じて設定してください。）
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
## プッシュリンクの設定
[](id:push)
1. **webRTCプッシュアドレスを発行します**。
	1. Tencent Cloud CSSコンソールにログインし、**CSSツールボックス**>**[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**でプッシュアドレスを発行します。具体的な操作については[アドレスジェネレーター](https://intl.cloud.tencent.com/document/product/267/31084)をご参照ください。
	2. 発行したアドレスのプレフィックス`rtmp`を`webrtc`に変更します。具体的な使用説明については、[自身でのライブストリーミングURLの結合](https://intl.cloud.tencent.com/document/product/267/38393) をご参照ください。
![](https://main.qcloudimg.com/raw/43330aaa66610d7884f9dc02bd931dd1.png)    
2. **OBSプッシュサービスを設定します**。[](id:set_obs)
	1. OBSを開いて、1番下のツールバーの**コントロール**>**設定**ボタンから設定画面に入ることができます。
	2. **プッシュ**をクリックしてストリーム設定タブに入り、サービスタイプは`Tenent webrtc`、サーバーは`Default`を選択し、ストリームキーに上記で発行した[WebRTCプッシュアドレス](#push)を入力し、その後で`&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream`を結合します。
	**ストリームキーの例：**
```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx &stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```
下図参照：
![](https://main.qcloudimg.com/raw/2ecd72b3b97389a1f40941d04760119e.png)     

[](id:play)
### ライブイベントストリーミングのプル再生
ライブイベントストリーミングSDKを統合してプル再生を行います。具体的には[ライブイベントストリーミングプル](https://intl.cloud.tencent.com/document/product/1071/41875)をご参照ください。
