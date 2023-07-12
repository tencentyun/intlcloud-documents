## 소개

본문에서는 Web 브라우저를 사용하여 Cloud Object Storage(COS) 버킷에 저장된 비디오 파일을 재생하고 일부 고급 비디오 재생 시나리오를 구현하는 방법을 설명합니다. [Tencent Cloud VOD Superplayer(TCPlayer)](https://intl.cloud.tencent.com/document/product/266/33977)를 예로 들어 단계를 설명합니다.

## 실행 순서

1. COS 비디오 파일 링크를 준비하려면 다음을 수행해야 합니다.
   - [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)
   - [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321)
   - [객체 정보](https://intl.cloud.tencent.com/document/product/436/13326)에서 객체 주소를 복사합니다.
2. 플레이어 양식 및 스크립트 파일을 페이지로 가져옵니다.
```
<!--플레이어 양식 파일-->
<link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/tcplayer.min.css" rel="stylesheet"/>
<!--Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 HLS 비디오를 재생하려면 tcplayer.v4.2.2.min.js을 가져오기 전에 hls.min.0.13.2m.js를 가져와야 합니다.-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/libs/hls.min.0.13.2m.js"></script>
<!--플레이어 스크립트 파일-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/tcplayer.v4.2.2.min.js"></script>
```
>?플레이어 SDK 사용 시 상기 정적 리소스를 직접 배포하는 것이 좋습니다. [플레이어 리소스를 다운로드하려면 여기 클릭](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/release.zip)합니다. 압축 해제 후 생성된 폴더를 배포합니다. 폴더의 디렉터리를 조정하지 마십시오. 그렇지 않으면 리소스 가져오기 예외가 발생할 수 있습니다.
>
3. 플레이어 컨테이너 노드를 설정합니다.
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
> 
4. 플레이어를 초기화하고 COS 비디오 파일 객체 URL을 전달합니다.
```
   var player = TCPlayer('player-container-id', {}); // player-container-id는 플레이어 컨테이너 ID로 html 상의 것과 일치해야 함
   player.src(url); // 재생 url
```

## 고급 사용 사례

### 사용 사례1: 공개 읽기 동영상 파일 재생

버킷의 공개 읽기 권한에는 공개 읽기/비공개 쓰기와 공개 읽기/쓰기의 두 가지 유형이 있습니다. 공개 읽기/비공개 쓰기 권한에서는 모든 사람(익명 방문자 포함)에게 버킷의 객체에 대한 읽기 권한이 있지만 버킷 작성자와 승인된 계정만 쓰기 권한이 있습니다. 공개 읽기/쓰기 권한에서는 모든 사람(익명 방문자 포함)이 버킷의 객체에 대해 읽기/쓰기 권한을 가지므로 권장하지 않습니다.

공개 읽기 비디오 파일을 재생하는 단계는 다음과 같습니다.
1. [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)에 설명된 대로 버킷을 공개적으로 읽을 수 있도록 설정합니다.
2. 동영상 파일을 업로드하고 [객체 정보](https://intl.cloud.tencent.com/document/product/436/13326)에서 객체 주소를 복사합니다.
3. TCPlayer를 사용하여 이전 단계에 따라 해당 주소에서 공개 읽기 비디오 파일을 재생합니다. 코드는 다음과 같습니다.
```
   <script>
     var tcplayer = TCPlayer("player-container-id", {})
     tcplayer.src('https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/test.mp4')
   </script>
```
4. 효과를 확인합니다.


### 사용 사례2: 비공개 읽기 동영상 파일 재생

버킷 데이터의 보안을 보장하기 위해 일반적으로 버킷에 대한 비공개 읽기/쓰기 권한을 설정하는 것이 좋습니다. 이 경우 버킷 생성자와 권한이 부여된 계정만 버킷의 객체를 읽고 쓸 수 있지만 다른 사람들은 읽을 수 없습니다.

비공개 읽기 비디오 파일 재생 단계는 다음과 같습니다.
1. [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)에 설명된 대로 버킷을 비공개로 읽을 수 있도록 설정합니다.
2. 버킷은 비공개 읽기이므로 액세스한 객체의 주소에 서명이 있어야 합니다. 세 가지 방법이 있습니다.
 - 옵션1: [객체 정보](https://intl.cloud.tencent.com/document/product/436/13326)의 **임시 링크 복사**. 여기에는 1시간 동안 유효한 서명 매개변수가 포함됩니다.

 - 옵션2: API 또는 SDK를 사용하여 객체 서명 계산. 자세한 내용은 [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)를 참고하십시오.
보다 편리하고 안전하게 객체 서명을 계산할 수 있는 SDK 옵션을 권장합니다.
3. TCPlayer를 사용하여 이전 단계를 기반으로 **서명과 함께** 주소에서 비공개 읽기 비디오 파일을 재생합니다. 코드는 다음과 같습니다.
```
   <script>
     var tcplayer = TCPlayer("player-container-id", {})
     tcplayer.src('https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/test.mp4?<Authorization>')
   </script>
```
4. 효과를 확인합니다.


### 사용 사례3: 공개 읽기 HLS 비디오 파일 재생

>? **HTTP Live Streaming(HLS)**은 Apple의 QuickTime X 및 iPhone 소프트웨어 시스템의 일부인 Apple에서 출시한 HTTP 기반 비디오 스트리밍 프로토콜입니다. 멀티파트 다운로드를 위해 전체 스트림을 작은 HTTP 기반 파일로 나누는 방식으로 작동합니다. 미디어 스트림이 재생되는 동안 클라이언트는 다른 소스에서 동일한 리소스를 다른 속도로 다운로드하도록 선택할 수 있으므로 스트리밍 세션이 다른 데이터 속도에 적응할 수 있습니다. 스트리밍 세션을 시작할 때 클라이언트는 메타데이터가 포함된 extended M3U m3u8playlist 파일을 다운로드하여 사용 가능한 미디어 스트림을 찾습니다.
>

Cloud Object Storage(COS) 데이터 처리는 [HLS 비디오 트랜스 코딩](https://intl.cloud.tencent.com/document/product/436/46409) 기능을 제공합니다. COS 데이터 워크플로에서 트랜스 코딩 작업을 기반으로 HLS 비디오 파일을 재생할 수 있습니다.

1. 시스템 템플릿에서 HLS 트랜스 코딩 작업을 선택하고 [작업 구성](https://intl.cloud.tencent.com/document/product/436/46409)의 지침에 따라 HLS 비디오 파일을 생성하도록 작업을 구성합니다.

2. 생성된 m3u8 파일 객체 주소를 복사합니다.

3. TCPlayer를 사용하여 이전 단계를 기반으로 해당 주소에서 **공개 읽기 HLS** 비디오 파일을 재생합니다. 코드는 다음과 같습니다.
```
   <script>
     var tcplayer = TCPlayer("player-container-id", {})
     tcplayer.src('https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/test.m3u8')
   </script>
```
4. 효과를 확인합니다.


### 사용 사례4: 비공개 읽기 HLS 비디오 파일 재생

사용 사례3을 기반으로 버킷 데이터의 보안을 보장하기 위해 버킷을 비공개 읽기/쓰기 가능으로 설정한 다음 PM3U8 API를 사용하여 비공개 HLS 비디오 파일을 재생할 수 있습니다. 단계는 다음과 같습니다.
1. [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)에 설명된 대로 버킷을 비공개로 읽을 수 있도록 설정합니다.
2. 버킷은 비공개이므로 TS 세그먼트별로 요청 서명을 설정해야 합니다. COS는 m3u8 파일을 요청할 때 `?ci-process=pm3u8&expires=3600` 매개변수를 전달할 수 있도록 **PM3U8** API를 제공합니다. 이러한 방식으로 반환된 파일의 TS 세그먼트에 대한 요청 경로는 해당 요청 서명을 전달할 수 있습니다.
  - ts 세그먼트에 서명이 없는 일반 m3u8 파일의 요청 결과는 다음과 같습니다.
     ![image-20211105162546606](https://qcloudimg.tencent-cloud.cn/raw/6209b43447acb028380ecc9a630b0fa7.png)
  - **PM3U8 API**를 사용한 후 요청 결과는 다음과 같으며, 여기서 ts 세그먼트는 서명을 전달합니다. ![image-20211105163202007](https://qcloudimg.tencent-cloud.cn/raw/d6eff5820f5aad79876c0cd65147ae64.png)
3. TCPlayer를 사용하여 이전 단계를 기반으로 해당 주소에서 **비공개 읽기 HLS** 비디오 파일을 재생합니다. 코드는 다음과 같습니다.
```
   <script>
     var tcplayer = TCPlayer("player-container-id", {})
     tcplayer.src('https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/test.m3u8?ci-process=pm3u8&expires=3600&sign')
   </script>
```


