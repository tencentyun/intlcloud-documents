본 문서는 비디오 재생을 구현하기 위해 유연한 API를 통해 자신의 Web 애플리케이션과 빠르게 통합될 수 있는 Web용 Tencent Cloud RT-Cube Superplayer(TCPlayer)에 대해 설명합니다. 이 문서는 JavaScript에 대한 기본 지식이 있는 개발자를 대상으로 합니다.

## 기능 개요
Web용 Tencent Cloud RT-Cube Superplayer는 HTML5 `<Video>` 태그와 Flash를 통해 비디오 재생을 구현합니다. 기본적으로 비디오 재생을 지원하지 않는 브라우저에서 비디오를 재생할 수 있도록 하여 플랫폼 간에 통합된 비디오 경험을 제공합니다. 또한 VOD 서비스를 통해 암호화된 일반 HLS 비디오의 링크 도용 방지 및 재생 기능을 제공합니다.

[](id:function)
### 기능 지원

<Table>
  <tr>
    <th width="50px" style="text-align:center">기능\브라우저</th>
      <th width="50px" style="text-align:center">Chrome</th>
      <th width="50px" style="text-align:center">Firefox</th>
      <th width="50px" style="text-align:center">Edge</th>
      <th width="50px" style="text-align:center">QQ 브라우저</th>
      <th width="50px" style="text-align:center">Mac Safari</th>
      <th width="50px" style="text-align:center">iOS의 Safari</th>
      <th width="50px" style="text-align:center">iOS의 WeChat/QQ</th>
      <th width="50px" style="text-align:center">Android의 Chrome</th>
      <th width="50px" style="text-align:center">Android의 WeChat/QQ</th>
      <th width="50px" style="text-align:center">모바일 QQ 브라우저</th>
      <th width="50px" style="text-align:center">IE 8, 9, 10, 11</th>
  </tr>
   <tr>
         <td style="text-align:center">MP4 포맷</td>
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
         <td style="text-align:center">HLS 포맷</td>
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
         <td style="text-align:center">플레이어 크기 설정</td>
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
         <td style="text-align:center">재생 재개 기능</td>
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
         <td style="text-align:center">배속 재생</td>
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
         <td style="text-align:center">썸네일 미리보기</td>
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
         <td style="text-align:center">- <br>(11지원)</td>
    </tr>
            <tr>
         <td style="text-align:center">재생을 위한 fileID 변경</td>
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
         <td style="text-align:center">미러링</td>
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
         <td style="text-align:center">진행 표시줄 표시</td>
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
         <td style="text-align:center">HLS 어댑티브 비트 레이트 재생</td>
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
         <td style="text-align:center">Referer 링크 도용 방지</td>
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
         <td style="text-align:center">해상도 전환 프롬프트</td>
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
         <td style="text-align:center">미리보기</td>
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
         <td style="text-align:center">암호화된 HLS 재생</td>
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
         <td style="text-align:center">비디오 통계</td>
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
         <td style="text-align:center">프롬프트 텍스트 사용자 정의</td>
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
>- H.264 비디오 인코더만 지원됩니다.
>- Windows 및 macOS에서 Chrome 및 Firefox가 지원됩니다.
>- Chrome, Firefox, Edge 및 QQ 브라우저는 HLS 파일을 재생할 때 hls.js를 로딩해야 합니다.
>- TBS 커널이 있는 Android용 WeChat 및 QQ는 기본적으로 MP4 및 HLS를 지원합니다.
>- Referer 링크 도용 방지 기능은 HTTP 요청 헤더의 Referer 필드를 기반으로 구현됩니다. 일부 Android 브라우저에서 시작된 HTTP 요청에는 Referer 필드가 없습니다.
>- Flash는 Internet Explorer 8에서 비디오를 재생하고 Internet Explorer 9/10/11에서 HLS 파일을 재생하는 데 필요합니다. 브라우저가 Flash를 지원하는지 확인하십시오.
>- Internet Explorer 8은 Windows 7에서만 지원됩니다.

