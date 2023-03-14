## 概要

ここでは、[DPlayer](https://dplayer.js.org/)を使用し、[Tencent Cloud Infinite(CI)](https://www.tencentcloud.com/document/product/1045/46980)の提供する豊富なオーディオビデオ機能と組み合わせて、WebブラウザでCOSビデオファイルを再生する方法についてご説明します。

## 統合ガイド

#### ステップ1：ページにプレーヤースクリプトファイルおよび必要に応じて一部依存ファイルをインポートする
```
<!--プレーヤースクリプトファイル-->
<script src="https://cdn.jsdelivr.net/npm/dplayer@1.26.0/dist/DPlayer.min.js"></script>
```
>?プレーヤーを正式に使用する際は、ご自身で上記の静的リソースをデプロイすることをお勧めします。

#### ステップ2：プレーヤーコンテナノードを設定する
プレーヤーを表示したいページ位置にプレーヤーコンテナを追加します。例えば、index.htmlに次のコードを追加します（コンテナIDおよび幅と高さはいずれもカスタマイズできます）。
```
<div id="dplayer" style="width: 100%; height: 100%"></div>
```

#### ステップ3：ビデオファイルオブジェクトアドレスを取得する
1. [バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)を行います。
2. [ビデオファイルのアップロード](https://intl.cloud.tencent.com/document/product/436/13321)を行います。
3. ビデオファイルのオブジェクトアドレスを取得します。形式は`https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<ビデオ形式>`です。

>?
> - クロスドメインの問題がある場合は、バケットのクロスドメインアクセスCORS設定を行う必要があります。詳細については、[クロスドメインアクセスの設定](https://intl.cloud.tencent.com/document/product/436/13318)をご参照ください。
> - バケットがプライベート読み取り/書き込みの場合、オブジェクトアドレスには署名が必要です。詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)をご参照ください。

#### ステップ4：プレーヤーを初期化し、COSビデオファイルのオブジェクトアドレスURLを渡す
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"); // COSビデオオブジェクトアドレス
  },
});
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
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"); // COSビデオオブジェクトアドレス
  },
});
```

サンプルコードを取得します。
- [MP4再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/mp4.html)
- [FLV再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/flv.html)
- [HLS再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/m3u8.html)
- [DASH再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/dash.html)

[](id:2)
### PM3U8ビデオを再生する
PM3U8はプライベートM3U8ビデオファイルのことです。COSはプライベートM3U8 TSリソースの取得に用いるダウンロード権限承認APIを提供しています。[プライベートM3U8インターフェース](https://intl.cloud.tencent.com/document/product/436/47220)をご参照ください。
```
 const dp = new DPlayer({
   container: document.getElementById('dplayer'),
   // pm3u8の詳細については、関連ドキュメント（https://intl.cloud.tencent.com/document/product/436/47220）をご参照ください
   video: {
     url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600' // プライベートtsリソースurlのダウンロードクレデンシャルの相対有効期間は3600秒です
   }
 });
```
サンプルコードを取得します。
- [PM3U8再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/pm3u8.html)

[](id:3)
### カバー画像を設定する
1. COSバケット上のカバー画像のオブジェクトアドレスを取得します。
>!Cloud Infinite[インテリジェントカバー](https://intl.cloud.tencent.com/document/product/1045/47740)機能により、最適なフレームを抽出してスクリーンキャプチャを生成し、それをカバーにすることでコンテンツの魅力をアップさせます。
2. プレーヤーを初期化し、カバー画像を設定します。
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
    url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4',
    pic: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.png',
  },
});
```

サンプルコードを取得します。
- [カバー画像設定サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/poster.html)

[](id:4)
### HLS暗号化ビデオを再生する
ビデオコンテンツの安全性を保障し、ビデオの違法なダウンロードと拡散を防止するため、Cloud InfiniteはHLSビデオコンテンツに対する暗号化機能を提供します。この機能はプライベート読み取りファイルよりさらに高いセキュリティレベルを有します。暗号化されたビデオは、アクセス権限のないユーザーの視聴用に配信できなくなります。ビデオがローカルにダウンロードされた場合でも、ビデオ自体が暗号化されているため、悪意ある二次配信が不可能であり、ビデオの著作権が違法に侵害されないよう保障することができます。
操作手順は次のとおりです。
1. [HLS暗号化ビデオの再生](https://intl.cloud.tencent.com/document/product/436/48293)および[COSオーディオビデオ実践 | ビデオをロックする](https://mp.weixin.qq.com/s/4f-GKyAG0S-FcZ2BZCn7jA)のフローを参照し、暗号化ビデオを生成します。
2. プレーヤーを初期化し、ビデオオブジェクトアドレスを渡します。
```
 const dp = new DPlayer({
   container: document.getElementById('dplayer'),
   video: {
     url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8' // 暗号化ビデオアドレス
   }
 });
```


サンプルコードを取得します。
- [HLS暗号化ビデオ再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/m3u8.html)

[](id:5)
### マルチ解像度切り替え

Cloud Infiniteの[アダプティブビットレートストリーミング](https://intl.cloud.tencent.com/document/product/1045/47745)機能は、ビデオファイルをトランスコードおよびパッケージ化し、アダプティブビットレートストリーミング出力ファイルを生成することで、ユーザーがさまざまなネットワーク状態の下でビデオコンテンツをスピーディーに配信できるようサポートするものです。プレーヤーも現在の帯域幅に応じて、最適なビットレートを動的に選択して再生できるようになります。詳細については、[COSオーディオビデオ実践 ｜ データワークフローによるマルチ解像度ビデオ再生のサポート](https://mp.weixin.qq.com/s/THUhur1FV_55T9zzqT2MFQ)をご参照ください。

操作手順は次のとおりです。
1. Cloud Infiniteの[アダプティブビットレートストリーミング](https://intl.cloud.tencent.com/document/product/1045/47745)機能によって、マルチビットレートのアダプティブなHLSまたはDASHターゲットファイルを生成します。
2. プレーヤーを初期化し、ビデオオブジェクトアドレスを渡します。
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8', //  マルチビットレートのHLS/DASHビデオ
  },
});
```

サンプルコードを取得します。
- [解像度切り替えサンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/multiDefinition.html)

[](id:6)
### 左上隅のロゴ設定
プレーヤーは左上隅へのロゴ設定をサポートしています。
操作手順は次のとおりです。
1. COSバケット上のロゴアイコンのオブジェクトアドレスを取得します。
2. プレーヤーを初期化し、ロゴアイコンを設定します。
```
const dp = new DPlayer({
	container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4',
  },
	logo: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.svg'
});
```

サンプルコードを取得します。
- [左上隅へのロゴ設定のサンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/logo.html)


