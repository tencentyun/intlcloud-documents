## 概要
ここでは、[VideojsPlayer](https://videojs.com/)を使用し、[Tencent Cloud Infinite(CI)](https://www.tencentcloud.com/document/product/1045/46980)の提供する豊富なオーディオビデオ機能と組み合わせて、WebブラウザでCOSビデオファイルを再生する方法についてご説明します。

## 統合ガイド

#### ステップ1：ページにプレーヤースタイルファイルとスクリプトファイルを導入する
```
<!--プレーヤースタイルファイル-->
<link href="https://vjs.zencdn.net/7.19.2/video-js.css" rel="stylesheet" />
<!--プレーヤースクリプトファイル-->
<script src="https://vjs.zencdn.net/7.19.2/video.min.js"></script>
```

>?プレーヤーを正式に使用する際は、ご自身で上記の静的リソースをデプロイすることをお勧めします。

#### ステップ2：プレーヤーコンテナノードを設定する
プレーヤーを表示したいページ位置にプレーヤーコンテナを追加します。例えば、index.htmlに次のコードを追加します（コンテナIDおよび幅と高さはいずれもカスタマイズできます）。
```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
></video>
```

#### ステップ3：ビデオファイルオブジェクトアドレスを取得する
1. [バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)を行います。
2. [ビデオファイルのアップロード](https://intl.cloud.tencent.com/document/product/436/13321)を行います。
3. ビデオファイルのオブジェクトアドレスを取得します。形式は`https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<ビデオ形式>`です。

>?
> - クロスドメインの問題がある場合は、バケットのクロスドメインアクセスCORS設定を行う必要があります。詳細については、[クロスドメインアクセスの設定](https://intl.cloud.tencent.com/document/product/436/13318)をご参照ください。
> - バケットがプライベート読み取り/書き込みの場合、オブジェクトアドレスには署名が必要です。詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)をご参照ください。

#### ステップ4：プレーヤーコンテナ内にビデオアドレスを設定し、COSビデオファイルのオブジェクトアドレスURLを渡す
```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
>
  <source
    src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
    type="video/mp4"
  />
</video>
```

## 機能ガイド
[](id:1)
### さまざまな形式のビデオファイルを再生する
1. COSバケット上のビデオファイルのオブジェクトアドレスを取得します。
>? トランスコードされていないソースビデオは再生の際に互換性の問題が生じる可能性があるため、トランスコード後のビデオで再生を行うことをお勧めします。Cloud Infiniteの[オーディオビデオトランスコーディング処理](https://intl.cloud.tencent.com/document/product/1045/49543)により、さまざまな形式のビデオファイルを取得することができます。
2. さまざまなビデオ形式に対し、マルチブラウザでの互換性を保証するためには、対応する依存関係の導入が必要です。
 - MP4：他の依存関係を導入する必要はありません。
 - HLS：ChromeやFirefoxなどの最新ブラウザでH5を介してHLS形式のビデオを再生したい場合は、 tcplayer.min.js の前にhls.min.jsを導入する必要があります。
```
  <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/libs/hls.min.0.13.2m.js"></script>
```
 - FLV：ChromeやFirefoxなどの最新ブラウザでH5を介してFLV形式のビデオを再生したい場合は、 tcplayer.min.js の前にflv.min.jsを導入する必要があります。
```
  <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/libs/flv.min.1.6.2.js"></script>
```
 - DASH：DASHビデオにはdash.all.min.jsファイルのロードが必要です。
```
  <script src="https://cos-video-1258344699.cos.ap-guangzhou.myqcloud.com/lib/dash.all.min.js"></script>
```
3. プレーヤーを初期化し、オブジェクトアドレスを渡します。
```
<!-- MP4 -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
  type="video/mp4"
/>

<!-- HLS -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"
  type="application/x-mpegURL"
/>

<!-- FLV -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.flv"
  type="video/x-flv"
/>

<!-- DASH -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mpd"
  type="application/dash+xml"
/>
```

サンプルコードを取得します。
- [MP4再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/mp4.html)
- [FLV再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/flv.html)
- [HLS再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/m3u8.html)
- [DASH再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/dash.html)

[](id:2)
### PM3U8ビデオを再生する
PM3U8はプライベートM3U8ビデオファイルのことです。COSはプライベートM3U8 TSリソースの取得に用いるダウンロード権限承認APIを提供しています。[プライベートM3U8インターフェース](https://intl.cloud.tencent.com/document/product/436/47220)をご参照ください。
```
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600"
  type="application/x-mpegURL"
/>
```

サンプルコードを取得します。
- [PM3U8再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/pm3u8.html)

[](id:3)
### カバー画像を設定する
1. COSバケット上のカバー画像のオブジェクトアドレスを取得します。
>!Cloud Infinite[インテリジェントカバー](https://intl.cloud.tencent.com/document/product/1045/47740)機能により、最適なフレームを抽出してスクリーンキャプチャを生成し、それをカバーにすることでコンテンツの魅力をアップさせます。
2. プレーヤーを初期化し、カバー画像を設定します。
```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
  poster="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/poster.png"
>
  <source
    src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
    type="video/mp4"
  />
</video>
```

サンプルコードを取得します。
- [カバー画像設定サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/poster.html)

[](id:4)
### HLS暗号化ビデオを再生する
ビデオコンテンツの安全性を保障し、ビデオの違法なダウンロードと拡散を防止するため、Cloud InfiniteはHLSビデオコンテンツに対する暗号化機能を提供します。この機能はプライベート読み取りファイルよりさらに高いセキュリティレベルを有します。暗号化されたビデオは、アクセス権限のないユーザーの視聴用に配信できなくなります。ビデオがローカルにダウンロードされた場合でも、ビデオ自体が暗号化されているため、悪意ある二次配信が不可能であり、ビデオの著作権が違法に侵害されないよう保障することができます。
操作手順は次のとおりです。
1. [HLS暗号化ビデオの再生](https://intl.cloud.tencent.com/document/product/436/48293)および[COSオーディオビデオ実践 | ビデオをロックする](https://mp.weixin.qq.com/s/4f-GKyAG0S-FcZ2BZCn7jA)のフローを参照し、暗号化ビデオを生成します。
2. プレーヤーを初期化し、ビデオオブジェクトアドレスを渡します。
```
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"
  type="application/x-mpegURL"
/>
```

サンプルコードを取得します。
- [HLS暗号化ビデオ再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/m3u8.html)