플레이어는 일반 브라우저와 호환되며 최적의 재생 구성표를 사용할 플랫폼을 자동으로 식별할 수 있습니다. 예를 들어 Internet Explorer 11/10/9/8의 Flash 플레이어를 사용하여 브라우저가 HTML5를 통해 HLS 비디오를 재생할 수 있도록 하고, 가급적이면 Chrome과 같은 최신 브라우저에서 비디오 재생을 위해 HTML5 기술을 사용하고 모바일 브라우저에서 HTML5 기술 또는 브라우저 커널 기능을 직접 사용하는 것이 좋습니다.

### VOD 플랫폼의 트랜스 코딩 서비스
MP4 및 HLS(M3U8)는 현재 데스크톱 및 모바일 브라우저에서 가장 널리 지원되는 형식이므로 Tencent Cloud의 VOD 플랫폼은 결국 업로드된 동영상을 MP4 또는 HLS(M3U8) 형식으로 게시합니다.
[](id:preparation)
## 준비 작업

특정 프로세스는 재생을 위해 [Superplayer로 비디오 재생 - 통합 가이드](https://intl.cloud.tencent.com/document/product/266/38098)를 참고하십시오.

## Web 플레이어 초기화
준비가 완료되면 다음 단계에 따라 웹페이지에 비디오 플레이어를 추가할 수 있습니다.
[](id:step1)
### 1단계: 페이지로 파일 가져오기
플레이어 스타일 및 스크립트 파일을 올바른 위치로 가져옵니다.
```
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.min.css" rel="stylesheet">
 <!--Chrome 및 Firefox와 같은 브라우저에서 H5를 통해 HLS 비디오를 재생하려면 tcplayer.v4.2.min.js를 가져오기 전에 hls.min.0.13.2m.js를 가져와야 합니다.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/libs/hls.min.0.13.2m.js"></script>
 <!--플레이어 스크립트 파일-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.v4.2.1.min.js"></script>
```

플레이어 SDK를 사용할 때 리소스를 직접 배포하는 것이 좋습니다. [플레이어 리소스를 다운로드하려면 클릭](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/release.zip)하십시오.

압축 해제 후 생성된 폴더를 배포합니다. 폴더의 디렉터리를 조정하지 마십시오. 그렇지 않으면 리소스 가져오기 예외가 발생할 수 있습니다.

배포 주소가 `aaa.xxx.ccc`인 경우 플레이어 스타일 및 스크립트 파일을 올바른 위치로 가져옵니다.
```
 <link href="aaa.xxx.ccc/tcplayer.min.css" rel="stylesheet">
 <!--Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 HLS 비디오를 재생하려면 tcplayer.v4.2.1.min.js을 가져오기 전에 hls.min.0.13.2m.js를 가져와야 합니다.-->
 <script src="aaa.xxx.ccc/libs/hls.min.0.13.2m.js"></script>
 <!--플레이어 스크립트 파일-->
 <script src="aaa.xxx.ccc/tcplayer.v4.2.1.min.js"></script>
```

>?현재 VUE, React와 같은 프레임워크에 대한 모듈 로딩 방식은 지원하지 않습니다. 관련 script를 전역으로 가져와 플레이어를 사용할 수 있습니다.
[](id:step2)
### 2단계: 플레이어 컨테이너 배치
플레이어를 표시할 페이지에 플레이어 컨테이너를 추가합니다. 예를 들어 index.html에 다음 코드를 추가합니다(컨테이너 ID와 너비 및 높이를 사용자 지정할 수 있음).
```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
>- 플레이어 컨테이너는 `<Video>` 태그여야 합니다.
>- 예시의 `player-container-id`는 사용자 정의할 수 있는 플레이어 컨테이너의 ID입니다.
>- CSS를 통해 플레이어 컨테이너 영역의 크기를 설정하는 것이 좋습니다. CSS는 속성보다 유연하고 전체 화면에 맞추기 및 컨테이너 적응과 같은 효과를 얻을 수 있습니다.
>- 예시의 `preload` 속성은 페이지가 로딩된 후 비디오 로딩 여부를 지정하며 일반적으로 재생을 더 빨리 시작하기 위해 `auto`로 설정됩니다. 다른 옵션에는 `meta`(페이지가 로딩된 후에만 메타데이터를 로딩함) 및 `none`(페이지가 로딩된 후 비디오를 로딩하지 않음)이 있습니다. 시스템 제한으로 인해 동영상은 모바일 장치에 자동으로 로딩되지 않습니다.
>- `playsinline` 및 `webkit-playsinline` 속성은 표준 모바일 브라우저가 비디오 재생을 가로채지 않을 때 인라인 재생을 구현하는 데 사용됩니다. 여기에서는 참고용일 뿐이며 필요에 따라 사용할 수 있습니다.
>- `x5-playsinline` 속성을 설정하면 TBS 커널에서 X5 UI 플레이어가 사용됩니다.
[](id:step3)
### 3단계: 코드 초기화
페이지 초기화 코드에 다음 초기화 스크립트를 추가하여 준비 과정에서 얻은 fileID([[미디어 자산]](https://console.cloud.tencent.com/vod/media)의 비디오 ID)와 appID([계정 정보]>[[기본 정보]](https://console.cloud.tencent.com/developer)에서 볼 수 있음)를 전달합니다.
```
var player = TCPlayer('player-container-id', { // player-container-id는 플레이어 컨테이너 ID로 html 상의 것과 일치해야 함
    fileID: '5285890799710670616', // 재생할 비디오의 fileID 입력(필수)
    appID: '1400329073' // VOD 계정의 appID 입력(필수)
  });
```

>!소스 비디오가 브라우저에서 정상적으로 재생될 수 있다는 보장이 없기 때문에 재생할 비디오는 Tencent Cloud로 트랜스 코딩해야 합니다.
[](id:fullExample)
## 전체 예시 페이지
[예시 코드](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)를 클릭하여 예시 코드 페이지를 입력하고 페이지를 우클릭한 다음 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.
## 사용 방법
모범 사례 및 예방 조치를 포함한 플레이어의 일부 기능이 아래에 자세히 설명되어 있습니다.
### 플레이어 크기 설정
다음은 플레이어의 크기를 설정하는 몇 가지 방법입니다.

* ![](https://main.qcloudimg.com/raw/9576adc95470eee7ec036688e6cae8c7.png) width 및 height 속성은 태그에 대해 설정할 수 있습니다. 픽셀 단위(예: width = "100px" 또는 width = 100)여야 하며 백분율은 설정 불가합니다.
*  크기는 CSS를 통해 설정할 수 있습니다. px 및 백분율 값(예: width:"100px" 또는 width:"100%")을 지원합니다.

>?
>- 너비와 높이를 설정하지 않으면 플레이어는 비디오의 획득한 해상도로 디스플레이 크기를 설정합니다. 브라우저의 가시 영역 크기가 비디오 해상도보다 작은 경우 플레이어는 브라우저의 가시 영역을 초과하게 되므로 일반적으로 권장되지 않습니다. 가장 좋은 방법은 CSS를 통해 플레이어 크기를 설정하는 것입니다.
>- CSS를 능숙하게 사용하면 전체 화면에 맞추기 및 컨테이너 자체 맞춤 등 효과를 구현할 수 있습니다.

#### 예시
- [CSS로 크기 설정](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size.html)
- [웹 페이지의 가시 영역에 맞추기](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-full-viewport.html)
- [비례 적응 구현](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-adaptive.html)

예시 코드 페이지를 입력하고 해당 페이지를 우클릭한 후 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.

### 재생 재개 기능
재생 재개 기능을 활성화하기 위한 전제 조건은 비디오가 fileID를 통해 재생되는 것입니다. 플레이어는 고유한 fileID로만 비디오의 재생 시점을 기록할 수 있습니다. 재생이 완료되기 전에 페이지를 닫은 경우 동일한 브라우저에서 페이지를 다시 열 때 재생이 중단된 위치부터 재생을 재개할 수 있습니다. 다음 매개변수를 사용하여 재생 재개 기능을 활성화할 수 있습니다.

```
var player = TCPlayer('player-container-id', {
    fileID: '', // 재생할 비디오의 fileID 전달(필수)
    appID: '', // VOD 계정의 appID 전달(필수)
    plugins:{
        ContinuePlay: { // 재생 재개 기능 활성화
          // auto: true, //[옵션] 비디오 재생 후 자동 재개 여부
          // text: 'You left off at', // [옵션] 프롬프트 텍스트
          // btnText: 'Resume' // [옵션] 버튼 텍스트
        },
      }
  });
```



#### 예시
[재생 재개 기능](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-continue-play.html)을 클릭하여 예시 코드 페이지를 입력하고 페이지를 우클릭한 다음 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.
>!
> - 이 기능은 Tencent Cloud에서 트랜스 코딩되어 fileID 및 appID를 통해 재생되는 동영상에만 사용할 수 있습니다.
> - 이 기능은 localStorage를 통해 재생 시점을 저장합니다. 브라우저가 이 기능을 지원해야 합니다.
> - 이 기능은 하이재킹된 브라우저에서 재생할 수 없습니다.
> - 이 기능은 플랫폼/브라우저 간에 상호 운용할 수 없습니다. 예를 들어 사용자가 PC 브라우저에서 중단한 경우 모바일 브라우저나 다른 PC 브라우저에서 재생을 재개할 수 없습니다. 이를 구현하려면 자체적으로 추가 API를 개발해야 합니다.

### 배속 재생
브라우저에서 지원하는 경우 플레이어에 대해 배속 재생이 기본적으로 활성화됩니다.

```
var player = TCPlayer('player-container-id', {
  fileID: '', // 재생할 비디오의 fileID 전달(필수)
  appID: '', // VOD 계정의 appID 전달(필수)
  playbackRates: [0.5, 1, 1.25, 1.5, 2] // HTML5에서만 사용할 수 있는 배속 재생 옵션을 설정합니다.
});
```

>!
>- 브라우저가 배속 재생을 지원하지 않는 경우 플레이어에 버튼이 표시되지 않습니다.
>- 이 기능을 비활성화해야 하는 경우 [개발자 가이드](https://intl.cloud.tencent.com/document/product/266/42095)를 참고하십시오.


### 썸네일 미리보기
VOD Superplayer는 썸네일 미리보기를 지원합니다. 이 기능을 활성화하는 방법에는 두 가지가 있습니다.
- 서버 API를 사용하여 동영상의 썸네일 및 VTT 파일을 생성합니다. 자세한 내용은 [화면 캡처 - 스프라이트 이미지](https://intl.cloud.tencent.com/document/product/266/33940)를 참고하십시오.
- 썸네일 및 VTT 파일을 직접 생성하고 두 파일의 URL을 플레이어에 전달합니다. 자세한 내용은 ‘썸네일 미리보기 - 썸네일 및 VTT 파일 전달’ 예시를 참고하십시오.



#### 예시
- [썸네일 미리보기 - 서버에서 생성](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail.html)
- [썸네일 미리보기 - 썸네일 및 VTT 파일 전달](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail-src.html)

예시 코드 페이지를 입력하고 해당 페이지를 우클릭한 후 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.
>!
>- 이 기능은 데스크톱 브라우저에서만 사용할 수 있습니다.
>- 이 기능은 브라우저 하이재킹 재생에 사용할 수 없습니다.
>- 생성된 썸네일이 많을수록 진행률 표시줄 미리보기가 더 정확하지만 로딩이 느려집니다. 원하는 균형을 찾아야 합니다.

### 재생을 위한 fileID 변경
객체의 loadVideoByID(args) 메소드를 인스턴스화하여 재생을 위해 비디오를 변경할 수 있습니다. 지원되는 매개변수는 다음과 같습니다.
```
player.loadVideoByID({
  fileID: '', // 재생할 비디오의 fileID 전달(필수)
  appID: '', // VOD 계정의 appID 전달(필수)
  psign:'' // Key 링크 도용 방지에 대한 설명을 참고하십시오.
});
```

#### 예시
[재생용 fileID 변경](http://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file.html)을 클릭하여 예시 코드 페이지를 입력하고 페이지를 우클릭한 다음 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.

### 미러링
미러링 기능을 활성화하여 비디오 화면을 뒤집을 수 있습니다.
우클릭 메뉴에 미러링 옵션 표시:

```
var player = TCPlayer('player-container-id', {
  fileID: '', // 재생할 비디오의 fileID 전달(필수)
  appID: '', // VOD 계정의 appID 전달(필수)
  plugins: {
    ContextMenu: {
      mirror: true
    }
  }
});
```

#### 예시
[미러링](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-mirror.html)을 클릭하여 예시 코드 페이지로 이동하고 페이지를 우클릭한 다음 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.

>!이 기능은 하이재킹된 브라우저에서 재생할 수 없습니다.

### 진행 표시줄 표시
서버 API를 통해 타임스탬프를 추가하여 플레이어에서 진행률 표시줄 표시를 활성화할 수 있습니다.


플레이어에서 활성화하는 방법:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // 재생할 비디오의 fileID 전달(필수)
  appID: '', // VOD 계정의 appID 전달(필수)
  plugins: {
    ProgressMarker: true
  }
});
```

#### 예시
[진행률 표시줄 표시](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-progress-marker.html)를 클릭하여 예시 코드 페이지로 이동하고 페이지를 우클릭한 다음 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.

>!
>- 이 기능은 데스크톱 브라우저에서만 사용할 수 있습니다.
>- 이 기능은 브라우저 하이재킹 재생에 사용할 수 없습니다.

### HLS 어댑티브 비트 레이트 재생
- HLS 사양의 Master Playlist는 네트워크 속도에 따른 어댑티브 비트 레이트로 재생할 수 있습니다. 비디오 다운로드 중에 네트워크 속도가 높은 비트 레이트로 TS 세그먼트를 다운로드할 만큼 충분히 높으면 플레이어는 TS 세그먼트를 재생합니다. 그렇지 않으면 낮은 비트 레이트로 TS 세그먼트를 재생합니다. 이 기능은 대부분의 모바일 및 데스크톱 브라우저에서 지원됩니다.
- HLS Master Playlist가 재생될 때 플레이어의 해상도 선택 기능은 네트워크 속도에 따라 지정된 비트 레이트 또는 자동 선택됩니다.


>!
>- 자동 전환 로직은 기본적으로 모든 장치에서 어댑티브 비트 레이트 재생에 사용됩니다. 
>- 특정 브라우저는 해당 API가 없거나 MSE를 지원하지 않기 때문에 수동 해상도 선택이 불가능하고 해상도 전환 옵션도 사용할 수 없습니다.
>- Flash 재생 모드에서는 수동 비트 레이트 선택이 지원되지 않습니다.

#### 예시
[HLS Master Playlist](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-hls-masterplaylist.html)을 클릭하여 예시 코드 페이지로 들어가고 페이지를 우클릭한 다음 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.

### Referer 링크 도용 방지
이 기능을 활성화하는 방법에 대한 자세한 지침은 [Referer 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33985)를 참고하십시오. 플레이어 초기화 중에 다음 매개변수를 추가해야 합니다.
```
var player = TCPlayer('player-container-id', {
     fileID: '', // 재생할 비디오의 fileID 전달(필수)
     appID: '', // VOD 계정의 appID 전달(필수)
     flash:{
         swf: '//[Tencent Cloud의 격리된 도메인 이름]/vod-player/[appID]/[fileID]/tcplayer/player.swf' //swf 파일 주소(필수)
     }
   });
```
swf URL을 전달해야 합니다. 브라우저가 재생을 위해 Flash를 사용하는 경우 Flash 플레이어는 이 주소에서 가져옵니다. Flash 플레이어가 비디오 요청을 시작하면 요청의 Referer가 이 URL 또는 페이지의 URL을 전달합니다.

>?
>- Flash 모드에서 플레이어가 시작한 비디오 요청의 Referer는 IE 및 Firefox의 swf URL 또는 Chrome의 페이지 URL을 전달합니다.
>- 또한 player.swf 파일을 CDN 서버로 다운로드하고 CDN 서버의 경로를 가리키는 swf 매개변수를 전달할 수 있습니다.
>- Tencent Cloud에서 제공하는 격리된 도메인 이름은 각 사용자에게만 제공되는 도메인 이름입니다. 하나의 appID는 하나의 도메인 이름에 해당하며 일반적으로 `[appID].vod2.myqcloud.com` 형식입니다.
>- Referer 링크 도용 방지가 활성화된 비디오를 Flash 모드에서 재생하려면 먼저 플레이어 swf URL의 도메인 이름을 얼로우리스트에 추가해야 합니다.
>- 플레이어의 Flash swf 파일은 기본적으로 `imgcache.qq.com` 도메인 이름으로 저장됩니다. 자체 서버에 배포해야 하는 경우 [swf 파일 주소](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf)에서 다운로드하여 직접 배포할 수 있습니다.
>- 비즈니스가 도메인 제한 지역에 있는 경우 기본적으로 Flash swf 파일을 `cloudcache.tencent-cloud.com` 도메인 이름으로 저장해야 합니다.
>- iframe이 플레이어 페이지에 포함된 경우 비디오 요청의 Referer는 iframe src를 가져옵니다.

### 해상도 전환 프롬프트


플레이어 초기화 중에 다음 매개변수를 추가해야 합니다.
```
var tcplayer = TCPlayer('player-container-id', { // player-container-id는 플레이어 컨테이너 ID이며 html과 동일해야 함
    fileID: '', // 재생할 비디오의 fileID 전달, 필수
    appID: '', // VOD 계정의 appID 전달, 필수
    plugins: {
      ContextMenu: {
        levelSwitch: {
          open: true, // 전환 프롬프트 활성화
          // switchingText: '다음으로 전환 중', // 전환 시작 시 텍스트
          // switchedText: '전환 성공', // 전환 성공 시 텍스트
          // switchErrorText: '전환 실패', // 전환 실패 시 텍스트
        }
      }
    }
  });

```


### Key 링크 도용 방지
이 기능을 활성화하는 방법에 대한 자세한 지침은 [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986)를 참고하십시오. 플레이어 초기화 중에 다음 매개변수를 추가해야 합니다.
```
var player = TCPlayer('player-container-id', {
     fileID: '', // 재생할 비디오의 fileID 전달(필수)
     appID: '', // VOD 계정의 appID 전달(필수)
     psign:''
   });
```
psign 매개변수는 Superplayer 서명입니다. 이에 대한 설명은 [Superplayer 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 참고하십시오.

>!Referer 링크 도용 방지도 활성화된 경우 Referer 링크 도용 방지 구성의 예시 코드에 매개변수를 추가하기만 하면 됩니다.

### 미리보기
미리보기 기능은 Key 링크 도용 방지 구성을 활성화한 후에만 사용할 수 있습니다. 활성화 방법에 대한 자세한 지침은 [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986)를 참고하십시오. 플레이어 초기화 중에 다음 매개변수를 추가해야 합니다.
```
var player = TCPlayer('player-container-id', {
  fileID: '', // 재생할 비디오의 fileID 전달(필수)
  appID: '', // VOD 계정의 appID 전달(필수)
  psign:''
});
```
psign 매개변수는 Superplayer 서명입니다. 이에 대한 설명은 [Superplayer 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 참고하십시오.

>!
>- 플레이어에서 비디오 재생 시간은 exper 매개변수로 지정된 길이입니다. 플레이어 측에서 재생 시간을 제어하는 다른 미리보기 기능과 달리 플레이어는 전체 비디오를 가져오지 못합니다.
>- 미리보기는 동영상 키프레임에 따라 동영상을 자르는 방식으로 작동하며 실제로 잘린 미리보기 동영상은 미리 구성된 미리보기 시간보다 짧을 수 있습니다.
>- 플레이어는 미리보기 기능이 활성화된 후에도 원래 비디오 재생 시간을 계속 표시합니다(미리보기 지속 시간은 Chrome 및 Firefox에서 HLS 비디오에 대해 표시됨).

### 암호화된 HLS 재생
재생 페이지는 hls.js를 로딩해야 하며 재생 예시 코드는 다음과 같습니다.
```
var player = TCPlayer('player-container-id', {
     fileID: '', // 재생할 비디오의 fileID 전달(필수)
     appID: '' // VOD 계정의 appID 전달(필수)
     psign:''
   });
```
psign 매개변수는 Superplayer 서명입니다. 이에 대한 설명은 [Superplayer 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 참고하십시오.

>!
>- 재생 페이지 또는 Flash swf의 URL이 암호 해독 키 서버와 다른 도메인 이름을 가진 경우, Key 서버가 crossdomain.xml 및 CORS(Cross-origin resource sharing)를 배포하여 Flash 및 JavaScript가 원본 간에 암호 해독 키를 얻을 수 있도록 해야 합니다.
>- swf URL의 도메인 이름은 Key 서버의 루트 디렉터리에 있어야 하는 crossdomain.xml에 구성됩니다.
>- 플레이어의 Flash swf 파일은 기본적으로 `imgcache.qq.com` 도메인 이름으로 저장됩니다. 자체 서버에 배포해야 하는 경우 [swf 파일 주소](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf)에서 다운로드하여 직접 배포할 수 있습니다.
>- 비즈니스가 도메인 제한 리전에 있는 경우 기본적으로 Flash swf 파일을 `cloudcache.tencent-cloud.com` 도메인 이름으로 저장해야 합니다.
>- 동영상은 한 번만 암호화할 수 있습니다. 비디오 암호화 문서의 단계를 엄격히 따르십시오.
>- 암호 해독 키는 16자를 포함해야 하며 공백 문자로 시작하거나 끝날 수 없습니다.

### 비디오 통계
우클릭하여 비디오 통계 패널을 열고 실시간 비디오 정보를 봅니다.

우클릭 메뉴에 비디오 통계 옵션 표시:

```
var player = TCPlayer('player-container-id', {
  fileID: '', // 재생할 비디오의 fileID 전달(필수)
  appID: '', // VOD 계정의 appID 전달(필수)
  plugins: {
    ContextMenu: {
      statistic: true
    }
  }
});
```

#### 예시
[비디오 통계](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file-statistic.html)를 클릭하여 예시 코드 페이지를 입력하고 페이지를 우클릭한 다음 [페이지 소스 코드 보기]를 선택하여 예시 소스 코드를 조회합니다.

>!
>- 이 기능은 데스크톱 브라우저에서만 사용할 수 있습니다.
>- 이 기능은 브라우저 하이재킹 재생에 사용할 수 없습니다.

### 프롬프트 텍스트 사용자 정의
프롬프트 텍스트를 사용자 정의하려면 초기화 매개변수 languages를 통해 설정합니다. 아래는 예시 코드입니다.

```
var player = TCPlayer('player-container-id', {
  fileID: '', // 재생할 비디오의 fileID 전달(필수)
  appID: '', // VOD 계정의 appID 전달(필수)
  languages:{
    'zh-cn':{
      'AppID is not exist, Please check if the AppID is correct.': 'appID가 제대로 입력되었는지 확인하십시오'
    }
  }
});
```

오류 코드의 해당 텍스트 프롬프트는 다음과 같습니다.

| 이름 | 설명                                           ||
|------|----------------------------------------------|-------------------------|
| -1   | No video has been loaded.                    | 플레이어가 사용 가능한 비디오 주소를 감지하지 못했습니다. |
| -2   | Could not download the video.                | 비디오 데이터 수집 시간이 초과되었습니다. |
| 1    | You aborted the media playback.              | 비디오 데이터 로딩이 중단되었습니다. |
| 2    | A network error caused the media download to fail part-way. | 네트워크 문제로 인해 비디오를 로딩하지 못했습니다. |
| 3    | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | 비디오를 디코딩하는 동안 오류가 발생했습니다. |
| 4    | The media could not be loaded, either because the server or network failed or because the format is not supported. | 지원되지 않는 형식 또는 서버/네트워크 문제로 인해 동영상을 로딩할 수 없습니다. |
| 5    | The media is encrypted and we do not have the keys to decrypt it.   | 동영상을 복호화하는 중에 오류가 발생했습니다. |
| 10   | Request timed out.                          | VOD 미디어 데이터 API 요청 시간이 초과되었습니다. |
| 11   | Server is not respond.                      | VOD 미디어 데이터 API가 데이터를 반환하지 않았습니다. |
| 12   | Server respond error data.                  | VOD 미디어 데이터 API가 예외 데이터를 반환했습니다. |
| 13   | No video transcoding information found.     | 플레이어가 현재 플레이어에서 재생할 수 있는 비디오 데이터를 감지하지 못했습니다. 동영상을 트랜스 코딩하십시오.|
| 14   | A network error caused the media download to fail part-way.   | 네트워크 문제로 인해 비디오를 다운로드하지 못했습니다. |
| 15   | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | 동영상 파일이 손상되었거나 동영상이 브라우저에서 지원하지 않는 기능을 사용하여 재생이 중단되었습니다. |
| 16   | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | 동영상 파일이 손상되었거나 동영상이 브라우저에서 지원하지 않는 기능을 사용하여 재생이 중단되었습니다. |
| 17   | Rise an internal exception when playing HLS.| HLS 비디오를 재생하는 동안 내부 예외가 발생했습니다. |
| 500  | Server failed.                              | 미디어 서버 오류가 발생했습니다. |
| 1001 | The media file does not exist. Please check if the fileID is correct. | 미디어 파일이 존재하지 않습니다. fileID가 올바른지 확인하십시오. |
| 1002 | The trial duration is illegal. The trial duration must be within the video duration. | 미리보기 시간이 잘못되었습니다. 미리보기 지속 시간은 비디오 지속 시간 내에 있어야 합니다. |
| 1003 | Param pcfg is not unique.                   | pcfg가 고유하지 않습니다. |
| 1004 | The license has expired. Please check whether the expiration time setting is reasonable. | license가 만료되었습니다. 만료 시간 설정이 합리적인지 확인하십시오. |
| 1005 | Did not find an adaptive stream that can be played. | 재생할 수 있는 어댑티브 비트 스트림을 찾을 수 없습니다. |
| 1006 | Invalid request format, please check the request format. | 잘못된 요청 형식입니다. 요청 형식을 확인하십시오. |
| 1007 | AppID is not exist, Please check if the AppID is correct. | AppID가 존재하지 않습니다. AppID가 맞는지 확인하십시오. |
| 1008 | Without anti-leech information.             | 링크 도용 방지 감지가 없습니다. |
| 1009 | psign check failed.                         | 재생 매개변수 psign을 확인하지 못했습니다. |
| 1010 | Other errors.                               | 다른 오류가 발생했습니다. |
| 2001 | Internal error.                             | 내부 오류가 발생했습니다. |
| 10008| The media file does not exist. Please check if the fileID is correct. | 미디어 파일이 존재하지 않습니다. fileID가 올바른지 확인하십시오. |

## 업데이트 로그
TCPlayer는 지속적으로 업데이트되고 최적화됩니다. 다음은 TCPlayer가 배포한 주요 버전입니다.

| 날짜             | 버전     | 업데이트|
|-----------------|--------- |-------------------------------------|
| 2020.7.10       |   4.1    |   1. 기본 hls.js 버전을 0.13.2로 변경했습니다.<br> 2. Key 링크 도용 방지에 대한 지원을 추가했습니다. <br>3. 기타 알려진 문제를 수정했습니다. |
| 2020.6.17       |   4.0    |   1. 동영상 미리보기 재생시간으로 원본 동영상 재생시간이 출력되던 현상이 수정되었습니다.<br>2. 백엔드 해상도 구성을 추가했습니다. <br>3. 기타 알려진 문제를 수정했습니다. |
