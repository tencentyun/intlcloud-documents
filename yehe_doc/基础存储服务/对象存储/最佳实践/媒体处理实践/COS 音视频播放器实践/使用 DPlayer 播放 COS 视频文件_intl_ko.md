## 소개

본문은 [DPlayer](https://dplayer.js.org/)를 [Cloud Infinite(CI)](https://www.tencentcloud.com/document/product/1045/46980)의 풍부한 오디오/비디오 기능과 함께 사용하여 Web 브라우저에서 COS에 저장된 비디오 파일을 재생하는 방법을 설명합니다.

## 통합 가이드

#### 1단계: 플레이어 스크립트 파일 및 필요한 종속성 파일을 페이지로 가져오기
```
<!-- 플레이어 스크립트 파일 -->
<script src="https://cdn.jsdelivr.net/npm/dplayer@1.26.0/dist/DPlayer.min.js"></script>
```
>?플레이어 사용 시 상기 정적 리소스를 직접 배포하는 것을 권장합니다.

#### 2단계: 플레이어 컨테이너 노드 설정
플레이어를 표시할 페이지에 플레이어 컨테이너를 추가합니다. 예를 들어 index.html에 다음 코드를 추가합니다(컨테이너 ID와 너비 및 높이를 사용자 지정할 수 있음).
```
<div id="dplayer" style="width: 100%; height: 100%"></div>
```

#### 3단계: 비디오 파일 객체 주소 가져오기
1. [버킷을 생성](https://intl.cloud.tencent.com/document/product/436/13309)합니다.
2. [비디오 파일 객체를 업로드](https://intl.cloud.tencent.com/document/product/436/13321)합니다.
3. `https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<비디오 형식>` 형식의 비디오 파일 객체 주소를 가져옵니다.

>?
> - Cross-Origin 액세스가 포함된 경우 [CORS 설정](https://intl.cloud.tencent.com/document/product/436/13318)을 참고하여 버킷에 대한 CORS를 설정해야 합니다.
> - 버킷 권한이 비공개 읽기/쓰기인 경우 객체 주소에 서명이 있어야 합니다. 자세한 내용은 [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)를 참고하십시오.

#### 4단계: 플레이어 초기화 및 COS 동영상 파일 객체 URL 전달
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4', // COS 비디오 객체 주소
  },
});
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
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4', // COS 비디오 객체 주소
  },
});
```

코드 샘플 가져오기:
- [MP4 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/mp4.html)
- [FLV 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/flv.html)
- [HLS 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/m3u8.html)
- [DASH 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/dash.html)

[](id:2)
### PM3U8 비디오 재생
PM3U8은 비공개 M3U8 비디오 파일을 나타냅니다. COS는 비공개 M3U8 TS 리소스를 얻기 위한 다운로드 인증 API를 제공합니다. 자세한 내용은 [Private M3U8 API](https://intl.cloud.tencent.com/document/product/436/47220)를 참고하십시오.
```
 const dp = new DPlayer({
   container: document.getElementById('dplayer'),
   // pm3u8에 대한 자세한 내용: https://intl.cloud.tencent.com/document/product/436/47220
   video: {
     url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600' // 비공개 ts 리소스 url에 대한 다운로드 자격 증명의 상대적 유효 기간(3600초)
   }
 });
```
코드 샘플 가져오기:
- [PM3U8 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/pm3u8.html)

[](id:3)
### 썸네일 설정
1. COS 버킷에 있는 썸네일의 객체 주소를 가져옵니다.
>!CI의 [Intelligent Thumbnail](https://intl.cloud.tencent.com/document/product/1045/47740) 기능은 최적의 프레임을 추출하여 썸네일을 생성하여 비디오 콘텐츠를 더 매력적으로 만들 수 있습니다.
2. 플레이어를 초기화하고 썸네일 이미지를 설정합니다.
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
    url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4',
    pic: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.png',
  },
});
```

코드 샘플 가져오기:
- [썸네일 구성 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/poster.html)

[](id:4)
### HLS 암호화 비디오 재생
CI는 동영상 콘텐츠의 보안을 확보하고 동영상의 무단 다운로드 및 배포를 방지하기 위해 개인이 읽을 수 있는 파일보다 안전한 HLS 동영상 콘텐츠를 암호화하는 기능을 제공합니다. 암호화된 비디오는 재생 액세스 권한이 없는 사용자에게 배포할 수 없습니다. 다운로드하더라도 여전히 암호화되어 악의적으로 재배포할 수 없습니다. 이렇게 하면 비디오 저작권이 침해되는 것을 방지할 수 있습니다.
작업 순서는 다음과 같습니다.
1. [HLS 암호화 비디오 재생](https://intl.cloud.tencent.com/document/product/436/48293) 및 [COS 오디오/비디오 실습 | 비디오 암호화](https://mp.weixin.qq.com/s/4f-GKyAG0S-FcZ2BZCn7jA)를 참고하여 암호화된 비디오를 생성합니다.
2. 플레이어를 초기화하고 비디오 객체 주소를 전달합니다.
```
 const dp = new DPlayer({
   container: document.getElementById('dplayer'),
   video: {
     url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8' // 암호화된 비디오 주소
   }
 });
```


코드 샘플 가져오기:
- [HLS 암호화 재생 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/m3u8.html)

[](id:5)
### 다중 해상도 전환

CI의 [Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/1045/47745) 기능은 비디오를 트랜스코딩하고 이를 어댑티 비트스트림으로 리먹싱하여 출력할 수 있으므로 다양한 네트워크 조건에서 비디오 콘텐츠를 빠르게 배포할 수 있습니다. 플레이어는 현재 대역폭에 따라 비디오를 재생하는 데 가장 적합한 비트레이트를 동적으로 선택할 수 있습니다. 자세한 내용은 [COS 오디오/비디오 실습 | 데이터 처리 워크플로로 다중 해상도 비디오 재생](https://mp.weixin.qq.com/s/THUhur1FV_55T9zzqT2MFQ)을 참고하십시오.

작업 순서는 다음과 같습니다.
1. CI의 [Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/1045/47745) 기능으로 멀티 비트레이트 어댑티브 HLS 또는 DASH 대상 파일을 생성합니다.
2. 플레이어를 초기화하고 비디오 객체 주소를 전달합니다.
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8', //  멀티 비트레이트 HLS/DASH 비디오
  },
});
```

코드 샘플 가져오기:
- [해상도 전환 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/multiDefinition.html)

[](id:6)
### 왼쪽 상단 LOGO 설정
플레이어를 사용하면 왼쪽 상단 모서리에 LOGO를 설정할 수 있습니다.
작업 순서는 다음과 같습니다.
1. COS 버킷에서 LOGO의 객체 주소를 가져옵니다.
2. 플레이어를 초기화하고 LOGO를 설정합니다.
```
const dp = new DPlayer({
	container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4',
  },
	logo: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.svg'
});
```

코드 샘플 가져오기:
- [좌측 상단 LOGO 설정 샘플 코드](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/logo.html)


