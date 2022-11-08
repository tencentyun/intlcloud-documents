본문에서는 VOD 및 라이브 재생에 적합한 Web Player SDK(TCPlayer)에 대해 설명합니다. 이 SDK는 Web 애플리케이션과 빠르고 자유롭게 통합되어 비디오 재생 기능을 구현할 수 있습니다. Web Player SDK(TCPlayer)에는 기본적으로 일부 UI가 포함되어 있으므로 필요에 따라 사용할 수 있습니다.
## 개요
Web용 Player는 HTML5 `<video>` 태그와 Flash를 통해 비디오 재생을 구현합니다. 기본적으로 비디오 재생을 지원하지 않는 브라우저에서 비디오를 재생할 수 있도록 하여 플랫폼 간에 통합된 비디오 경험을 제공합니다. 또한 VOD 서비스를 통해 암호화된 일반 HLS 비디오의 링크 도용 방지 및 재생 기능을 제공합니다.


### 프로토콜 지원

<table>
<tr><th style="text-align:center">멀티미디어 프로토콜</th><th>용도</th><th>URL 형식</th><th>PC 브라우저</th><th>모바일 브라우저</th>
</tr>
<tr>
<td style="text-align:center">MP3</td>
<td>오디오</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.mp3</code></td>
<td>지원</td>
<td>지원</td>
</tr>
<tr>
<td style="text-align:center">MP4</td>
<td>VOD</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.mp4</code></td>
<td>지원</td>
<td>지원</td>
</tr>
<tr>
<td rowspan=2 style="text-align:center">HLS<br>(M3U8)</td>
<td>라이브 방송</td>
<td><code>http://xxx.liveplay.myqcloud.com/xxx.m3u8</code></td>
<td>지원</td>
<td>지원</td>
</tr><tr>
<td>VOD</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.m3u8</code></td>
<td>지원</td>
<td>지원</td>
</tr><tr>
<td rowspan=2 style="text-align:center">FLV</td>
<td>라이브 방송</td>
<td><code>http://xxx.liveplay.myqcloud.com/xxx.flv</code></td>
<td>지원</td>
<td>일부 지원</td>
</tr><tr>
<td>VOD</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.flv</code></td>
<td>지원</td>
<td>일부 지원</td>
</tr>
<tr>
<td style="text-align:center">WebRTC</td>
<td>라이브 방송</td>
<td><code>webrtc://xxx.liveplay.myqcloud.com/live/xxx</code></td>
<td>지원</td>
<td>지원</td>
</tr>
</table>


