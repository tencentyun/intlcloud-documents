## 학습 목표
이 문서는 비디오를 암호화하고 플레이어를 사용하여 암호화된 비디오를 재생하는 방법을 설명합니다.
본 문서를 읽기 전에 플레이어 가이드의 [Stage 1. Play back a source video](https://www.tencentcloud.com/document/product/266/51564)을 읽으십시오. 이 문서는 활성화된 계정과 [1단계](https://intl.cloud.tencent.com/document/product/266/38098)에서 업로드한 비디오를 사용합니다.

## 1단계: 비디오 암호화
1. VOD 콘솔에서 왼쪽 사이드바의 **미디어 자산**>[**오디오/비디오 자산**](https://console.cloud.tencent.com/vod/media)을 선택하고, 대상 비디오를 선택하고(이 예시에서 처리된 비디오의 FileId는 387xxxxx8142975036임) **프로세스**를 클릭합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/7ut4367_1.jpg" width="722" />

2. **프로세스** 페이지에서:
 - **처리 유형**은 **태스크 플로우**를 선택합니다.
 - **태스크 플로우 템플릿**에 대해 **SimpleAesEncryptPreset**을 선택합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/GkuI523_2.jpg" width="" style="zoom:90%;" /><span>

>?
>- SimpleAesEncryptPreset은 어댑티브 비트레이트 스트리밍을 위한 템플릿 12, 썸네일 생성을 위한 템플릿 10, 이미지 스프라이트 캡처를 위한 템플릿 10을 사용하는 사전 설정 태스크 플로우입니다.
>- 템플릿 12를 사용한 어댑티브 비트 레이트 스트리밍은 암호화된 다중 비트 레이트 스트림을 출력하는 것입니다.

3. **확인**을 클릭하고 [오디오/비디오 처리](https://console.cloud.tencent.com/vod/task) 탭 목록의 ‘작업 상태’가 ‘처리 중’에서 ‘완료’로 변경되어 비디오 처리가 완료되었음을 표시할 때까지 기다립니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/hUM7408_3.png)

4. **미디어 자산**>[**오디오/비디오 관리**](https://console.cloud.tencent.com/vod/media)로 이동하고 대상 비디오 오른쪽에 있는 **관리**를 클릭하여 관리 페이지로 들어갑니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ETsG597_4.jpg" width="900" />

**기본 정보** 탭을 선택합니다.
 - 암호화된 어댑티브 비트레이트 스트리밍(템플릿 ID: 12)의 생성된 썸네일 및 출력을 볼 수 있습니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/KBkV486_5.jpg" width="722" />
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/5NsV447_6.jpg" width="900" />

 **스크린샷 정보** 탭을 선택합니다.
 - 생성된 스프라이트 이미지를 볼 수 있습니다(템플릿 ID: 10).

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/XTu8560_7.jpg" width="900" />

## 2단계: Player 서명 생성
이 단계에서는 서명 툴을 사용하여 플레이어가 비디오를 재생할 서명을 빠르게 생성할 수 있습니다.
**배포 및 재생**>[**플레이어 서명 툴**](https://console.cloud.tencent.com/vod/distribute-play/signature)을 선택하고 다음 정보를 입력합니다.
 - **비디오 fileId**: **1단계**에서 사용한 FileId(387xxxxx8142975036)를 입력합니다.
 - **서명 만료 시간**: 플레이어 서명 만료 시간을 입력합니다. 비워두면 서명이 만료되지 않습니다.
 - **재생 가능한 비디오 유형**: **암호화된 어댑티브 비트레이트**를 선택합니다.
 - **암호화 유형**: **개인 암호화(SimpleAES)**를 선택합니다.
 - **재생 가능한 어댑티브 비트레이트 스트리밍 템플릿**: `Adpative-HLS-Encrypt (12)`를 선택합니다.
 - **썸네일 미리보기용 이미지 스프라이트 템플릿**: `SpriteScreenshot (10)`을 선택합니다.

**생성**을 클릭하여 서명 문자열을 가져옵니다.



## 3단계: 비디오 재생
2단계 후에는 비디오 재생에 필요한 세 가지 매개변수인 `appId`, `fileId` 및 `psign`(플레이어 서명)을 얻었습니다. 다음은 Web에서 비디오를 재생하는 방법을 설명합니다.

### Web에서 재생
[Web 플레이어 데모](https://tcplayer.vcube.tencent.com/)를 열고 다음과 같이 구성합니다.
 - **플레이어 기능**: **비디오 재생**을 선택합니다.
 - **FileID로 재생** 탭을 클릭합니다.
 - **fileID**: 이전 단계에서 FileId(387xxxxx8142975036)를 입력합니다.
 - **appID**: 파일이 속한 appId 즉, 이전 단계에서 플레이어 서명 생성 페이지의 appID를 입력합니다.
 - **psign**: 이전 단계에서 생성한 서명 문자열을 입력합니다.

**미리보기**를 클릭하여 비디오를 재생합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Eapx633_9.png" width="800" />

### 멀티 플랫폼 플레이어 Demo
Player 서명을 받은 후 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android) 및 [iOS](https://github.com/LiteAVSDK/Player_iOS)용 Player Demo를 사용하여 확인할 수 있습니다. 자세한 내용은 Demo 소스 코드를 참고하십시오.


## 결론

이제 비디오를 암호화하고 플레이어를 사용하여 재생하는 방법을 이해했습니다.
