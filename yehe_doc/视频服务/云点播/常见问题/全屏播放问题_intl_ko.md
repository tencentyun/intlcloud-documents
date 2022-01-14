
### 기기의 전체 화면과 웹 페이지 전체 화면을 구별하는 방법은 무엇입니까?
- 기기 전체 화면: 기기 화면 범위 내의 전체 화면 모드입니다. 이 모드에서는 기기 화면에 동영상 콘텐츠만 표시되고 주소 표시줄과 같은 브라우저 요소는 표시되지 않습니다. 이 모드를 사용하려면 브라우저에서 해당 API 지원을 제공해야 합니다. 기기 전체 화면을 지원하는 API에는 Fullscreen 및 webkitEnterFullScreen의 두 가지가 있습니다. 전자의 경우 기기 전체 화면 모드에서도 HTML과 CSS로 구성된 플레이어 인터페이스가 계속 표시됩니다. 후자는 비디오 태그에만 적용할 수 있으며 일반적으로 전자가 모바일 기기에서 지원되지 않을 때 사용됩니다. 후자의 전체 화면 모드 플레이어 인터페이스는 시스템의 기본 인터페이스입니다.
- 웹 페이지 전체 화면: 웹 페이지 표시 영역 내의 전체 화면 모드입니다. 이 모드에서는 주소 표시줄과 같은 브라우저 요소가 표시됩니다. 일반적으로 이 모드는 브라우저가 시스템 전체 화면을 지원하지 않을 때 전체 화면 효과를 얻는 방법입니다. 따라서 의사 전체 화면이라고도 합니다. CSS로 구현됩니다.

VOD의 Web 플레이어는 기기 전체 화면 위주로, 웹 페이지 전체 화면을 보조로 하는 전체 화면 방식을 사용합니다. 전체 화면 모드의 우선 순위는 Fullscreen API > webkitEnterFullScreen > 웹 페이지 전체 화면입니다.

Flash가 브라우저에 의해 점차 제한됨에 따라 VOD Web 플레이어는 HTML5 표준으로 개발되었으며, Flash 사용을 줄였습니다. 일부 레거시 브라우저에서는 전체 화면 기능의 사용이 제한됩니다. 레거시 VOD 플레이어 1.0은 Flash를 사용하여 개발되었으며 Flash 플러그 인으로 기기 전체 화면을 구현했습니다. Fullscreen API를 지원하지 않는 브라우저의 전체 화면 모드의 경우 기존 VOD 플레이어 1.0만 사용할 수 있습니다.

현재 알려진 전체 화면 지원 현황은 다음과 같습니다.

- X5 커널(Android의 WeChat, 모바일 QQ 및 QQ 브라우저 포함): Fullscreen API는 지원되지 않으며 webkitEnterFullScreen은 지원됩니다. 전체 화면 모드에서는 X5 커널이 있는 기기 전체 화면이 표시됩니다.
- Android의 Chrome: Fullscreen API가 지원됩니다. 전체 화면 모드에서는 Tencent Cloud 플레이어 UI가 있는 기기 전체 화면이 표시됩니다.
- iOS(WeChat, Mobile QQ, Safari 포함): Fullscreen API는 지원되지 않으며 webkitEnterFullScreen은 지원됩니다. 전체 화면 모드에서는 iOS 시스템 UI가 있는 기기 전체 화면이 표시됩니다.
- IE 8/9/10: Fullscreen API 및 webkitEnterFullScreen이 지원되지 않습니다. 전체 화면 모드에서 웹 페이지 전체 화면이 표시됩니다.
- 데스크톱 WeChat 브라우저: Fullscreen API 및 webkitEnterFullScreen이 지원되지 않습니다. 전체 화면 모드에서는 웹 페이지 전체 화면이 표시됩니다(macOS의 WeChat 브라우저는 현재 전체 화면 모드를 지원하지 않습니다).
- 기타 최신 데스크톱 브라우저: 일반적으로 Fullscreen API가 지원됩니다. 전체 화면 모드에서는 Tencent Cloud 플레이어 UI가 있는 기기 전체 화면이 표시됩니다.

