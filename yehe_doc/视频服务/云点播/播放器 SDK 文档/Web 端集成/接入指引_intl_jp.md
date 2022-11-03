このドキュメントでは、VOD再生とCSS再生に適用されるWeb Player+（TCPlayer）についてご紹介します。それは高速で自由にWebアプリケーションを統合し、ビデオ再生機能を実現します。Web Player+（TCPlayer）内にはデフォルトで一部のUIが含まれ、必要に応じて取得することができます。
## 概要
WebプレーヤーはHTML5の`<video>`タグおよびFlashを介してビデオ再生を実現します。ブラウザがビデオ再生をサポートしていない場合に、ビデオ再生効果のマルチプラットフォーム統合体験を実現し、かつTencent Cloud Video on Demand Video Serviceと組み合わせて、リンク不正アクセス防止とHLS共通暗号化ビデオ再生などの機能を提供します。


### プロトコルのサポート

<table>
<tr><th style="text-align:center">オーディオビデオプロトコル</th><th>用途</th><th>URLアドレス形式</th><th>PCブラウザ</th><th>モバイルブラウザ</th>
</tr>
<tr>
<td style="text-align:center">MP3</td>
<td>オーディオ</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.mp3</code></td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td style="text-align:center">MP4</td>
<td>オンデマンド</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.mp4</code></td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td rowspan=2 style="text-align:center">HLS<br>(M3U8)</td>
<td>ライブストリーミング</td>
<td><code>http://xxx.liveplay.myqcloud.com/xxx.m3u8</code></td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr><tr>
<td>オンデマンド</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.m3u8</code></td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr><tr>
<td rowspan=2 style="text-align:center">FLV</td>
<td>ライブストリーミング</td>
<td><code>http://xxx.liveplay.myqcloud.com/xxx.flv</code></td>
<td>サポートしています</td>
<td>一部サポートしています</td>
</tr><tr>
<td>オンデマンド</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.flv</code></td>
<td>サポートしています</td>
<td>一部サポートしています</td>
</tr>
<tr>
<td style="text-align:center">WebRTC</td>
<td>ライブストリーミング</td>
<td><code>webrtc://xxx.liveplay.myqcloud.com/live/xxx</code></td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
</table>


