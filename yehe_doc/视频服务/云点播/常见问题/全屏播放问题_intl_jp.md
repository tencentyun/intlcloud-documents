
### 全画面とWebページの全画面の違いは何ですか。
- 端末の全画面表示：表示パネル範囲内の全画面表示を指します。全画面表示では、ビデオ画像のみが端末画面に表示され、アドレスバーなどのUIコンポーネントは表示されません。端末の全画面表示では、ブラウザがAPIに対応する必要があります。端末の全画面表示をサポートするAPIは、Fullscreen APIとwebkitEnterFullScreenの2つがあります。Fullscreen APIを使用して全画面表示した場合、HTMLとCSSで構成されるプレーヤーパネルが表示されるのは特徴です。webkitEnterFullScreenはvideoタグにのみ使用でき、通常、モバイル端末がFullscreen APIをサポートしない場合に使用されます。このAPIを介して全画面表示に入った後、プレーヤーパネルはシステムに搭載されているUIになります。
- Webページの全画面表示：Webページの表示領域内の全画面表示を指します。Webページが全画面表示されても、アドレスバーなどのUIコンポーネントが表示されます。通常、この表示モードは、ブラウザが端末の全画面表示をサポートしていない場合に全画面表示を実装する方法です。そのため、疑似全画面表示とも呼ばれます。Webページの全画面表示はCSSによって実装されます。

VODのWebプレーヤーは、端末の全画面表示がメインであり、Webページの全画面表示が補足という全画面表示方式を採用しています。全画面表示の優先順位は、Fullscreen API > webkitEnterFullScreen > Webページの全画面表示の順となります。

Flashの使用はブラウザで徐々に制限されるようになっているため、VOD Webプレーヤーは、Flashの使用を減らしてHTML5標準で開発されています。一部の古いブラウザでは、全画面表示機能の使用が制限されています。旧バージョンのVODプレーヤー1.0は、Flashを使用して開発され、Flashプラグインを使用して端末の全画面表示を実現しました。Fullscreen APIをサポートしていないブラウザで全画面表示するには、旧バージョンのVODプレーヤー1.0のみを使用できます。

現在の全画面表示の対応状況は次のとおりです。

- X5カーネル（Android端末のWeChat、モバイルQQ、QQブラウザを含む）：Fullscreen APIをサポートしなく、webkitEnterFullScreenをサポートしています。全画面表示にすると、X5カーネルの端末の全画面表示モードに入ります。
- Android端末のChrome：Fullscreen APIがサポートされています。全画面表示モードでは、Tencent Cloud プレーヤーUIを備えた端末の全画面表示モードに入ります。
- iOS端末（WeChat、Mobile QQ、Safariを含む）：FullscreenAPIをサポートしなくwebkitEnterFullScreenをサポートしています。全画面表示モードでは、iOSシステムUIの端末の全画面表示モードに入ります。
- IE 8/9/10：Fullscreen APIもwebkitEnterFullScreenもサポートしません。全画面表示は、Webページの全画面表示となります。
- デスクトップWeChatブラウザ：FullscreenAPIもwebkitEnterFullScreenもサポートしません。全画面表示モードは、Webページの全画面表示となります（macOSのWeChatブラウザは現在、全画面表示モードをサポートしません）。
- その他のデスクトップブラウザ：Fullscreen APIは一般的にサポートします。全画面表示モードでは、Tencent Cloud プレーヤーUIを備えた端末の全画面表示モードに入ります。

[](id:p1)
### ビデオが再生されるときに強制的に全画面表示に入る問題を解決するにはどうすればよいですか。
ページ内（全画面表示ではない）の再生を実現するには、playsinlineとwebkit-playsinline属性をvideoタグに追加する必要があります。これにより、Tencent Cloudプレーヤーではデフォルトでplaysinlineとwebkit-playsinline属性を追加します。iOS 10以降はplaysinline属性を認識しますが、iOS 10以前のシステムはwebkit-playsinline属性を認識します。

テストの結果、iOSのSafariブラウザではページ埋め込み（インライン）再生を実現できます。Androidはwebkit-playsinlineを認識しますが、Androidのオープン性により、カスタムブラウザが多数あるため、これらの属性は有効にならない場合があります。たとえば、TBSカーネルを搭載したブラウザ（WeChat、モバイルQQ、QQブラウザを含むがこれらに限定されない）で、システムによりビデオ再生が強制的に全画面表示に入ることを防ぐために、同じレイヤーのプレーヤー属性（[Integration Documentation](https://x5.tencent.com/tbs/guide/video.html)、[使い方の説明](https://x5.tencent.com/tbs/guide/web/x5-video.html)）を使用する必要がある場合があります。

それでも問題が解決しない場合は、 [Submit Ticket](https://console.cloud.tencent.com/workorder/category) でお問い合わせください。


### デフォルトで全画面再生に入る問題を解決するにはどうすればよいですか？
[ビデオが再生されるときに強制的に全画面表示に入る]（#p1）の解決策をご参照ください。

### iOS Hybrid AppのWebViewでデフォルトで全画面再生に入る問題を解決するにはどうすればよいですか。
WebViewパラメータallowsInlineMediaPlayback = YESに設定して、インラインビデオ再生を許可します。つまり、WebView/UiWebView強制的に全画面ビデオ再生を禁止します。

### iframeでプレーヤーが全画面再生に入らない問題を解決するにはどうすればよいですか。
iframeタグでallowfullscreen属性を設定します。サンプルコードは以下のとおりです。
```
<iframe allowfullscreen src="" frameborder="0" scrolling="no" width="100%" height="270"></iframe>
```

### IE 8/9/10で全画面表示できない問題を解決するにはどうすればよいですか。
Full Screen API をサポートしていない古いブラウザでは、VODプレーヤーはCSSを使用してWebページの全画面表示を実装します。ブラウザの全画面表示（通常はF11を押す）を使用すると、端末の全画面表示を実現できます。プレーヤーのページ内の全画面スタイルがページ内のCSSによって制限されていないことを確認する必要があります。たとえば、プレーヤーの親コンテナ`overflow:hidden`を設定してはなりません。

iframeが使用されている場合、プレーヤーはiframeの外部のCSSスタイルを変更できず、外部ページはスクリプトとスタイルのサポートを提供する必要があります。通常、外部ページでは、Webページの全画面表示を実装するにはクロスドメインのサポートが必要です。そのため、iframeでプレーヤーを使用することはお勧めしません。
？>IE8/9/10はFull Screen APIをサポートしていないため、Full Screen APIを使用して端末の全画面表示を実装することはできません。
