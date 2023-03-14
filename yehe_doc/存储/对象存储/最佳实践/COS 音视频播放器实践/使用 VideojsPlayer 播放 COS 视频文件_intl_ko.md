## 소개
본문은 [VideojsPlayer](https://videojs.com/)를 [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045/46980)의 풍부한 오디오/비디오 기능과 함께 사용하여 Web 브라우저에서 COS에 저장된 비디오 파일을 재생하는 방법을 설명합니다.

## 통합 가이드

#### 1단계: 플레이어 양식 및 스크립트 파일을 페이지로 가져오기
```
<!-- 플레이어 양식 파일 -->
<link href="https://vjs.zencdn.net/7.19.2/video-js.css" rel="stylesheet" />
<!-- 플레이어 스크립트 파일 -->
<script src="https://vjs.zencdn.net/7.19.2/video.min.js"></script>
```

>?플레이어 사용 시 위의 정적 리소스를 직접 배포하는 것을 권장합니다.

#### 2단계: 플레이어 컨테이너 노드 설정
플레이어를 표시할 페이지에 플레이어 컨테이너를 추가합니다. 예를 들어 index.html에 다음 코드를 추가합니다(컨테이너 ID와 너비 및 높이를 사용자 지정할 수 있음).
```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
></video>
```

#### 3단계: 비디오 파일 객체 주소 가져오기
1. [버킷을 생성](https://intl.cloud.tencent.com/document/product/436/13309)합니다.
2. [비디오 파일 객체를 업로드](https://intl.cloud.tencent.com/document/product/436/13321)합니다.
3. `https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<비디오 형식>` 형식의 비디오 파일 객체 주소를 가져옵니다.

>?
> - Cross-Origin 액세스가 포함된 경우 [CORS 설정](https://intl.cloud.tencent.com/document/product/436/13318)을 참고하여 버킷에 대한 CORS를 설정해야 합니다.
> - 버킷 권한이 비공개 읽기/쓰기인 경우 객체 주소에 서명이 있어야 합니다. 자세한 내용은 [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)를 참고하십시오.

#### 4단계: 플레이어 컨테이너에 비디오 주소를 설정하고 COS 비디오 파일 객체 URL을 전달합니다.
```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
>
  <source
    src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
    type="video/mp4"
  />
</video>
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
<!-- MP4 -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
  type="video/mp4"
/>

<!-- HLS -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"
  type="application/x-mpegURL"
/>

<!-- FLV -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.flv"
  type="video/x-flv"
/>

<!-- DASH -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mpd"
  type="application/dash+xml"
/>
```

코드 샘플 가져오기:
- [MP4 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/mp4.html)
- [FLV 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/flv.html)
- [HLS 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/m3u8.html)
- [DASH 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/dash.html)

[](id:2)
### PM3U8 비디오 재생
PM3U8은 개인 M3U8 비디오 파일을 나타냅니다. COS는 개인 M3U8 TS 리소스를 가져오기 위한 다운로드 권한 API를 제공합니다. 자세한 내용은 [Private M3U8 API](https://intl.cloud.tencent.com/document/product/436/47220)를 참고하십시오.
```
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600"
  type="application/x-mpegURL"
/>
```

코드 샘플 가져오기:
- [PM3U8 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/pm3u8.html)

[](id:3)
### 썸네일 설정
1. COS 버킷에 있는 썸네일의 객체 주소를 가져옵니다.
>!CI의 [Intelligent Thumbnail](https://intl.cloud.tencent.com/document/product/1045/47740) 기능은 최적의 프레임을 추출하여 썸네일을 생성하여 비디오 콘텐츠를 더 매력적으로 만들 수 있습니다.
2. 플레이어를 초기화하고 썸네일 이미지를 설정합니다.
```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
  poster="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/poster.png"
>
  <source
    src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
    type="video/mp4"
  />
</video>
```

코드 샘플 가져오기:
- [썸네일 구성 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/poster.html)

[](id:4)
### HLS 암호화 비디오 재생
CI는 동영상 콘텐츠의 보안을 확보하고 동영상의 무단 다운로드 및 배포를 방지하기 위해 개인이 읽을 수 있는 파일보다 안전한 HLS 동영상 콘텐츠를 암호화하는 기능을 제공합니다. 암호화된 비디오는 재생 액세스 권한이 없는 사용자에게 배포할 수 없습니다. 다운로드하더라도 여전히 암호화되어 악의적으로 재배포할 수 없습니다. 이렇게 하면 비디오 저작권이 침해되는 것을 방지할 수 있습니다.
작업 순서는 다음과 같습니다.
1. [HLS 암호화 비디오 재생](https://intl.cloud.tencent.com/document/product/436/48293) 및 [COS 오디오/비디오 실습 | 비디오 암호화](https://mp.weixin.qq.com/s/4f-GKyAG0S-FcZ2BZCn7jA)를 참고하여 암호화된 비디오를 생성합니다.
2. 플레이어를 초기화하고 비디오 객체 주소를 전달합니다.
```
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"
  type="application/x-mpegURL"
/>
```

코드 샘플 가져오기:
- [HLS 암호화 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/m3u8.html)



