## 소개
본문은 TCToolkit SDK에 통합된 TCPlayer와 [CI(Cloud Infinite)](https://www.tencentcloud.com/document/product/1045/46980)의 풍부한 오디오/비디오 기능을 사용하여 웹 브라우저에서 COS에 저장된 비디오 파일을 재생하는 방법을 설명합니다.


## 통합 가이드
#### 1단계: 플레이어 양식 및 스크립트 파일을 페이지로 가져오기
```
<!--플레이어 양식 파일-->
<link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.min.css" rel="stylesheet">
<!--플레이어 스크립트 파일-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.0/tcplayer.v4.5.0.min.js"></script>
```
>?
>- 플레이어 SDK를 사용할 때 위의 정적 리소스를 직접 배포하는 것이 좋습니다. [플레이어 리소스를 다운로드하려면 여기 클릭](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/release.zip)하십시오.
>- 압축 해제 후 생성된 폴더를 배포합니다. 폴더의 디렉터리를 조정하지 마십시오. 그렇지 않으면 리소스 가져오기 예외가 발생할 수 있습니다.

#### 2단계: 플레이어 컨테이너 노드 설정
플레이어를 표시할 페이지에 플레이어 컨테이너를 추가합니다. 예를 들어 index.html에 다음 코드를 추가합니다(컨테이너 ID와 너비 및 높이를 사용자 지정할 수 있음).

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
> - 플레이어 컨테이너는 `<video>` 태그여야 합니다.
> - 예시의 `player-container-id`는 사용자 정의할 수 있는 플레이어 컨테이너의 ID입니다.
> - CSS를 통해 플레이어 컨테이너 영역의 크기를 설정하는 것이 좋습니다. CSS는 속성보다 유연하고 전체 화면에 맞추기 및 컨테이너 적응과 같은 효과를 얻을 수 있습니다.
> - 예시의 `preload` 속성은 페이지가 로딩된 후 비디오 로딩 여부를 지정하며 일반적으로 재생을 더 빨리 시작하기 위해 `auto`로 설정됩니다. 다른 옵션에는 `meta`(페이지가 로딩된 후에만 메타데이터를 로딩함) 및 `none`(페이지가 로딩된 후 비디오를 로딩하지 않음)이 있습니다. 시스템 제한으로 인해 동영상은 모바일 장치에 자동으로 로딩되지 않습니다.
> - `playsinline` 및 `webkit-playsinline` 속성은 표준 모바일 브라우저가 비디오 재생을 가로채지 않을 때 인라인 재생을 구현하는 데 사용됩니다. 여기에서는 참고용일 뿐이며 필요에 따라 사용할 수 있습니다.
> - `x5-playsinline` 속성을 설정하면 TBS 커널에서 X5 UI 플레이어가 사용됩니다.

#### 3단계: 비디오 파일 객체 주소 가져오기
1. [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309).
2. [동영상 파일 객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321).
3. `https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<비디오 형식>` 형식의 비디오 파일 객체 주소를 가져옵니다.

>?
> - Cross-Origin 액세스가 포함된 경우 [CORS 설정](https://intl.cloud.tencent.com/document/product/436/13318)에서 설명한 대로 버킷에 대한 CORS를 설정해야 합니다.
> - 버킷 권한이 비공개 읽기/쓰기인 경우 객체 주소에 서명이 있어야 합니다. 자세한 내용은 [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)를 참고하십시오.

#### 4단계: 플레이어 초기화 및 COS 동영상 파일 객체 URL 전달
```
var player = TCPlayer("player-container-id", {}); // player-container-id는 플레이어 컨테이너 ID로 html과 동일해야 합니다.
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"); // COS 비디오 객체 주소
```

## 기능 가이드
[](id:1)
### 다양한 형식의 비디오 파일 재생
1. COS 버킷에 있는 비디오 파일의 객체 주소를 가져옵니다.
>? 트랜스코딩되지 않은 비디오는 재생 중에 호환성 문제가 발생할 수 있으므로 재생을 위해 비디오를 트랜스코딩하는 것이 좋습니다. CI의 [Audio/Video Transcoding](https://intl.cloud.tencent.com/document/product/1045/49543) 기능을 사용하여 다양한 형식의 비디오 파일을 얻을 수 있습니다.
2. 다른 비디오 형식의 경우 다른 브라우저와의 호환성을 보장하기 위해 해당 종속성을 가져와야 합니다.
 - MP4: 다른 종속성을 가져올 필요가 없습니다.
 - HLS: Chrome 및 Firefox와 같은 최신 브라우저에서 HTML5를 통해 HLS 동영상을 재생하려면 tcplayer.min.js를 가져오기 전에 hls.min.js를 가져와야 합니다.
```
  <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/libs/hls.min.0.13.2m.js"></script>
```
 - FLV: Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 FLV 비디오를 재생하려면 tcplayer.min.js를 가져오기 전에 flv.min.js를 가져와야 합니다.
```
  <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/libs/flv.min.1.6.2.js"></script>
```
 - DASH: dash.all.min.js 파일을 가져와야 합니다.
```
  <script src="https://cos-video-1258344699.cos.ap-guangzhou.myqcloud.com/lib/dash.all.min.js"></script>
```
3. 플레이어를 초기화하고 객체 주소를 전달합니다.
```
var player = TCPlayer("player-container-id", {}); // player-container-id는 플레이어 컨테이너 ID로 html과 동일해야 합니다.
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"); // COS 비디오 주소
```

코드 샘플 가져오기:
- [MP4 재생을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/mp4.html)
- [FLV 재생을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/flv.html)
- [HLS 재생을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/m3u8.html)
- [DASH 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/dash.html)


[](id:2)
### PM3U8 비디오 재생
PM3U8은 개인 M3U8 비디오 파일을 나타냅니다. COS는 개인 M3U8 TS 리소스를 가져오기 위한 다운로드 권한 API를 제공합니다. 자세한 내용은 [Private M3U8 API](https://intl.cloud.tencent.com/document/product/436/47220)를 참고하십시오.
```
var player = TCPlayer("player-container-id", {
	poster: "https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600" // 개인 TS 리소스 URL에 대한 다운로드 자격 증명의 상대 유효 기간, 3600초
});
```

코드 샘플 가져오기:
- [PM3U8 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/pm3u8.html)

[](id:3)
### 썸네일 설정
1. COS 버킷에 있는 썸네일의 객체 주소를 가져옵니다.
>!CI의 [Intelligent Thumbnail](https://intl.cloud.tencent.com/document/product/1045/47740) 기능은 최적의 프레임을 추출하여 썸네일을 생성하여 비디오 콘텐츠를 더 매력적으로 만들 수 있습니다.
2. 썸네일을 설정합니다.
```
var player = TCPlayer("player-container-id", {
	poster: "https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.png"
});
```

코드 샘플 가져오기:
- [썸네일 구성 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/poster.html)

[](id:4)
### HLS 암호화 비디오 재생
CI는 동영상 콘텐츠의 보안을 확보하고 동영상의 무단 다운로드 및 배포를 방지하기 위해 개인이 읽을 수 있는 파일보다 안전한 HLS 동영상 콘텐츠를 암호화하는 기능을 제공합니다. 암호화된 비디오는 재생 액세스 권한이 없는 사용자에게 배포할 수 없습니다. 다운로드하더라도 여전히 암호화되어 악의적으로 재배포할 수 없습니다. 이렇게 하면 비디오 저작권이 침해되는 것을 방지할 수 있습니다.

작업 순서는 다음과 같습니다.
1. [HLS 암호화 비디오 재생](https://www.tencentcloud.com/document/product/436/48293)의 지침에 따라 암호화된 비디오를 생성합니다.
2. 플레이어를 초기화하고 비디오 객체 주소를 전달합니다.
```
var player = TCPlayer("player-container-id", {}); // player-container-id는 플레이어 컨테이너 ID로 html 상의 것과 일치해야 합니다.
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"); // hls 암호화된 비디오 주소
```

코드 샘플 가져오기:
- [HLS 암호화 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/m3u8.html)

[](id:5)
### 해상도 전환
CI의 [Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/1045/47745) 기능은 비디오를 트랜스코딩하고 출력을 위해 어댑티브 비트스트림으로 리먹스할 수 있으므로 다양한 네트워크 조건에서 비디오 콘텐츠를 빠르게 배포할 수 있습니다. 플레이어는 현재 대역폭을 기반으로 비디오를 재생하는 데 가장 적절한 비트레이트를 동적으로 선택할 수 있습니다.
작업 순서는 다음과 같습니다.
1. CI의 [어댑티브 비트레이트 스트리밍]() 기능을 사용하여 다중 비트레이트 어댑티브 HLS 또는 DASH 대상 파일을 생성합니다.
2. 플레이어를 초기화하고 비디오 객체 주소를 전달합니다.
```
var player = TCPlayer("player-container-id", {}); // player-container-id는 플레이어 컨테이너 ID로 html 상의 것과 일치해야 합니다.
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"); // 다중 비트레이트 비디오 주소
```

코드 샘플 가져오기:
- [해상도 전환을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/multiDefinition.html)

[](id:6)
### 동적 워터마크 설정
플레이어는 비디오에 위치와 속도가 변화하는 동적 워터마크 추가를 지원합니다. 동적 워터마크 기능을 사용할 때 플레이어 객체의 참고가 전역 환경에 노출되어서는 안 됩니다. 그렇지 않으면 동적 워터마크를 쉽게 제거할 수 있습니다. CI를 사용하면 클라우드의 비디오에 동적 워터마크를 추가할 수도 있습니다. 자세한 내용은 워터마크 템플릿 API를 참고하십시오.
```
var player = TCPlayer("player-container-id", {
    plugins:{
      DynamicWatermark: {
        speed: 0.2, // 속도
        content: "Tencent Cloud CI", // 텍스트
        opacity: 0.7 // 불투명도
      }
    }
  });
```

코드 샘플 가져오기:
- [동적 워터마크 설정을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/dynamicWatermark.html)

[](id:7)
### 롤 이미지 광고 설정
작업 순서는 다음과 같습니다.
1. 광고 썸네일과 링크를 준비합니다.
2. 플레이어를 초기화하고, 광고 썸네일과 링크를 설정하고, 광고 노드를 설정합니다.
```
var PosterImage = TCPlayer.getComponent('PosterImage');
PosterImage.prototype.handleClick = function () {
	window.open('https://cloud.tencent.com/product/ci'); // 광고 링크 설정
};

var player = TCPlayer('player-container-id', {
	poster: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx..png', // 광고 미리보기 이미지
});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');

var adTextNode = document.createElement('span');
adTextNode.className = 'ad-text-node';
adTextNode.innerHTML = ‘광고’;

var adCloseIconNode = document.createElement('i');
adCloseIconNode.className = 'ad-close-icon-node';
adCloseIconNode.onclick = function (e) {
  e.stopPropagation();
  player.posterImage.hide();
};

player.posterImage.el_.appendChild(adTextNode);
player.posterImage.el_.appendChild(adCloseIconNode);
```

코드 샘플 가져오기:
- [롤 이미지 광고 구성을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/advertise.html)

[](id:8)
### 비디오 진행 썸네일 설정(이미지 스프라이트)
작업 순서는 다음과 같습니다.
1. CI의 [Video Frame Capturing](https://intl.cloud.tencent.com/document/product/1045/47736) 기능을 사용하여 이미지 스프라이트를 생성합니다.
2. 1단계에서 생성된 이미지 스프라이트 및 VTT(이미지 스프라이트 위치 설명 파일)의 객체 주소를 가져옵니다.
3. 플레이어를 초기화하고 비디오 및 VTT 파일 주소를 설정합니다.
```
var player = TCPlayer('player-container-id', {
  plugins: {
    VttThumbnail: {
      vttUrl: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.vtt' // VTT 파일
    },
  },
});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
```

코드 샘플 가져오기:
- [이미지 스프라이트 구성을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/preview.html)

[](id:9)
### 동영상 자막 설정
작업 순서는 다음과 같습니다.
1. CI의 음성 인식 기능으로 자막 파일을 생성합니다.
2. 1단계에서 생성된 SRT 파일의 객체 주소를 가져옵니다.
3. 플레이어를 초기화하고 비디오 및 SRT 파일 주소를 설정합니다.
```
var player = TCPlayer('player-container-id', {});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
player.on('ready', function () {
  // 자막 파일 추가
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.srt', // 자막 파일
    kind: 'subtitles',
    srclang: 'zh-cn',
    label: '중국어',
    default: 'true',
  }, true);
});
```

코드 샘플 가져오기:
- [동영상 자막 구성을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/subtitle.html)

[](id:10)
### 다국어 동영상 자막 설정
작업 순서는 다음과 같습니다.
1. CI의 음성 인식 기능으로 자막 파일을 생성하고 다국어로 번역합니다.
2. 1단계에서 생성된 다국어 SRT 파일의 객체 주소를 가져옵니다.
3. 플레이어를 초기화하고 비디오 및 다국어 SRT 파일 주소를 설정합니다.
```]
var player = TCPlayer('player-container-id', {});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
player.on('ready', function () {
  // 중국어 자막 설정
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/zh.srt', // 자막 파일
    kind: 'subtitles',
    srclang: 'zh-cn',
    label: '중국어',
    default: 'true',
  }, true);
  // 영어 자막 설정
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/en.srt', // 자막 파일
    kind: 'subtitles',
    srclang: 'en',
    label: '영어',
    default: 'false',
  }, true);
});
```

코드 샘플 가져오기:
- [다국어 자막 구성을 위한 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/multiLanguage.html)