<dx-alert infotype="explain" title="">
- H.264 비디오 코덱만 지원됩니다.
- 플레이어는 일반적인 브라우저와 호환되며 플레이어는 자동으로 플랫폼을 구분하고 최적의 재생 방식을 사용합니다.
- HLS 및 FLV 비디오는 일부 브라우저 환경에서 재생하려면 [Media Source Extensions](https://caniuse.com/?search=Media%20Source%20Extensions)에 종속해야 합니다.
- WebRTC를 지원하지 않는 브라우저 환경에서 플레이어에 전달된 WebRTC 주소는 미디어 재생을 더 잘 지원하기 위해 자동으로 프로토콜 전환을 수행합니다.
</dx-alert>

## 기능 지원

<Table>
  <tr>
    <th width="50px" style="text-align:center">기능\브라우저</th>
      <th width="50px" style="text-align:center">Chrome</th>
      <th width="50px" style="text-align:center">Firefox</th>
      <th width="50px" style="text-align:center">Edge</th>
      <th width="50px" style="text-align:center">QQ 브라우저</th>
      <th width="50px" style="text-align:center">Mac Safari</th>
      <th width="50px" style="text-align:center">iOS의 Safari</th>
      <th width="50px" style="text-align:center">WeChat</th>
      <th width="50px" style="text-align:center">Android의 Chrome</th>
      <th width="50px" style="text-align:center">IE 11</th>
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
         <td style="text-align:center">&#10003;</td>
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
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
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
    </tr>
    <tr>
         <td style="text-align:center">HLS 표준 암호화 재생</td>
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
         <td style="text-align:center">HLS 개인 암호화 재생</td>
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
    </tr>
    <tr>
         <td style="text-align:center">비디오 데이터 모니터링</td>
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
    </tr>
    <tr>
         <td style="text-align:center">사용자 정의 UI</td>
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
         <td style="text-align:center">댓글 자막</td>
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
         <td style="text-align:center">워터마크</td>
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
         <td style="text-align:center">비디오 리스트</td>
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
         <td style="text-align:center">약한 네트워크 프레임 추적</td>
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
- H.264 비디오 코덱만 지원됩니다.
- Windows 및 macOS에서 Chrome 및 Firefox가 지원됩니다.
- Chrome, Firefox, Edge 및 QQ 브라우저는 HLS 파일을 재생할 때 hls.js를 로딩해야 합니다.
- Referer 링크 도용 방지 기능은 HTTP 요청 헤더의 Referer 필드를 기반으로 구현됩니다. 일부 Android 브라우저에서 시작된 HTTP 요청에는 Referer 필드가 없습니다.
</dx-alert>

플레이어는 일반 브라우저와 호환되며 최적의 재생 구성표를 사용할 플랫폼을 자동으로 식별할 수 있습니다. 예를 들어 Chrome과 같은 최신 브라우저에서 비디오 재생을 위해 HTML5 기술을 사용하고 모바일 브라우저에서 HTML5 기술 또는 브라우저 커널 기능을 직접 사용하는 것이 좋습니다.


## 통합 가이드

다음 단계에 따라 웹페이지에 비디오 플레이어를 추가할 수 있습니다.

### 1단계: 페이지로 파일 가져오기

로컬 프로젝트에서 index.html 파일을 생성하고 플레이어 양식 파일과 스크립트 파일을 html 페이지로 가져옵니다.
```html
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/tcplayer.min.css" rel="stylesheet"/>
 <!--Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 Webrtc 비디오를 재생하려면 tcplayer.vx.x.x.min.js를 가져오기 전에 TXLivePlayer-x.x.x.min.js를 가져와야 합니다.-->
 <!--일부 브라우저 환경은 Webrtc를 지원하지 않으며 플레이어는 Webrtc 스트림 주소를 HLS 형식 주소로 자동 변환하므로 빠른 라이브 장면에서도 hls.min.x.xx.xm.js를 가져와야 합니다.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/TXLivePlayer-1.2.3.min.js"></script>
 <!--Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 HLS 프로토콜의 비디오를 재생하려면 tcplayer.vx.x.x.min.js를 가져오기 전에 hls.min.x.xx.xm.js를 가져와야 합니다.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/hls.min.1.1.5.js"></script>
 <!--Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 FLV 비디오를 재생하려면 tcplayer.vx.x.x.min.js를 가져오기 전에 flv.min.x.x.x.js를 가져와야 합니다.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/flv.min.1.6.3.js"></script>
  <!--Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 DASH 비디오를 재생하려면 tcplayer.vx.x.x.min.js를 가져오기 전에 dash.min.x.x.x.js를 가져와야 합니다.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/dash.all.min.4.4.1.js"></script>
 <!--플레이어 스크립트 파일-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/tcplayer.v4.5.4.min.js"></script>
```
플레이어 SDK를 사용할 때 리소스를 직접 배포하는 것이 좋습니다. [플레이어 리소스를 다운로드하려면 클릭](https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/release.zip)하십시오.
압축 해제 후 생성된 폴더를 배포합니다. 폴더의 디렉터리를 조정하지 마십시오. 그렇지 않으면 리소스 가져오기 예외가 발생할 수 있습니다.
배포 주소가 `aaa.xxx.ccc`인 경우 플레이어 스타일 및 스크립트 파일을 올바른 위치로 가져옵니다.
```html
 <link href="aaa.xxx.ccc/tcplayer.min.css" rel="stylesheet"/>
 <!--Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 HLS 비디오를 재생하려면 tcplayer.vx.x.x.min.js를 가져오기 전에 hls.min.x.xx.m.js를 가져와야 합니다.-->
 <script src="aaa.xxx.ccc/libs/hls.min.x.xx.m.js"></script>
 <!--플레이어 스크립트 파일-->
 <script src="aaa.xxx.ccc/tcplayer.vx.x.x.min.js"></script>
```

### 2단계: 플레이어 컨테이너 배치

플레이어를 표시할 페이지에 플레이어 컨테이너를 추가합니다. 예를 들어 index.html에 다음 코드를 추가합니다(컨테이너 ID와 너비 및 높이를 사용자 지정할 수 있음).
```html
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
>
>- 플레이어 컨테이너는 `<video>` 태그여야 합니다.
>- 예시의 `player-container-id`는 사용자 정의할 수 있는 플레이어 컨테이너의 ID입니다.
>- CSS를 통해 플레이어 컨테이너 영역의 크기를 설정하는 것이 좋습니다. CSS는 속성보다 유연하고 전체 화면에 맞추기 및 컨테이너 적응과 같은 효과를 얻을 수 있습니다.
>- 예시의 `preload` 속성은 페이지가 로딩된 후 비디오 로딩 여부를 지정하며 일반적으로 재생을 더 빨리 시작하기 위해 `auto`로 설정됩니다. 다른 옵션에는 `meta`(페이지가 로딩된 후에만 메타데이터를 로딩함) 및 `none`(페이지가 로딩된 후 비디오를 로딩하지 않음)이 있습니다. 시스템 제한으로 인해 동영상은 모바일 장치에 자동으로 로딩되지 않습니다.
>- `playsinline` 및 `webkit-playsinline` 속성은 표준 모바일 브라우저가 비디오 재생을 가로채지 않을 때 인라인 재생을 구현하는 데 사용됩니다. 여기에서는 참고용일 뿐이며 필요에 따라 사용할 수 있습니다.
>- `x5-playsinline` 속성을 설정하면 TBS 커널에서 X5 UI 플레이어가 사용됩니다.

### 3단계: 플레이어 초기화
페이지가 초기화된 후 비디오 리소스를 재생할 수 있습니다. Player는 VOD 및 라이브 방송 시나리오를 모두 지원하며 구체적인 재생 방법은 다음과 같습니다.
- VOD 재생: 플레이어는 FileID를 통해 Tencent Cloud VOD 미디어 리소스를 재생할 수 있으며, VOD의 구체적인 프로세스는 재생을 위해 [Player로 비디오 재생 > 통합 가이드](https://intl.cloud.tencent.com/document/product/266/38098)를 참고하십시오.
- 라이브 재생: 플레이어는 URL을 전달하고, 라이브 멀티미디어 스트림은 URL을 전달하기만 하면 재생을 위해 풀링할 수 있습니다. Tencent Cloud 라이브 스트리밍 URL 생성 방법에 대한 자세한 내용은 [라이브 스트리밍 URL 스플라이싱](https://intl.cloud.tencent.com/document/product/267/38393)을 참고하십시오.

<dx-tabs>
::: URL을 통해 재생(라이브 방송, VOD)
페이지가 초기화된 후 플레이어 인스턴스에서 메서드를 호출하여 메서드에 URL 주소를 전달합니다.
<dx-codeblock>
:::  javascript
var player = TCPlayer('player-container-id', {}); // player-container-id는 플레이어 컨테이너 ID로 html 상의 것과 일치해야 함
player.src(url); // 재생 url
:::
</dx-codeblock>

:::
::: FileID를 통해 재생(VOD)
index.html 페이지 초기화 코드에 다음 초기화 스크립트를 추가하여 준비 과정에서 얻은 fileID([**미디어 자산**](https://console.cloud.tencent.com/vod/media))의 비디오 ID와 appID(**계정 정보**>[**기본 정보**](https://console.cloud.tencent.com/developer)에서 볼 수 있음)를 전달합니다.

<dx-codeblock>
:::  javascript
var player = TCPlayer('player-container-id', { // player-container-id는 플레이어 컨테이너 ID로 html 상의 것과 일치해야 함
    fileID: '3701925921299637010', // 재생할 비디오의 fileID 입력(필수)
    appID: '1500005696' // VOD 계정의 appID 입력(필수)
  //비공개 암호화 재생을 위해서는 Player의 서명인 psign을 입력해야 합니다. 서명 및 생성 방법에 관한 내용은 다음 링크를 참고하십시오. https://www.tencentcloud.com/document/product/266/38099
  //psign:'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAwNTY5NiwiZmlsZUlkIjoiMzcwMTkyNTkyMTI5OTYzNzAxMCIsImN1cnJlbnRUaW1lU3RhbXAiOjE2MjY4NjAxNzYsImV4cGlyZVRpbWVTdGFtcCI6MjYyNjg1OTE3OSwicGNmZyI6InByaXZhdGUiLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI5YzkyYjBhYiJ9LCJkcm1MaWNlbnNlSW5mbyI6eyJleHBpcmVUaW1lU3RhbXAiOjI2MjY4NTkxNzksInN0cmljdE1vZGUiOjJ9fQ.Bo5K5ThInc4n8AlzIZQ-CP9a49M2mEr9-zQLH9ocQgI',
});
:::
</dx-codeblock>

>!소스 비디오가 브라우저에서 정상적으로 재생되지 않을 수 있기 때문에 재생할 비디오는 Tencent Cloud 트랜스 코딩 사용을 권장합니다.
:::
</dx-tabs>

### 4단계: 추가 기능
플레이어는 어댑티브 비트 레이트 스트리밍 자동 전환, 비디오 썸네일 미리보기 및 비디오 키 프레임 정보 추가와 같은 VOD의 서버 능력과 함께 고급 기능을 구현할 수 있습니다. 이러한 기능은 [긴 비디오 재생 솔루션](https://intl.cloud.tencent.com/document/product/266/44191)에 자세히 설명되어 있으며 문서를 참고하여 구현할 수 있습니다.

이 외에도 플레이어는 더 많은 기능을 제공하고 있으며, 기능 목록 및 사용 방법은 [기능 표시](https://tcplayer.vcube.tencent.com/) 페이지를 참고하십시오.
