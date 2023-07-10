본문은 클라우드에서 COS 오디오/비디오 파일을 처리하고 클라이언트에서 재생하는 방법을 설명합니다. 이 문서의 예시는 오디오/비디오 처리를 위해 지원되는 프로토콜 및 기능을 다루며 재생 성능을 향상시키기 위해 CI에서 [Media Processing Service](https://www.tencentcloud.com/document/product/1045/46980)의 풍부한 오디오/비디오 처리 기능을 기반으로 제품 기능을 사용하는 방법에 대해 더 많은 아이디어를 제공합니다.

## 지원되는 프로토콜

|   오디오/비디오 프로토콜    | URL 형식                                                 | PC 브라우저 | 모바일 브라우저 |
| :-------------: | ------------------------------------------------------------ | --------- | ------------ |
|       MP3       | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.mp3 | 지원      | 지원         |
|       MP4       | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.mp4 | 지원      | 지원         |
| HLS<br/>(M3U8) | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.m3u8 | 지원      | 지원         |
|       FLV       | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.flv | 지원      | 지원         |
|      DASH       | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.mpd | 지원      | 지원         |

>!HLS, FLV, DASH 비디오는 일부 브라우저 환경에서 재생하려면 <a href="https://caniuse.com/?search=Media Source Extensions">Media Source Extensions</a>에 종속해야 합니다.

## 지원되는 기능

| 기능                       | TCPlayer | DPlayer | Videojs Player |
| -------------------------- | --------------- | -------------- | -------------- |
| MP4 비디오 재생          | 상세 보기        | 상세 보기       | 상세 보기       |
| HLS 비디오 재생          | 상세 보기        | 상세 보기       | 상세 보기       |
| FLV 비디오 재생          | 상세 보기        | 상세 보기       | 상세 보기       |
| DASH 비디오 재생         | 상세 보기        | 상세 보기       | 상세 보기       |
| PM3U8(개인 M3U8) 비디오 재생 | 상세 보기        | 상세 보기       | 상세 보기       |
| 썸네일 구성                 | 상세 보기        | 상세 보기       | 상세 보기       |
| 표준 HLS 암호화 구성          | 상세 보기        | 상세 보기       | 상세 보기       |
| 해상도 전환                 | 상세 보기        | 상세 보기       | -              |
| 동적 워터마크 구성               | 상세 보기        | -              | -              |
| 왼쪽 상단 LOGO 구성            | -               | 상세 보기       | -              |
| 진행률 표시줄 미리보기 이미지 구성             | 상세 보기        | -              | -              |
| 자막 구성                   | 상세 보기        | -              | -              |
| 다국어 구성                 | 상세 보기        | -              | -              |
| 롤 이미지 광고 구성               | 상세 보기        | -              | -              |

>? 플레이어는 일반 브라우저와 호환되며 최적의 재생 구성표를 사용할 플랫폼을 자동으로 식별할 수 있습니다. 예를 들어 Chrome과 같은 최신 브라우저에서 비디오 재생을 위해 HTML5 기술을 사용하고 모바일 브라우저에서 HTML5 기술 또는 브라우저 커널 기능을 직접 사용하는 것이 좋습니다.

## 사용 가이드
- TCPlayer 사용하여 COS에서 비디오 재생
- DPlayer 사용하여 COS에서 비디오 재생
- VideojsPlayer 사용하여 COS 비디오 재생


