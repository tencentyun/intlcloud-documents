QUIC(Quick UDP Internet Connection)とは、Googleが開発したUDPプロトコルをベースとした次世代の高品質トランスポートプロトコルです。2018年以降、IETFはQUICプロトコルをHTTP/3.0ネットワークプロトコルの標準として、普及を進めています。QUICプロトコルはTCPプロトコルと比較すると、脆弱なネットワークや高いパケット損失というシナリオでのデータ送信に適しています。

Tencent Video Cloudは現在、QUICプロトコルを使用した[CSSプッシュ](#push)と[CSSプル](#play)をサポートしています。

## プロトコルバージョンのサポート

CSSで現在サポートされているQUICプロトコルのバージョン：39、41、42、43、44。

> ! バージョン43の使用をお勧めします。

## 注意事項

QUICプル機能を使用する必要がある場合は、Tencent Cloudに[チケットを提出](https://console.cloud.tencent.com/workorder/category)して、プルドメイン名に対応するQUICプロトコルプル機能をアクティブ化するようにしてください。


## CSSプッシュ

[](id:push)

### アクセス方法
CSSプッシュはRTMP over QUICプロトコルをサポートしますが、UDP 1935を使用してプッシュする必要があります。プッシュアドレスはRTMP over TCPプロトコルと同様で、CSSコンソールの【[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)】の中で[プッシュアドレスの生成](https://intl.cloud.tencent.com/document/product/267/31084)を行うことができます。

![](https://main.qcloudimg.com/raw/31d20b09de1c8d3c9748872e59f9a828.png)


プッシュアクセスの方法には、次の2種類があります。

- **Tencent Cloudの[モバイルライブストリーミングSDK](https://intl.cloud.tencent.com/document/product/1071/38150)**を使用：使用方法はRTMP over TCPと同様で、SDKはデフォルトでQUICプロトコルを使用してTencent Cloudへアクセスします。
- **独自のQUICプロトコルクライアントを使用**：標準ライブストリーミングによって生成されたプッシュアドレスを介して、直接QUICプロトコルプッシュを開始できます。RTMP over QUICのプッシュアドレスとRTMP over TCPのプッシュアドレスは同じです。QUICプロトコルプッシュは、Tencent CloudのQUICストリーミングサーバーに直接接続します。

[](id:pushtest)


## ライブストリーミングのプル

[](id:play)

### プルアクセス

CSSプルはHTTP over QUICプロトコルをサポートしますが、UDP 443ポートを使用してプルする必要があります。プルストリーミングアドレスはHTTP FLVプロトコルのアドレスと同様です。また、CSSコンソールの【[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)】の中で[プルストリーミングアドレスの生成](https://intl.cloud.tencent.com/document/product/267/31084)を行うこともできます。
![](https://main.qcloudimg.com/raw/e4727db59f2e195abdd9382456212d14.png)

[](id:playtest)

### プルテスト

Tencent Cloudの[TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/vcplayer/demo/tcplayer-test.html)ツールを使用してテストを行うことができます。具体的な手順は次のとおりです。
> ? ChromeブラウザはQUICプロトコルリクエストをサポートしています。ChromeブラウザとTencent CloudのTCPlayerDemoを連携させて使用すると、QUICプロトコルを使用して再生されたかどうか検証することができます。

1. ChromeのQUICスイッチをオンにします。
   Chromeブラウザのアドレスバーに`chrome://flags/#enable-quic `と入力し、スイッチをEnabledに設定して、Chromeブラウザを再起動すれば完了です。
   ![](https://main.qcloudimg.com/raw/b5aee3532ef918518206b607cc2d8f53.png) 
2. TCPlayerDemoを開き、HTTPS再生アドレスを入力するときは、FLVおよびHLSのプルストリーミングアドレスを使用することをお勧めします。RTMPのアドレスは、Flash再生のみをサポートしています。「生成」をクリックして接続した後、![](https://main.qcloudimg.com/raw/5886ad8b68619d7ba99268e0a4e24f2c.png)をクリックして再生を開始します。
![](https://main.qcloudimg.com/raw/a2e4d83ca259b97b4376875215015a22.png)
3. Chromeの開発者ツールにおいて【Network】タブを選択すると、リクエストされたプロトコルがすでに`http/2+quic/46`であることが確認できます。
![](https://main.qcloudimg.com/raw/e1e61b7ae544881b898ccd7aa116e8a4.png)

> ? 
> - ブラウザのバージョンが異なります。QIUCのバージョン番号が若干異なる場合があります。
> - Protocolフィールドがデフォルトで表示されていない場合は、ディスプレイを右クリックし、Protocolにチェックを入れると表示することができます。
> ![](https://main.qcloudimg.com/raw/ee21e41e7f61e87dccb2f2509ff7678d.png)
