## 概要
ここでは、オーディオビデオ端末SDK（Tencent Cloud View Cube）を統合したTCPlayerを使用し、[Tencent Cloud Infinite(CI)](https://www.tencentcloud.com/document/product/1045/46980)の提供する豊富なオーディオビデオ機能と組み合わせて、WebブラウザでCOSビデオファイルを再生する方法についてご説明します。


## 統合ガイド
#### ステップ1：ページにプレーヤースタイルファイルとスクリプトファイルを導入する
```
<!--プレーヤースタイルファイル-->
<link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.min.css" rel="stylesheet">
<!--プレーヤースクリプトファイル-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.0/tcplayer.v4.5.0.min.js"></script>
```
>?
>- Player SDKを正式に使用する際は、上記の関連静的リソースをご自身でデプロイすることをお勧めします。[クリックしてプレーヤーリソースをダウンロード](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/release.zip)します。
>- デプロイし解凍した後のフォルダについては、リソースの相互引用の異常を回避するため、フォルダ内のディレクトリを調整することができません。

#### ステップ2：プレーヤーコンテナノードを設定する
プレーヤーを表示したいページ位置にプレーヤーコンテナを追加します。例えば、index.htmlに次のコードを追加します（コンテナIDおよび幅と高さはいずれもカスタマイズできます）。

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
> - プレーヤーコンテナは`<video>`タグである必要があります。
> - 例中の`player-container-id`はプレーヤーコンテナのIDであり、自身で設定することができます。
> - プレーヤーコンテナ領域のサイズについては、CSSを介して設定することをお勧めします。CSS設定はプロパティ設定よりもフレキシブルで、フルスクリーンやコンテナ適応などの効果を実現することができます。
> - 例中の`preload`属性はページのロード後にビデオをロードするかどうかを指定します。通常、ビデオ再生を高速化するため、`auto`に設定しますが、その他のオプション値には、`meta`（ページロード後にメタデータのみをロード），`none`（ページロード後にビデオをロードしない）があります。モバイル端末ではシステムの制限のために自動的にビデオをロードすることができません。
> - `playsinline`や`webkit-playsinline`といったいくつかの属性は標準的なモバイル端末ブラウザがビデオ再生をハイジャックせずにインライン再生を実現するためのものです。ここでは例示するにとどめますが、必要に応じてご使用ください。
> - `x5-playsinline`属性をTBSカーネルに設定すると、X5UIのプレーヤーを使用できます。

#### ステップ3：ビデオファイルオブジェクトアドレスを取得する
1. [バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)を行います。
2. [ビデオファイルのアップロード](https://intl.cloud.tencent.com/document/product/436/13321)を行います。
3. ビデオファイルのオブジェクトアドレスを取得します。形式は`https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<ビデオ形式>`です。

>?
> - クロスドメインの問題がある場合は、バケットのクロスドメインアクセスCORS設定を行う必要があります。詳細については、[クロスドメインアクセスの設定](https://intl.cloud.tencent.com/document/product/436/13318)をご参照ください。
> - バケットがプライベート読み取り/書き込みの場合、オブジェクトアドレスには署名が必要です。詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)をご参照ください。

#### ステップ4：プレーヤーを初期化し、COSビデオファイルのオブジェクトアドレスURLを渡す
```
var player = TCPlayer("player-container-id", {}); // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"); // COSビデオオブジェクトアドレス
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
var player = TCPlayer("player-container-id", {}); // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"); // COSビデオアドレス
```

サンプルコードを取得します。
- [MP4再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/mp4.html)
- [FLV再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/flv.html)
- [HLS再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/m3u8.html)
- [DASH再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/dash.html)


[](id:2)
### PM3U8ビデオを再生する
PM3U8はプライベートM3U8ビデオファイルのことです。COSはプライベートM3U8 TSリソースの取得に用いるダウンロード権限承認APIを提供しています。[プライベートM3U8インターフェース](https://intl.cloud.tencent.com/document/product/436/47220)をご参照ください。
```
var player = TCPlayer("player-container-id", {
	poster: "https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600" // プライベートtsリソースurlのダウンロードクレデンシャルの相対有効期間は3600秒です
});
```

サンプルコードを取得します。
- [PM3U8再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/pm3u8.html)

[](id:3)
### カバー画像を設定する
1. COSバケット上のカバー画像のオブジェクトアドレスを取得します。
>!Cloud Infinite[インテリジェントカバー](https://intl.cloud.tencent.com/document/product/1045/47740)機能により、最適なフレームを抽出してスクリーンキャプチャを生成し、それをカバーにすることでコンテンツの魅力をアップさせます。
2. カバー画像を設定します。
```
var player = TCPlayer("player-container-id", {
	poster: "https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.png"
});
```

サンプルコードを取得します。
- [カバー画像設定サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/poster.html)

[](id:4)
### HLS暗号化ビデオを再生する
ビデオコンテンツの安全性を保障し、ビデオの違法なダウンロードと拡散を防止するため、Cloud InfiniteはHLSビデオコンテンツに対する暗号化機能を提供します。この機能はプライベート読み取りファイルよりさらに高いセキュリティレベルを有します。暗号化されたビデオは、アクセス権限のないユーザーの視聴用に配信できなくなります。ビデオがローカルにダウンロードされた場合でも、ビデオ自体が暗号化されているため、悪意ある二次配信が不可能であり、ビデオの著作権が違法に侵害されないよう保障することができます。

操作手順は次のとおりです。
1. [HLS暗号化ビデオの再生](https://www.tencentcloud.com/document/product/436/48293)のフローを参照し、暗号化したビデオを生成します。
2. プレーヤーを初期化し、ビデオオブジェクトアドレスを渡します。
```
var player = TCPlayer("player-container-id", {}); // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"); // hls暗号化ビデオアドレス
```

サンプルコードを取得します。
- [HLS暗号化ビデオ再生サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/m3u8.html)

[](id:5)
### 解像度を切り替える
Cloud Infiniteの[アダプティブビットレートストリーミング](https://intl.cloud.tencent.com/document/product/1045/47745)機能は、ビデオファイルをトランスコードおよびパッケージ化し、アダプティブビットレートストリーミング出力ファイルを生成することで、ユーザーがさまざまなネットワーク状態の下でビデオコンテンツをスピーディーに配信できるようサポートするものです。プレーヤーも現在の帯域幅に応じて、最適なビットレートを動的に選択して再生できるようになります。
操作手順は次のとおりです。
1. Cloud Infiniteの[アダプティブビットレートストリーミング]()機能により、マルチビットレートアダプティブなHLSまたはDASHターゲットファイルを生成します。
2. プレーヤーを初期化し、ビデオオブジェクトアドレスを渡します。
```
var player = TCPlayer("player-container-id", {}); // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"); // マルチビットレートビデオアドレス
```

サンプルコードを取得します。
- [解像度切り替えサンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/multiDefinition.html)

[](id:6)
### 動的ウォーターマークを設定する
プレーヤーはビデオに、位置と速度が変化するウォーターマークを追加することができます。動的ウォーターマーク機能を使用する際、プレーヤーによるオブジェクトの参照をグローバル環境に公開すると、動的ウォーターマークが簡単に除去できるため、公開してはなりません。Cloud Infiniteでは、クラウド側でのビデオに対する動的ウォーターマーク追加などの操作もサポートしています。詳細についてはウォーターマークテンプレートインターフェースをご参照ください。
```
var player = TCPlayer("player-container-id", {
    plugins:{
      DynamicWatermark: {
        speed: 0.2, // 速度
        content: "Tencent Cloud Infinite CI", // テキスト
        opacity: 0.7 // 透明度
      }
    }
  });
```

サンプルコードを取得します。
- [動的ウォーターマークの設定](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/dynamicWatermark.html)

[](id:7)
### ロール画像広告を設定する
操作手順は次のとおりです。
1. ビデオ広告のカバー画像および広告リンクを準備します。
2. プレーヤーを初期化し、広告のカバー画像およびリンクを設定し、広告ノードを設定します。
```
var PosterImage = TCPlayer.getComponent('PosterImage');
PosterImage.prototype.handleClick = function () {
	window.open('https://www.tencentcloud.com/products/ci'); // 広告リンクの設定
};

var player = TCPlayer('player-container-id', {
	poster: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx..png', // 広告カバー画像
});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');

var adTextNode = document.createElement('span');
adTextNode.className = 'ad-text-node';
adTextNode.innerHTML = '広告';

var adCloseIconNode = document.createElement('i');
adCloseIconNode.className = 'ad-close-icon-node';
adCloseIconNode.onclick = function (e) {
  e.stopPropagation();
  player.posterImage.hide();
};

player.posterImage.el_.appendChild(adTextNode);
player.posterImage.el_.appendChild(adCloseIconNode);
```

サンプルコードを取得します。
- [ロール画像広告設定サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/advertise.html)

[](id:8)
### ビデオ進捗画像を設定する
操作手順は次のとおりです。
1. Cloud Infiniteで[ビデオフレームキャプチャ](https://intl.cloud.tencent.com/document/product/1045/47736)を行い、スプライトイメージを生成します。
2. ステップ1で生成したスプライトイメージとVTT（スプライトイメージの位置記述ファイル）のオブジェクトアドレスを取得します。
3. プレーヤーを初期化し、ビデオアドレスとVTTファイルを設定します。
```
var player = TCPlayer('player-container-id', {
  plugins: {
    VttThumbnail: {
      vttUrl: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.vtt' // 進捗画像VTTファイル
    },
  },
});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
```

サンプルコードを取得します。
- [ビデオ進捗画像設定サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/preview.html)

[](id:9)
### ビデオ字幕を設定する
操作手順は次のとおりです。
1. Cloud Infiniteによって音声認識を行い、字幕ファイルを生成します。
2. ステップ1で生成した字幕SRTファイルのオブジェクトアドレスを取得します。
3. プレーヤーを初期化し、ビデオアドレスと字幕SRTファイルを設定します。
```
var player = TCPlayer('player-container-id', {});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
player.on('ready', function () {
  // 字幕ファイルの追加
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.srt', // 字幕ファイル
    kind: 'subtitles',
    srclang: 'zh-cn',
    label: '中国語',
    default: 'true',
  }, true);
});
```

サンプルコードを取得します。
- [ビデオ字幕設定サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/subtitle.html)

[](id:10)
### ビデオ多言語字幕を設定する
操作手順は次のとおりです。
1. Cloud Infiniteによって音声認識と字幕ファイル生成を行い、同時に多言語に翻訳します。
2. ステップ1で生成した多言語字幕SRTファイルのオブジェクトアドレスを取得します。
3. プレーヤーを初期化し、ビデオアドレスと多言語字幕SRTファイルを設定します。
```]
var player = TCPlayer('player-container-id', {});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
player.on('ready', function () {
  // 中国語字幕の設定
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/zh.srt', // 字幕ファイル
    kind: 'subtitles',
    srclang: 'zh-cn',
    label: '中国語',
    default: 'true',
  }, true);
  // 英語字幕の設定
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/en.srt', // 字幕ファイル
    kind: 'subtitles',
    srclang: 'en',
    label: '英語',
    default: 'false',
  }, true);
});
```

サンプルコードを取得します。
- [ビデオ多言語字幕設定サンプルコード](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/multiLanguage.html)

