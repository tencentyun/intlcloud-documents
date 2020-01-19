
### How to distinguish between device full screen and webpage full screen?
- Device full screen: this refers to the full screen mode within the device screen range. In this mode, only the video content is displayed on the device screen, and browser elements such as address bar are invisible. This mode requires the browser to provide corresponding API support. There are two APIs that support device full screen: Fullscreen and webkitEnterFullScreen. With the former, after entering device full screen, the player interface composed of HTML and CSS is still visible. The latter can only be applied to the video tag and is usually used when the former is not supported by a mobile device. After entering full screen through the latter, the player interface is the device's native interface.
- Webpage full screen: this refers to the full screen mode within the webpage display area. In this mode, browser elements such as address bar are visible. Generally, this mode is a way to achieve a full screen effect when the browser does not support device full screen; therefore, it is also called pseudo full screen. It is implemented by CSS.

The web player of VOD uses a full screen scheme where device full screen is dominant and supplemented by webpage full screen. The priority of full screen mode is Fullscreen API > webkitEnterFullScreen > webpage full screen.

As Flash is gradually restricted by browsers, the VOD web player is developed in the HTML5 standard with reduced use of Flash. In some legacy browsers, the use of the full screen feature is restricted. The legacy VOD player 1.0 was developed by using Flash and achieved device full screen with the Flash plugin. For full screen mode in browsers that do not support the Fullscreen API, only the legacy VOD player 1.0 can be used.

Currently known full screen support is as follows:

- X5 kernel (including WeChat, Mobile QQ and QQ Browser on Android): webkitEnterFullScreen rather than Fullscreen API is supported. In full screen mode, the device full screen with the X5 kernel is displayed.
- Chrome on Android: Fullscreen API is supported. In full screen mode, the device full screen with the Tencent Cloud Player UI is displayed.
- iOS (including WeChat, Mobile QQ, and Safari): webkitEnterFullScreen rather than Fullscreen API is supported. In full screen mode, the device full screen with the iOS system UI is displayed.
- IE 8/9/10: neither Fullscreen API no webkitEnterFullScreen is supported. In full screen mode, the webpage full screen is displayed.
- Desktop WeChat Browser: neither Fullscreen API nor webkitEnterFullScreen is supported. In full screen mode, the webpage full screen is displayed. WeChat Browser on macOS currently does not support any full screen mode.
- Other modern desktop browsers: Fullscreen API is generally supported. In full screen mode, the device full screen with the Tencent Cloud Player UI is displayed.

<span id = "p1"></span>
### How to solve the problem with forced full screen mode after video playback is activated?
To achieve in-page (non-full screen) playback, the `playsinline` and `webkit-playsinline` attributes need to be added to the video tag, which is done by Tencent Cloud Player by default. iOS 10+ recognizes the `playsinline` attribute, while older iOS versions recognize the `webkit-playsinline` attribute.

Tests show that in-page (inline) playback can be implemented in Safari on iOS. Android recognizes `webkit-playsinline`, but due to the openness of Android, there are many custom browsers for which such attributes may not necessarily take effect. For example, in browsers with TBS kernel (including but not limited to WeChat, Mobile QQ, and QQ Browser), the same-layer player attributes may need to be used to prevent the system from forcing playback in full screen mode (for more information, please see the [Access Document](https://x5.tencent.com/tbs/guide/video.html) and [Uses Guide](https://x5.tencent.com/tbs/guide/web/x5-video.html)).

If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


### How to solve the problem where playback is in full screen mode by default?
This problem is caused in the same way as the problem of [forced full screen mode after video playback is activated](#p1) and can be solved similarly.

### How to solve the problem that playback is in full screen mode by default in the WebView of an iOS hybrid app?
Set the WebView parameter `allowsInlineMediaPlayback` to `YES` to allow inline video playback, i.e., forbidding WebView/UiWebView to force full-screen video playback.

### How to solve the problem that the player cannot enter full screen mode in iframe?
Set the `allowfullscreen` attribute in the `iframe` tag. Below is the sample code:
```
<iframe allowfullscreen src="" frameborder="0" scrolling="no" width="100%" height="270"></iframe>
```

### How to solve the problem that full screen cannot be entered in IE 8/9/10?
In legacy browsers that do not support the Fullscreen API, the VOD player uses CSS to implement the webpage full screen mode. With the aid of full screen mode of the browsers (generally by pressing F11), the device full screen effect can be achieved. It should be ensured that the in-page full screen style of the player is not restricted by CSS in the page; for example, the parent container `overflow:hidden` should not be set for the browser.

If iframe is used, the player cannot modify the CSS style outside the iframe, and the external page needs to provide script and style support. Generally, the external page requires cross-domain support to implement webpage full screen. Therefore, it is not recommended to use the player with iframe.
> IE 8/9/10 do not support the Fullscreen API; therefore, the device full screen mode cannot be implemented through this API.