<span id = "p1"></span>
### 동영상 재생 시 전체 화면 모드 강제 활성화 문제를 해결하는 방법은 무엇입니까?
페이지 내(전체 화면이 아닌) 재생을 구현하려면 기본적으로 Tencent Cloud 플레이어의 video 태그에 playsinline 및 webkit-playsinline 속성을 추가해야 합니다. iOS 10+는 playsinline 속성을 인식하지만 그 이전 iOS 버전은 webkit-playsinline 속성을 인식합니다.

테스트 결과 iOS Safari에서 페이지 내(inline) 재생이 지원되는 것으로 나타났습니다. Android는 webkit-playsinline을 인식하지만 Android의 개방성으로 인해 사용자 정의 브라우저가 많기 때문에 이러한 속성이 적용되지 않을 수 있습니다. 예를 들어, TBS 커널이 있는 브라우저(WeChat, Mobile QQ 및 QQ Browser를 포함하되 이에 국한되지 않음)에서 시스템이 강제로 전체 화면 모드로 재생하지 못하도록 하려면 동일 계층 플레이어 속성([통합 문서](https://x5.tencent.com/tbs/guide/video.html), [사용 설명](https://x5.tencent.com/tbs/guide/web/x5-video.html))을 사용해야 할 수 있습니다.

문제가 지속되면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하시기 바랍니다.


### 동영상 재생 시 전체 화면 모드 기본 활성화 문제를 해결하는 방법은 무엇입니까?
[동영상 재생 시 전체 화면 모드 강제 활성화 문제](#p1)와 동일하므로 해결 방법을 참고하십시오.

### iOS Hybrid App의 WebView에서 기본적으로 전체 화면 모드로 재생되는 문제를 해결하는 방법은 무엇입니까?
WebView 매개변수 allowInlineMediaPlayback을 YES로 설정하여 인라인 동영상 재생을 허용합니다. 즉, WebView/UiWebView가 강제로 전체 화면 모드로 동영상을 재생하는 것을 차단합니다.

### iframe에서 플레이어 전체 화면 모드 활성화 불가 문제를 해결하는 방법은 무엇입니까?
iframe 태그에서 allowfullscreen 속성을 설정하십시오. 샘플 코드는 다음과 같습니다.
```
<iframe allowfullscreen src="" frameborder="0" scrolling="no" width="100%" height="270"></iframe>
```

### IE 8/9/10에서 전체 화면 모드 활성화 불가 문제를 해결하는 방법은 무엇입니까?
Full screen API를 지원하지 않는 기존 브라우저에서 VOD 플레이어는 CSS를 사용하여 웹 페이지 전체 화면 모드를 구현합니다. 브라우저의 전체 화면 모드(일반적으로 ‘F11’ 키)를 사용하여 기기 전체 화면 효과를 얻을 수 있습니다. 플레이어의 페이지 내 전체 화면 스타일이 페이지의 CSS에 의해 제한되지 않도록 해야 합니다. 예를 들어 부모 컨테이너 `overflow:hidden`은 브라우저에 대해 설정되어서는 안 됩니다.

iframe을 사용하는 경우 플레이어는 iframe 외부에서 CSS 스타일을 수정할 수 없으며 외부 페이지에서 스크립트 및 스타일 지원을 제공해야 합니다. 일반적으로 외부 페이지는 웹 페이지 전체 화면을 구현하기 위해 크로스 도메인 지원이 필요합니다. 따라서 iframe이 있는 플레이어는 사용하지 않는 것이 좋습니다.
>？ IE 8/9/10은 Full Screen API를 지원하지 않습니다. 따라서 이 API를 통해 기기 전체 화면 모드를 구현할 수 없습니다.
