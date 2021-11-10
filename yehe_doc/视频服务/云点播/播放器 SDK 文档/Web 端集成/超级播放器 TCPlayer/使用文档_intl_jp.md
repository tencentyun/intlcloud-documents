このドキュメントでは、Tencent Cloudのカスタマーがフレキシブルなインターフェースを介して、すばやく自身のWebアプリケーションを統合し、ビデオ再生機能を実現する、Tencent Cloud View Cube Web Super Player（TCPlayer）について説明します。このドキュメントはある程度Javascript言語の基礎がある開発者向けです。

## 機能紹介
Tencent Cloud View Cube Web Super PlayerはHTML5の`<Video>`タグおよびFlashを介してビデオ再生を実現します。ブラウザがビデオ再生をサポートしていない場合に、ビデオ再生効果のマルチプラットフォーム統合体験を実現し、かつTencent Cloud Video on Demandサービスと組み合わせて、ホットリンク防止とHLS共通暗号化ビデオ再生などの機能を提供します。

[](id:function)
### 機能のサポート

<Table>
  <tr>
    <th width="50px" style="text-align:center">機能\ブラウザ</th>
      <th width="50px" style="text-align:center">Chrome</th>
      <th width="50px" style="text-align:center">Firefox</th>
      <th width="50px" style="text-align:center">Edge</th>
      <th width="50px" style="text-align:center">QQブラウザ</th>
      <th width="50px" style="text-align:center">Mac Safari</th>
      <th width="50px" style="text-align:center">iOS Safari</th>
      <th width="50px" style="text-align:center">iOS WeChat QQ</th>
      <th width="50px" style="text-align:center">Android Chrome</th>
      <th width="50px" style="text-align:center">Android WeChat、QQ</th>
      <th width="50px" style="text-align:center">スマホQQブラウザ</th>
      <th width="50px" style="text-align:center">IE 8, 9, 10, 11</th>
  </tr>
   <tr>
         <td style="text-align:center">MP4フォーマット</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
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
         <td style="text-align:center">HLSフォーマット</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
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
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">- <br>（11サポート）</td>
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
         <td style="text-align:center">-</td>
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
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
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
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">HLS暗号化再生</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
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
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>

</Table>

>?
>- ビデオコーデック形式はH.264コードのみをサポートしています。
>- Chrome、FirefoxにはWindows、macOSプラットフォームが含まれます。
>- Chrome、Firefox、EdgeおよびQQブラウザでHLSを再生するには、`hls.js`をダウンロードする必要があります。
>- Android WeChat、QQがTBSカーネルである場合は、MP4、HLSの再生をネイティブサポートしています。
>- Refererホットリンク防止機能はHTTPリクエストヘッダーのRefererフィールドをもとに実現されます。一部のAndroidブラウザが開始するHTTPリクエストにはRefererフィールドを付加することができません。
>- IE8がFlash再生を採用し、IE9/10/11のHLS再生時にFlash再生を採用する場合は、ブラウザサポートFlashプラグインを確保する必要があります。
>- IE8はWindows7システムのIE8のみをサポートしています。

プレーヤーは一般的なブラウザと互換性があり、プレーヤーがプラットフォームを自動的に識別し、最適な再生プランを使用します。例：IE11/10/9/8ブラウザではFlashプレーヤーを使用して、サポートされていないHTML5でのHLS再生機能を実現し、Chromeなどの最新ブラウザではHTML5技術を優先的に使用してビデオ再生を実現します。またスマホブラウザではHTML5技術やブラウザカーネル機能を使用してビデオ再生を実現します。

### VODプラットフォームのトランスコードサービス
MP4とHLS（M3U8）は、現在、デスクトップブラウザとスマホブラウザでのサポート範囲が最も広いフォーマットであることから、Tencent CloudのビデオVODプラットフォームは最終的にアップロードされたビデオをMP4とHLS（M3U8）形式で公開します。
[](id:preparation)
## 準備作業

