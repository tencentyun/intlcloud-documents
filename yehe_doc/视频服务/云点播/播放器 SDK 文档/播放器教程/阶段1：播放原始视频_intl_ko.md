## 학습 목표
이 문서는 비디오를 VOD에 업로드하고 Player에서 재생하는 방법을 설명합니다.

## 전제 조건
시작하기 전에 다음을 수행하십시오.

### VOD 활성화
VOD를 활성화하려면 다음 단계를 따르십시오.

1. [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985) 및 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)을 완료합니다.
2. VOD 서비스를 구매합니다. 자세한 내용은 [과금 개요](https://intl.cloud.tencent.com/document/product/266/2838)를 참고하십시오.
3. **클라우드 서비스**>**비디오 서비스**>[**VOD**](https://console.cloud.tencent.com/vod)를 선택하여 VOD 콘솔로 이동합니다.

이제 VOD가 활성화됐습니다.

## 1단계: 비디오 업로드
이 단계에서는 비디오를 업로드하는 방법을 설명합니다.

1. VOD 콘솔에 로그인하고 **미디어 자산**>[ **오디오/비디오 관리** ](https://console.cloud.tencent.com/vod/media)를 선택하고 **오디오/비디오 업로드**를 클릭합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/eDZY097_1.jpg" width="822" />

2. 업로드 페이지에서 **로컬 업로드**를 선택하고 **파일 선택**을 클릭하여 로컬 비디오를 업로드하고 다른 필드를 다음과 같이 설정합니다.
	- **비디오 처리**에서 **업로드 후 처리 안 함**을 선택합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/zB6K038_2.jpg" style="zoom:67%;" />

3. **업로드**를 클릭하여 ‘업로드 중’ 페이지로 들어갑니다. **상태**가 **업로드됨**으로 변경되면 업로드가 완료된 것입니다. **파일 ID**는 업로드된 파일의 FileId입니다(여기서는 387xxxxx8142975036).
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/nMEx197_3.jpg" width="900" />

## 2단계: Player 서명 생성
이 단계에서는 서명 툴을 사용하여 Player가 비디오를 재생할 서명을 빠르게 생성할 수 있습니다.
**배포 및 재생** > [**Player 서명 툴**](https://console.cloud.tencent.com/vod/distribute-play/signature)을 선택하고 다음 정보를 입력합니다.
 - **비디오 fileId**: **1단계**에서 사용한 FileId(387xxxxx8142975036)를 입력합니다.
 - **서명 만료 시간**: 플레이어 서명 만료 시간을 입력합니다. 비워두면 서명이 만료되지 않습니다.
 - **재생 가능한 비디오 유형**: **원본**을 선택합니다.

**생성**을 클릭하여 서명 문자열을 가져옵니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3pgW155_4.jpg" width="900" />

## 3단계: 비디오 재생
2단계 후에는 비디오 재생에 필요한 세 가지 매개변수인 `appId`, `fileId` 및 `psign`(플레이어 서명)을 얻었습니다. 다음은 Web에서 비디오를 재생하는 방법을 설명합니다.

### Web에서 재생
[Web 플레이어 데모](https://tcplayer.vcube.tencent.com/)를 열고 다음과 같이 구성합니다.
 - **플레이어 기능**: **비디오 재생**을 선택합니다.
 - **FileID로 재생** 탭을 클릭합니다.
 - **fileID**: 이전 단계에서 FileId를 입력합니다(387xxxxx8142975036).
 - **appID**: 파일이 속한 appId 즉, 이전 단계에서 플레이어 서명 생성 페이지의 appID를 입력합니다.
 - **psign**: 이전 단계에서 생성한 서명 문자열을 입력합니다.

**미리보기**를 클릭하여 비디오를 재생합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/SfPg988_5.png" width="800" />

### 멀티 플랫폼 플레이어 Demo
Player 서명을 받은 후 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android) 및 [iOS](https://github.com/LiteAVSDK/Player_iOS)용 Player Demo를 사용하여 확인할 수 있습니다. 자세한 내용은 Demo 소스 코드를 참고하십시오.


## 요약

이제 비디오를 VOD에 업로드하고 플레이어에서 재생하는 방법을 학습 완료했습니다.

또한:
- [Stage 2. Play back a transcoded video](https://www.tencentcloud.com/document/product/266/51565)의 안내에 따라 트랜스코딩된 비디오를 재생합니다.
- [Stage 3. Play back an adaptive bitrate streaming video](https://www.tencentcloud.com/document/product/266/51566)의 안내에 따라 어댑티브 비트레이트 스트리밍 비디오를 재생합니다.
- [4단계: 암호화된 비디오 재생](https://www.tencentcloud.com/document/product/266/51556)의 안내에 따라 암호화된 비디오를 재생합니다.
- [5단계: 긴 비디오 재생](https://www.tencentcloud.com/document/product/266/51557)의 안내에 따라 긴 비디오를 재생합니다.