<dx-alert infotype="explain" title="">
- ビデオコーデック形式はH.264コードのみをサポートしています。
- プレーヤーは一般的なブラウザと互換性があり、プレーヤーは内部で自動的にプラットフォームを区別し、最適な再生方式を使用します。
- 一部のブラウザ環境でHLSおよびFLVビデオを再生する場合、[Media Source Extensions](https://caniuse.com/?search=Media%20Source%20Extensions)に依存する必要があります。
- WebRTCをサポートしていないブラウザ環境では、プレーヤーに渡されたWebRTCアドレスは、メディア再生をより適切にサポートするために自動的にプロトコル変換されます。
</dx-alert>

## 機能サポート

<Table>
  <tr>
    <th width="50px" style="text-align:center">機能\ブラウザ</th>
      <th width="50px" style="text-align:center">Chrome</th>
      <th width="50px" style="text-align:center">Firefox</th>
      <th width="50px" style="text-align:center">Edge</th>
      <th width="50px" style="text-align:center">QQブラウザ</th>
      <th width="50px" style="text-align:center">Mac Safari</th>
      <th width="50px" style="text-align:center">iOS Safari</th>
      <th width="50px" style="text-align:center">WeChat</th>
      <th width="50px" style="text-align:center">Android Chrome</th>
      <th width="50px" style="text-align:center">IE 11</th>
  </tr>
     <tr>
         <td style="text-align:center">プレーヤーサイズ設定</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">再生継続設定機能</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">倍速再生</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">サムネイルプレビュー</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
            <tr>
         <td style="text-align:center">fileIDを切り替えて再生</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
            <tr>
         <td style="text-align:center">イメージ機能</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">プログレスバーの表示</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">HLSアダプティブビットレート</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">Refererホットリンク防止</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">解像度切り替えプロンプト</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">プレビュー機能</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
    <tr>
         <td style="text-align:center">HLS標準暗号化再生</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
  	<tr>
         <td style="text-align:center">HLSプライベート暗号化再生</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">
      		<ul>
            <li nowrap="nowrap">Android: &#10003;</li><br>
            <li nowrap="nowrap">iOS: -</li>
           </ul>	
      	</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">ビデオ統計情報</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
    </tr>
    <tr>
         <td style="text-align:center">ビデオデータモニタリング</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
    </tr>
               <tr>
         <td style="text-align:center">カスタムプロンプトテキスト</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
    <tr>
         <td style="text-align:center">カスタムUI</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
  	<tr>
         <td style="text-align:center">弾幕</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
    <tr>
         <td style="text-align:center">ウォーターマーク</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
    <tr>
         <td style="text-align:center">ビデオリスト</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
     <tr>
         <td style="text-align:center">脆弱ネットワーク追跡フレーム</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
</Table>
<dx-alert infotype="explain" title="">
- ビデオコーデック形式はH.264コードのみをサポートしています。
- Chrome、FirefoxにはWindows、macOSプラットフォームが含まれます。
- Chrome、Firefox、Edge、QQブラウザでHLSを再生するには、`hls.js`をダウンロードする必要があります。
- Refererリンク不正アクセス防止機能はHTTPリクエストヘッダーのRefererフィールドをもとに実現されます。一部のAndroidブラウザが開始するHTTPリクエストにはRefererフィールドを付加することができません。
</dx-alert>

プレーヤーは一般的なブラウザと互換性があり、プレーヤーがプラットフォームを自動的に識別し、最適な再生方式を使用します。例としては、Chromeなどの最新ブラウザではHTML5技術を優先的に使用してビデオ再生を実現します。またスマホブラウザでは、HTML5技術やブラウザカーネル機能を使用してビデオ再生を実現します。


## 統合ガイド

次の手順でウェブページにビデオプレーヤーを追加することができます。

### 手順1：ホームにファイルを導入します

ローカルプロジェクトにindex.htmlファイルを新規作成し、htmlページ内にプレーヤースタイルファイルとスクリプトファイルをインポートします。
```html
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/tcplayer.min.css" rel="stylesheet"/>
 <!--ChromeやFirefoxなどの最新ブラウザでH5を介してWebrtcのビデオを再生したい場合は、tcplayer.vx.x.x.min.jsの前にTXLivePlayer-x.x.x.min.jsをインポートする必要があります。-->
 <!--中にはWebrtcに対応していないブラウザ環境もあり、プレーヤーはWebrtcのストリームアドレスをHLS形式のアドレスに自動変換するため、ライブイベントストリーミングのシナリオでは同様に、hls.min.x.xx.xm.jsをインポートする必要があります。-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/TXLivePlayer-1.2.3.min.js"></script>
 <!--ChromeやFirefoxなどの最新ブラウザでH5を介してChromeやFirefoxなどのモダンブラウザでHLSプロトコルのビデオを再生したい場合は、tcplayer.vx.x.x.min.jsの前にhls.min.x.xx.xm.jsをインポートする必要があります。-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/hls.min.1.1.5.js"></script>
 <!--ChromeやFirefoxなどの最新ブラウザでH5を介してChromeやFirefoxなどのモダンブラウザでFLV形式のビデオを再生したい場合は、tcplayer.vx.x.x.min.jsの前にflv.min.x.jsをインポートする必要があります。-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/flv.min.1.6.3.js"></script>
  <!--ChromeやFirefoxなどの最新ブラウザでH5を介してDASHビデオを再生したい場合は、tcplayer.vx.x.x.min.jsの前にdash.min.x.x.x.jsを導入する必要があります。-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/dash.all.min.4.4.1.js"></script>
 <!--プレーヤースクリプトファイル-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/tcplayer.v4.5.4.min.js"></script>
```
プレーヤーSDKを使用する場合は、ご自身でリソースをデプロイすることをお勧めします。[クリックしてプレーヤーリソースをダウンロード](https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/release.zip)します。
デプロイし解凍した後のフォルダについては、リソースの相互引用の異常を回避するため、フォルダ内のディレクトリを調整することができません。
デプロイするアドレスが`aaa.xxx.ccc`である場合は、適切な場所にプレーヤースタイルファイルとスクリプトファイルを導入します。
```html
 <link href="aaa.xxx.ccc/tcplayer.min.css" rel="stylesheet"/>
 <!--ChromeやFirefoxなどの最新ブラウザでH5を介してChromeやFirefoxなどのモダンブラウザでHLS形式のビデオを再生したい場合は、tcplayer.vx.x.x.min.jsの前にhls.min.x.xx.m.jsをインポートする必要があります。-->
 <script src="aaa.xxx.ccc/libs/hls.min.x.xx.m.js"></script>
 <!--プレーヤースクリプトファイル-->
 <script src="aaa.xxx.ccc/tcplayer.vx.x.x.min.js"></script>
```

### 手順2：プレーヤーコンテナを配置します

プレーヤーを表示したいページ位置にプレーヤーコンテナを追加します。例えば、index.htmlに次のコードを追加します（コンテナIDおよび幅と高さはいずれもカスタマイズできます）。
```html
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
>
>- プレーヤーコンテナは`<video>`タグである必要があります。
>- 例中の`player-container-id`はプレーヤーコンテナのIDであり、自身で設定することができます。
>- プレーヤーコンテナ領域のサイズについては、CSSを介して設定することをお勧めします。CSS設定はプロパティ設定よりもフレキシブルで、フルスクリーンやコンテナ適応などの効果を実現することができます
>- 例中の`preload`属性はページのロード後にビデオをロードするかどうかを指定します。通常、ビデオ再生を高速化するため、`auto`に設定しますが、その他のオプション値には、`meta`（ページロード後にメタデータのみをロード），`none`（ページロード後にビデオをロードしない）があり、モバイル端末はシステムの制限のために自動的にビデオをロードすることができません。
>- `playsinline`や`webkit-playsinline`といったいくつかの属性は標準的なモバイル端末ブラウザがビデオ再生をハイジャックせずにインライン再生を実現するためのものです。ここでは例示するにとどめますが、必要に応じてご使用ください。
>- `x5-playsinline`属性をTBSカーネルに設定すると、X5UIのプレーヤーを使用できます。

### ステップ3：プレーヤーの初期化
ページが初期化されると、ビデオリソースを再生できるようになります。プレーヤーは、オンデマンドとライブストリーミングといった両方のシナリオをサポートします。具体的な再生方法は以下のとおりです。
- VOD再生：プレーヤーは、FileIDを介してTencent Cloudオンデマンドメディアリソースを再生することができます。VODの具体的な手順については、[プレーヤーで再生 > アクセスガイドライン](https://intl.cloud.tencent.com/document/product/266/38098)ドキュメントをご参照ください。
- ライブストリーミング再生：プレーヤーはURLアドレスを渡すことで、ライブストリーミングオーディオビデオストリームをプルしてライブストリーミングを再生することができます。Tencent Cloud CSSのURL生成方法については、[自身でのライブストリーミングURLの結合](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。

<dx-tabs>
::: URLによる再生（ライブストリーミング、オンデマンド）
ページが初期化された後、プレーヤーインスタンスのメソッドが呼び出され、URLアドレスがメソッドに渡されます。
<dx-codeblock>
:::  javascript
var player = TCPlayer('player-container-id', {}); // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
player.src(url); // url再生アドレス
:::
</dx-codeblock>

:::
::: FileIDによって再生（オンデマンド）
index.htmlページ初期化コードに次の初期化スクリプトを追加し、準備作業で取得したfileID（[**メディア資産管理**](https://console.cloud.tencent.com/vod/media)中のビデオID）とappID（**アカウント情報**>[**基本情報**](https://console.cloud.tencent.com/developer)で表示）を渡します。

<dx-codeblock>
:::  javascript
var player = TCPlayer('player-container-id', { // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
    fileID: '3701925921299637010', // 再生したいビデオfileIDを渡してください（必須）
    appID: '1500005696' // VODアカウントのappIDを渡してください（必須）
  //プライベートの暗号化再生にはpsignの入力が必要です。psignはプレーヤーの署名です。署名についての紹介および生成方法については、以下のリンクをご参照ください。https://www.tencentcloud.com/document/product/266/38099
  //psign:'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAwNTY5NiwiZmlsZUlkIjoiMzcwMTkyNTkyMTI5OTYzNzAxMCIsImN1cnJlbnRUaW1lU3RhbXAiOjE2MjY4NjAxNzYsImV4cGlyZVRpbWVTdGFtcCI6MjYyNjg1OTE3OSwicGNmZyI6InByaXZhdGUiLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI5YzkyYjBhYiJ9LCJkcm1MaWNlbnNlSW5mbyI6eyJleHBpcmVUaW1lU3RhbXAiOjI2MjY4NTkxNzksInN0cmljdE1vZGUiOjJ9fQ.Bo5K5ThInc4n8AlzIZQ-CP9a49M2mEr9-zQLH9ocQgI',
});
:::
</dx-codeblock>

>!再生したいビデオは、Tencent Cloudを使用してトランスコードすることをお勧めします。ブラウザでのオリジナルビデオの正常な再生を保証することはできません。
:::
</dx-tabs>

### ステップ4：その他の機能
このプレーヤーは、Video on Demandのサーバー機能と組み合わせて、アダプティブビットレートストリーミング、プレビュービデオのサムネイル、ビデオマーカー情報の追加といった高度な機能を実装できます。これらの機能は、[長編ビデオ再生スキーム](https://intl.cloud.tencent.com/document/product/266/44191)で詳しく説明されていますので、ドキュメントを参照しながら実装することができます。

この他にも、プレーヤーにはさまざまな機能が提供されています。機能リストとその使用方法については、[機能表示](https://tcplayer.vcube.tencent.com/)ページをご参照ください。
