AOMedia Video 1(AV1)은 무료 오픈 소스 비디오 코딩 형식입니다. 동일한 비디오 품질을 제공하면서 H.265[HEVC]보다 30% 이상 낮은 비트 레이트로 비디오를 인코딩합니다. 이는 동일한 대역폭에서 AV 1로 인코딩된 비디오가 H.265로 인코딩된 비디오보다 더 높은 품질을 가짐을 의미합니다. 이 문서는 AV1을 사용하여 비디오를 인코딩하는 방법과 AV1 인코딩된 비디오를 재생하는 방법을 보여줍니다.

## AV1 사용

### 전제 조건

- [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 있어야 합니다.
- CSS를 활성화하고 [재생 도메인 및 푸시 도메인](https://intl.cloud.tencent.com/document/product/267/35970)을 추가해야 합니다.

[](id:step1)
### 1단계: 트랜스코딩 템플릿 생성
1. CSS 콘솔에 로그인하여 **기능 설정** > [라이브 트랜스코딩](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. **트랜스코딩 템플릿 생성**을 클릭하고 트랜스코딩 유형으로 표준 트랜스코딩 또는 최고속 코덱 트랜스코딩을 선택한 다음 고급 구성을 확장합니다.
3. **AV1**을 코덱으로 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9cd4c835c3cc37f3da93c07805ce4e5f.png) 
4. **저장**을 클릭합니다.

[](id:step2)
### 2단계: 도메인 바인딩
생성된 트랜스코딩 템플릿을 선택하고 **바인딩 도메인 이름**을 클릭합니다. 팝업 창에서 **재생 도메인**을 선택하고 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a7d945597ae3ff71557720b4e6eeae43.png)

[](id:step3)
### 3단계: 재생 URL 생성
왼쪽 사이드바에서 **주소 생성기**를 선택합니다. 2단계에서 바인딩된 재생 도메인과 [1단계](#step1)에서 생성한 트랜스코딩 템플릿을 선택하고 **주소 생성**을 클릭하여 재생 URL을 생성합니다.

[](id:step4)
### 4단계: AV1 인코딩 동영상 재생

3단계에서 생성된 재생 URL을 사용하여 AV1을 지원하는 플레이어로 AV1 인코딩된 비디오를 재생합니다. AV1을 지원하는 타사 플레이어를 사용하거나 자체 플레이어를 다시 빌드할 수 있습니다.

- **AV1을 지원하는 타사 플레이어**
	- **App 클라이언트**
		- [ExoPlayer](https://github.com/google/ExoPlayer) libgav1 사용
		- [ijkplayer](https://github.com/bilibili/ijkplayer) FFmpeg (FFmpeg 업데이트 및 [dav1d](https://code.videolan.org/videolan/dav1d) 통합)
	- **Web**
		- [dash.js](http://cdn.dashjs.org/v2.4.0/jsdoc/index.html). 플레이어는 AV1을 지원하지만 AV1 비디오 디코딩 가능 여부는 브라우저에 따라 다릅니다. Chrome은 AV1 디코딩을 지원합니다.
		- [shaka-player](https://github.com/shaka-project/shaka-player). 플레이어는 AV1을 지원하지만 AV1 비디오 디코딩 가능 여부는 브라우저에 따라 다릅니다. Chrome은 AV1 디코딩을 지원합니다.
	- **PC**
	[Windowos](https://share.weiyun.com/haPT1L0W) & [MacOS](https://share.weiyun.com/W2btBASt)용 VLC는 FLV에서 AV1 및 FLV에서 HEVC를 지원합니다.
- **자신만의 플레이어 재구축**
플레이어가 AV1 동영상을 재생할 수 없는 경우 [고객센터](https://intl.cloud.tencent.com/contact-us)를 통해 AV1을 지원하도록 플레이어를 재구성할 수 있습니다.