具体的な手順については[Super Playerで再生 - アクセスガイドライン](https://intl.cloud.tencent.com/document/product/266/38098)ドキュメントをご参照ください。

## Webプレーヤーの初期化
準備作業が完了したら、次の手順でウェブページにビデオプレーヤーを追加することができます。
[](id:step1)
### 手順1：ホームにファイルを導入します
適切な場所にプレーヤースタイルファイルとスクリプトファイルを導入します。
```
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.min.css" rel="stylesheet">
 <!--ChromeやFirefoxなどの最新ブラウザで、H5を介してHLS形式のビデオを再生したい場合は、tcplayer.v4.2.min.jsの前にhls.min.0.13.2m.jsを導入する必要があります。-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/libs/hls.min.0.13.2m.js"></script>
 <!--プレーヤースクリプトファイル-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.v4.2.1.min.js"></script>
```

Player+を使用する場合は、自身でリソースをデプロイすることをお勧めします。[クリックしてプレーヤーリソースをダウンロード](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/release.zip)します。

デプロイし解凍した後のフォルダについては、リソースの相互引用の異常を回避するため、フォルダ内のディレクトリを調整することができません。

デプロイするアドレスが`aaa.xxx.ccc`である場合は、適切な場所にプレーヤースタイルファイルとスクリプトファイルを導入します。
```
 <link href="aaa.xxx.ccc/tcplayer.min.css" rel="stylesheet">
 <!--ChromeやFirefoxなどの最新ブラウザでH5を介して形式のビデオを再生したい場合は、tcplayer.v4.2.1.min.jsの前にhls.min.0.13.2m.jsを導入する必要があります。-->
 <script src="aaa.xxx.ccc/libs/hls.min.0.13.2m.js"></script>
 <!--プレーヤースクリプトファイル-->
 <script src="aaa.xxx.ccc/tcplayer.v4.2.1.min.js"></script>
```

>?VUE Reactなどのフレームワークモジュールのロード方式を現時点ではサポートしていません。scriptを介して関連スクリプトをグローバルに導入する方式で使用できます。
[](id:step2)
### 手順2：プレーヤーコンテナを配置します
プレーヤーを表示したいページ位置にプレーヤーコンテナを追加します。例えば、index.htmlに次のコードを追加します（コンテナIDおよび幅と高さはいずれもカスタマイズできます）。
```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
>- プレーヤーコンテナは`<Video>`タグである必要があります。
>- 例中の`player-container-id`はプレーヤーコンテナのIDであり、自身で設定することができます。
>- プレーヤーコンテナ領域のサイズについては、CSSを介して設定することをお勧めします。CSS設定はプロパティ設定よりもフレキシブルで、フルスクリーンやコンテナ適応などの効果を実現することができます
>- 例中の`preload`属性はページのロード後にビデオをロードするかどうかを指定します。通常、ビデオ再生を高速化するため、`auto`に設定しますが、その他のオプション値には、`meta`（ページロード後にメタデータのみをロード），`none`（ページロード後にビデオをロードしない）があり、モバイル端末はシステムの制限のために自動的にビデオをロードすることができません。
>- `playsinline`や`webkit-playsinline`といったいくつかの属性は標準的なモバイル端末ブラウザがビデオ再生をハイジャックせずにインライン再生を実現するためのものです。ここでは例示するにとどめますが、必要に応じてご使用ください。
>- `x5-playsinline`属性をTBSカーネルに設定すると、X5UIのプレーヤーを使用できます。
[](id:step3)
### 手順3：コードの初期化
ページ初期化コードに次の初期化スクリプトを追加し、準備作業で取得したfileID（[【メディア資産管理】](https://console.cloud.tencent.com/vod/media)中のビデオID）とappID（【アカウント情報】>[【基本情報】](https://console.cloud.tencent.com/developer)で表示）を渡します。
```
var player = TCPlayer('player-container-id', { // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
    fileID: '5285890799710670616', // 再生したいビデオfileIDを渡してください（必須）
    appID: '1400329073' // VODアカウントのappIDを渡してください（必須）
  });
```

>!再生したいビデオはTencent Cloudを介してトランスコードする必要があり、ブラウザでのオリジナルビデオの正常な再生を保証することはできません。
[](id:fullExample)
## サンプルページの完成
[サンプルコード](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)をクリックし、サンプルページに移動します。このページでマウスを右クリックし【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。
## 機能の使用説明
以下、プレーヤーの一部機能（ベストプラクティスと注意事項を含む）を詳細に説明します。
### プレーヤーサイズの設定
ここではいくつかのプレーヤーサイズ設定方法について紹介します。

* ![](https://main.qcloudimg.com/raw/9576adc95470eee7ec036688e6cae8c7.png)にタグを送りwidthとheight属性を設定することができます。widthとheightの属性値はピクセルで計算され（例：width=「100px」またはwidth=100）、パーセンテージで設定することはできません。
* CSSを介してサイズを設定することで、ピクセルとパーセンテージなどのタイプの値（例：width:「100px」またはwidth:「100%」）をサポートすることができます。

>?
>- 幅と高さを設定しない場合、プレーヤーはビデオの解像度を取得した後、ビデオの解像度を利用してプレーヤーの表示サイズを設定することができますが、ブラウザの可視領域サイズがビデオの解像度を下回る場合は、プレーヤー領域がブラウザの可視領域を超えてしまうため、通常は、この方法をお勧めしません。ベストプラクティスはCSSを介してプレーヤーのサイズを設定することです。
>- CSSを上手に使用することで、フルスクリーンやコンテナ適応などの効果を実現することができます。

#### 事例
- [CSSを利用したサイズの設定](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size.html)
- [フルサイズウェブページ可視領域](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-full-viewport.html)
- [等比適応](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-adaptive.html)

サンプルページに移動し、このページでマウスを右クリックして、【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。

### 再生継続機能
再生継続機能を有効にする前提として、fileIDを使用して再生する必要があります。一意のfileIDがある場合に限り、プレーヤーはこのビデオの再生時間を記録することができます。再生が終わる前にページを閉じ、同じブラウザで再生ページを再度開く場合は、前回視聴した時点から再生を継続することができます。次のパラメータを介して再生継続機能を有効にします。

```
var player = TCPlayer('player-container-id', {
    fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
    appID: '', // VODアカウントのappIDを渡してください（必須）
    plugins:{
        ContinuePlay: { // 再生継続機能を有効にします
          // auto: true, //[オプション]ビデオ再生後に自動的に再生を継続するかどうか
          // text:'前回の再生 ',//[オプション]プロンプトテキスト
          // btnText: '再生再開'//[オプション]ボタンテキスト
        },
      }
  });
```
正常に有効化された後に表示される効果は下図のとおりです。
![](https://mc.qcloudimg.com/static/img/e155be329a6fec959e1ad6b361add390/image.png)

#### 事例
[再生継続](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-continue-play.html)をクリックしてサンプルページに移動し、このページでマウスを右クリックして、【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。
>!
> - この機能を使用するには、fileIDとappIDを使用してTencent Cloudによってトランスコードされたビデオを再生する必要があります。
> - この機能はlocalStorageを介して再生時点をストレージしますので、ブラウザはこの特性をサポートしている必要があります。
> - ブラウザがビデオ再生をハイジャックする場合は、この機能を使用することができません。
> - この機能は複数端末、複数ブラウザで相互運用されるものではなく、例えばPCブラウザで見終わっていない場合は、モバイル端末のブラウザやPCの別のブラウザで再生を継続することはできません。追加のインターフェースが必要な場合は、自身で開発することができます。

### 倍速再生
ブラウザがサポートしている場合、プレーヤーの倍速再生機能はデフォルトで有効です。

```
var player = TCPlayer('player-container-id', {
  fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
  appID: '', // VODアカウントのappIDを渡してください（必須）
  playbackRates: [0.5, 1, 1.25, 1.5, 2] // 変速再生倍率オプションを設定します。HTML5再生モードでのみ有効です
});
```

>!
>- ブラウザが倍速再生をサポートしていない場合、プレーヤーには倍速切り替えボタンが表示されません。
>- この機能を終了したい場合は、[開発ドキュメント](https://intl.cloud.tencent.com/document/product/266/42095)をご参照ください。


### サムネイルプレビュー
VOD Super Playerはサムネイルプレビューをサポートしています。この機能を有効にするには、2つの方法があります。
- サーバーAPIを介してビデオのサムネイルとVTTファイルを生成します。関連ドキュメントについては、[スクリーンキャプチャ-スプライトイメージ](https://intl.cloud.tencent.com/document/product/266/33940)をご参照ください。
- サムネイルファイルとVTTファイルを自身で生成し、2つのファイルのURLをプレーヤーに渡します。参考示例「サムネイルプレビュー-サムネイルとVTTファイルを渡す」の事例をご参照ください

正常に有効化された場合の効果は次のとおりです。
![](https://main.qcloudimg.com/raw/cf668bbf1a991c347fbeacb6555831c1.png)

#### 事例
- [サムネイルプレビュー-サーバーの生成](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail.html)
- [サムネイルプレビュー-サムネイルとVTTファイルを渡す](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail-src.html)

サンプルページに移動し、このページでマウスを右クリックして、【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。
>!
>- この機能はデスクトップブラウザのみをサポートしています。
>- ブラウザがビデオ再生をハイジャックする場合は、この機能を使用することができません。
>- 生成するサムネイルが多いほど、プログレスバーのプレビューは正確になりますが、サムネイルが多いほど、画像のロードは遅くなりますので、バランスを考える必要があります。

### fileIDを切り替えて再生
オブジェクトのloadVideoByID（args）方法をインスタンス化することにより、再生するビデオを変更することができます。この方法でサポートされるパラメータは次のとおりです。
```
player.loadVideoByID({
  fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
  appID: '', // VODアカウントのappIDを渡してください（必須）
  psign:'' // Keyホットリンク防止の説明をご参照ください
});
```

#### 事例
[fileIDを切り替えて再生](http://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file.html)をクリックしてサンプルページに移動します。このページでマウスを右クリックして【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。

### イメージ機能
イメージ機能をアクティブ化すると、下図に示すとおり、ビデオ画面のイメージを反転させることができます。
![](https://main.qcloudimg.com/raw/d5886d7d550be72b608077f341299610.png)
右クリックでメニューのイメージオプションを開きます。
```
var player = TCPlayer('player-container-id', {
  fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
  appID: '', // VODアカウントのappIDを渡してください（必須）
  plugins: {
    ContextMenu: {
      mirror: true
    }
  }
});
```

#### 事例
[イメージ機能](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-mirror.html)をクリックしてサンプルページに移動します。このページでマウスを右クリックして【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。

>!ブラウザがビデオ再生をハイジャックする場合は，この機能を使用することができません。

### プログレスバーの表示
サーバーAPIを介してビデオにドット情報を追加するには、次の図に示すように、プレーヤーのプログレスバーの表示を有効にします。
![](https://main.qcloudimg.com/raw/70d880065adce22cb64270f4999558f8.png)

プレーヤーの起動方法：
```
var player = TCPlayer('player-container-id', {
  fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
  appID: '', // VODアカウントのappIDを渡してください（必須）
  plugins: {
    ProgressMarker: true
  }
});
```

#### 事例
[プログレスバーの表示](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-progress-marker.html)をクリックしてサンプルページに移動します。このページでマウスを右クリックして【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。

>!
>- この機能はデスクトップブラウザのみをサポートしています。
>- ブラウザがビデオ再生をハイジャックする場合は、この機能を使用することができません。

### HLSアダプティブビットレート再生
- HLS仕様のMaster Playlistは、ネットワーク速度のアダプティブビットレートに基づき再生することができます、ビデオのダウンロード中にネットワーク速度が高ビットレートのTSセグメントのダウンロード条件を満たす場合は、プレーヤーが高ビットレートのTSセグメントの再生に切り替え、満たさない場合は、低ビットレートのTSセグメントを再生します。モバイル端末とデスクトップの大部分のブラウザはこの特性をサポートしています。
- HLS Master Playlistを再生する場合、プレーヤーの解像度選択機能は、下図に示すとおり、特定のビットレートの選択か、またはネットワーク速度に応じた自動選択に変更されます。
![](https://main.qcloudimg.com/raw/339d7dfb3a4d247deb70460edac35a0e.png)

>!
>- 自動切り替えロジックは、アダプティブビットレート再生のすべての端末にデフォルトで採用されています。 
>- 一部のブラウザは対応するインターフェースを提供しておらず、MSEをサポートしていないことから、これらのブラウザでは特定の解像度を手動選択することも、解像度切り替えオプションを表示することもできません。
>- Flash再生モードは特定のビットレートの手動選択をサポートしていません。

#### 事例
[HLS Master Playlist](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-hls-masterplaylist.html)をクリックしてサンプルページに移動します。このページでマウスを右クリックして【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。

### Refererホットリンク防止
有効にする手順については、[Refererホットリンク防止](https://intl.cloud.tencent.com/document/product/266/33985)をご参照ください。プレーヤーを初期化するには次のパラメータを追加する必要があります。
```
var player = TCPlayer('player-container-id', {
     fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
     appID: '', // VODアカウントのappIDを渡してください（必須）
     flash:{
         swf: '//[Tencent Cloud隔離ドメイン名]/vod-player/[appID]/[fileID]/tcplayer/player.swf' //swfファイルアドレス（必須）
     }
   });
```
swf URLを渡す必要があります。ブラウザがFlash再生を使用する場合は、このアドレスからFlashプレーヤーを取得できます。Flashプレーヤーがビデオリクエストを開始すると、リクエストされたRefererはこのURLまたはページのURLを追加します。

>?
>- プレーヤーがFlashモードでビデオリクエストが開始されたRefererは、ChromeブラウザがページのURLを追加する状況とは異なり、IE、Firefoxブラウザにswf URLを追加します。
>- player.swfファイルをダウンロードした後、CDNサーバーに保存し、swfパラメータをCDNサーバーパスに渡すこともできます。
>- Tencent Cloudが提供する隔離ドメイン名はユーザー固有のドメイン名で、1つのappIDに1つのドメイン名が対応します。通常の形式は`[appID].vod2.myqcloud.com`です。
>- プレーヤーswfURLのドメイン名をホワイトリストに追加する必要があります。Flashモードで再生することができるのはRefererホットリンク防止が有効化されているビデオだけです。
>- プレーヤーのFlash swfファイルは、デフォルトでドメイン名`imgcache.qq.com`に保存されています。自身のサーバーにデプロイしたい場合は、[swfファイルアドレス](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf)からダウンロードしてデプロイすることができます。
>- ドメイン名制限エリアでは、必要なプレーヤーのFlash swfファイルは、デフォルトでドメイン名`cloudcache.tencent-cloud.com`に保存されます。
>- iiframeはプレーヤーページに埋め込まれており、ビデオリクエストのRefererはiframesrcを追加します。

### 解像度切り替えプロンプト
解像度切り替えプロンプトスイッチをオンにすると、次のプロンプトを追加することができます。
![](https://main.qcloudimg.com/raw/0d5559bd07681929fd45ce0b8a2353e9.png)

プレーヤーを初期化するには次のパラメータを追加する必要があります。
```
var tcplayer = TCPlayer('player-container-id', { // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
    fileID: '', // 再生したいビデオのfileIDを渡してください 必須
    appID: '', // VODアカウントのappIDを渡してください 必須
    plugins: {
      ContextMenu: {
        levelSwitch: {
          open: true, // 切り替えプロンプトの起動
          // switchingText: '現在、切り替え中'、 // 切り替え開始時のテキスト
          // switchedText: '切り替えに成功しました'、 // 切り替え成功時のテキスト
          // switchErrorText: '切り替えに失敗しました'、 // 切り替え失敗時のテキスト
        }
      }
    }
  });

```


### Keyホットリンク防止
有効にする手順については、[Keyホットリンク防止](https://intl.cloud.tencent.com/document/product/266/33986)をご参照ください。プレーヤーを初期化するには次のパラメータを追加する必要があります。
```
var player = TCPlayer('player-container-id', {
     fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
     appID: '', // VODアカウントのappIDを渡してください（必須）
     psign:''
   });
```
パラメータpsign、つまりSuper Player署名の具体的な定義については、[Super Player署名](https://intl.cloud.tencent.com/document/product/266/38099)をご参照ください。

>!Refererホットリンク防止を同時に有効にする場合は、Refererホットリンク防止設定のサンプルコードをもとにパラメータを追加します。

### プレビュー機能
プレビュー機能を使用する場合は、まずKeyホットリンク防止を有効にする必要があります。有効にする手順については、[Keyホットリンク防止](https://intl.cloud.tencent.com/document/product/266/33986)をご参照ください。プレーヤーを初期化するには次のパラメータを追加する必要があります。
```
var player = TCPlayer('player-container-id', {
  fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
  appID: '', // VODアカウントのappIDを渡してください（必須）
  psign:''
});
```
パラメータpsign、つまりSuper Player署名の具体的な定義については、[Super Player署名](https://intl.cloud.tencent.com/document/product/266/38099)をご参照ください。

>!
>- プレーヤーが再生するビデオ時間はexperパラメータが指定する時間であり、以前のプレーヤー側が制御する再生時間のプレビュー機能とは異なりますので、プレーヤーは完全なビデオを取得することができません。
>- プレビュー時間はビデオのキーフレームに基づきトリミングされ、実際にキャプチャされるプレビュー時間は設定値より少なくなる可能性があります。
>- プレビューを有効にした後もプレーヤーはビデオの元の時間を表示します（ChromeとFirefoxでHLS形式のプレビュービデオを再生する場合はプレビュー時間が表示されます）。

### HLS暗号化再生
再生ページはhls.jsをロードする必要があり、再生サンプルコードは次のとおりです。
```
var player = TCPlayer('player-container-id', {
     fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
     appID: '' // VODアカウントのappIDを渡してください（必須）
     psign:''
   });
```
パラメータpsign、つまりSuper Player署名の具体的な定義については、[Super Player署名](https://intl.cloud.tencent.com/document/product/266/38099)をご参照ください。

>!
>- 再生ページまたはFlash swf URLが復号キーサーバーのドメイン名と一致しない場合は、FlashとJavaScriptがクロスドメインで復号キーを取得できるよう、Keyサーバーはcorssdomain.xmlとCORS（「クロスドメインでのリソースの共有」、Cross-origin resource sharing）をデプロイする必要があります。
>- crossdomain.xmlにswf URLのドメイン名を設定し、かつxmlファイルはKeyサーバーのルートディレクトリに設定する必要があります。
>- プレーヤーのFlash swfファイルは、デフォルトでドメイン名`imgcache.qq.com`に保存されています。自身のサーバーにデプロイしたい場合は、[swfファイルアドレス](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf)からダウンロードしてデプロイすることができます。
>- ドメイン名制限エリアでは、必要なプレーヤーのFlash swfファイルは、デフォルトでドメイン名`cloudcache.tencent-cloud.com`に保存されます。
>- ビデオは1回のみ暗号化することができ、複数回暗号化することはできません。ビデオ暗号化ドキュメントの操作に厳密に従ってください。
>- 復号キーの正確な長さは16文字であり、冒頭と末尾を空白にすることはできません。

### ビデオ統計情報
右クリックしてビデオ統計パネルを開けば、下図に示すように、ビデオのリアルタイム情報を表示することができます。
![](https://main.qcloudimg.com/raw/77d6e949cb3a5cfb28bed86a7dea980e.png)
右クリックでメニューを開き、ビデオ統計情報オプションを開きます。
```
var player = TCPlayer('player-container-id', {
  fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
  appID: '', // VODアカウントのappIDを渡してください（必須）
  plugins: {
    ContextMenu: {
      statistic: true
    }
  }
});
```

#### 事例
[ビデオ統計情報](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file-statistic.html) をクリックしてサンプルページに移動します。このページでマウスを右クリックして【ウェブページソースコードを表示する】を選択すれば、サンプルソースコードを表示することができます。

>!
>- この機能はデスクトップブラウザのみをサポートしています。
>- ブラウザがビデオ再生をハイジャックする場合は、この機能を使用することができません。

### カスタムプロンプトテキスト
カスタムプロンプトテキストが必要な場合は、初期化パラメータlanguagesを介して指定のプロンプトテキストを設定します。サンプルコードは次のとおりです。

```
var player = TCPlayer('player-container-id', {
  fileID: '', // 再生したいビデオのfileIDを渡してください（必須）
  appID: '', // VODアカウントのappIDを渡してください（必須）
  languages:{
    'zh-cn':{
      'AppID is not exist, Please check if the AppID is correct.': 'appIDの入力に誤りがないかどうかを確認してください'
    }
  }
});
```

エラーコード対応テキストリスト：

| 名称 | 説明                                           ||
|------|----------------------------------------------|-------------------------|
| -1   | No video has been loaded.                    | プレーヤーは有効なビデオアドレスを検出できませんでした。 |
| -2   | Could not download the video.                | ビデオデータの取得がタイムアウトしました。 |
| 1    | You aborted the media playback.              | ビデオデータのロードプロセスが中断されました。 |
| 2    | A network error caused the media download to fail part-way. | ネットワークの問題でビデオのロードに失敗しました。 |
| 3    | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | ビデオのデコード時にエラーが発生しました。 |
| 4    | The media could not be loaded, either because the server or network failed or because the format is not supported. |形式がサポートされていないか、サーバーまたはネットワークの問題で、ビデオをロードできません。 |
| 5    | The media is encrypted and we do not have the keys to decrypt it.   | ビデオ復号時にエラーが発生しました。 |
| 10   | Request timed out.                          | VODメディアデータインターフェースのリクエストがタイムアウトしました。 |
| 11   | Server is not respond.                      | VODメディアデータインターフェースからデータが返されません。 |
| 12   | Server respond error data.                  | VODメディアデータインターフェースから異常なデータが返されました。 |
| 13   | No video transcoding information found.     | プレーヤーは現在のプレーヤーで再生できるビデオデータを検出できませんでした。このビデオに対するトランスコード操作を実施してください。|
| 14   | A network error caused the media download to fail part-way.   | ネットワークエラーのため、ビデオのダウンロードに失敗しました。 |
| 15   | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | ビデオファイルの破損、またはこのビデオがブラウザのサポートしていない機能を使用しているため、再生を終了します。 |
| 16   | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | ビデオファイルの破損、またはこのビデオがブラウザのサポートしていない機能を使用しているため、再生を終了します。 |
| 17   | Rise an internal exception when playing HLS.| HLS再生時に内部異常が発生しました。 |
| 500  | Server failed.                              | メディアサーバーエラーです。 |
| 1001 | The media file does not exist. Please check if the fileID is correct. | メディアファイルが存在しません。 fileIDに誤りがないかどうかチェックしてください。 |
| 1002 | The trial duration is illegal. The trial duration must be within the video duration. | プレビュー時間が不正です。プレビュー時間はビデオ時間の範囲内にする必要があります。 |
| 1003 | Param pcfg is not unique.                   | pcfgが一意ではありません。 |
| 1004 | The license has expired. Please check whether the expiration time setting is reasonable. | licenseの有効期限が切れています。有効期限の設定が合理的かどうかをチェックしてください。 |
| 1005 | Did not find an adaptive stream that can be played. | 再生できるアダプティブビットレートストリーミングが見つかりません。 |
| 1006 | Invalid request format, please check the request format. | リクエストフォーマットが不正です。リクエストフォーマットをチェックしてください。 |
| 1007 | AppID is not exist, Please check if the AppID is correct. |AppIDが存在しません。AppIDに誤りがないかどうかチェックしてください。 |
| 1008 | Without anti-leech information.             | ホットリンク防止テストが追加されていません。 |
| 1009 | psign check failed.                         | 再生パラメータpsignの検証に失敗しました。 |
| 1010 | Other errors.                               | その他のエラー。 |
| 2001 | Internal error.                             | 内部エラー。 |
| 10008| The media file does not exist. Please check if the fileID is correct. | メディアファイルが存在しません。fileIDに誤りがないかどうかチェックしてください。 |

## ログの更新
TCPlayerは常に更新され、改善されています。以下にリリースされたTCPlayerの主なバージョンを紹介します。

| 日時             | バージョン   | 更新内容|
|-----------------|--------- |-------------------------------------------- |
| 2020.7.10       |   4.1    |   1. デフォルトのhls.jsバージョンを0.13.2に変更しました。<br> 2. Keyホットリンク防止機能をサポートしています。 <br>3. その他既知の問題を修正しました。 |
| 2020.6.17       |   4.0    |   1. プレビュービデオ時間が元の時間の表示を維持するように修正しました。<br>2. バックエンドの解像度設定を有効にしました。 <br>3. その他既知の問題を修正しました。 |