## 학습 목표
이 문서는 비디오를 코드 변환하고 플레이어를 사용하여 출력 비디오를 재생하는 방법을 설명합니다.
본 문서를 읽기 전에 Player 가이드의 [Stage 1. Play back a source video](https://www.tencentcloud.com/document/product/266/51564)을 반드시 읽으십시오. 이 문서는 [1단계](https://intl.cloud.tencent.com/document/product/266/38098)에서 활성화된 계정과 업로드된 비디오를 사용합니다.

## 1단계: 비디오 트랜스코딩
1. VOD 콘솔에서 **미디어 자산**>왼쪽 사이드바의 [**오디오/비디오 관리**](https://console.cloud.tencent.com/vod/media)를 선택하고 대상 비디오(여기 예시에서는, 암호화된 비디오의 FileId는 387xxxxx8142975036임) **처리**를 클릭합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3unX216_1.png" width="900" />

2. **처리** 페이지에서:
 - **처리 유형**에 대해 **트랜스코딩**을 선택합니다.
 - **트랜스코딩 템플릿**에 대해 **템플릿 선택**을 클릭합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/U4VK178_2.png" width="722" />

**트랜스코딩 템플릿 선택** 팝업 페이지에서 템플릿 `STD-H264-MP4-540P`(ID: `100020`)를 선택합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/xtzd936_3.png" width="722" />

**확인**을 클릭하여 트랜스코딩 작업을 시작합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/pahm058_4.png" width="650" />

3. [**작업 관리**](https://console.cloud.tencent.com/vod/task)페이지로 이동하여 작업 상태를 확인합니다. **작업 상태**가 **처리 중**에서 **완료**로 변경되면 비디오 처리가 완료된 것입니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Q4bA978_5.png" width="900" />

4. 미디어 자산>[**오디오/비디오 관리**](https://console.cloud.tencent.com/vod/media)로 이동하고 대상 비디오 오른쪽에 있는 **관리**를 클릭하여 관리 페이지로 들어갑니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Mfdx017_6.png" width="900" />

**기본 정보** 탭을 선택합니다.
 - **표준 트랜스코딩 목록**에서 트랜스코딩에 성공한 템플릿 목록을 확인할 수 있습니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/LJcj256_7.jpg" width="900" />

## 2단계: Player 서명 생성
이 단계에서는 서명 툴을 사용하여 플레이어가 비디오를 재생할 서명을 빠르게 생성할 수 있습니다.
**배포 및 재생**>[**플레이어 서명 툴**](https://console.cloud.tencent.com/vod/distribute-play/signature)을 선택하고 다음 정보를 입력합니다.
 - **비디오 fileId**: **1단계**에서 사용한 FileId(387xxxxx8142975036)를 입력합니다.
 - **서명 만료 시간**: 플레이어 서명 만료 시간을 입력합니다. 비워두면 서명이 만료되지 않습니다.
 - **재생 가능한 비디오 유형**: **트랜스코딩**을 선택합니다.
 - **재생 가능한 트랜스코딩 템플릿**: `STD-H264-MP4-540P (100020)`를 선택합니다.

**생성**을 클릭하여 서명 문자열을 가져옵니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/SpCE136_8.png" width="900" />

## 3단계: 비디오 재생
2단계 후에는 비디오 재생에 필요한 세 가지 매개변수인 `appId`, `fileId` 및 `psign`(플레이어 서명)을 얻었습니다. 다음은 Web에서 비디오를 재생하는 방법을 설명합니다.

### Web에서 재생
[Web 플레이어 데모](https://tcplayer.vcube.tencent.com/)를 열고 다음과 같이 구성합니다.
 - **플레이어 기능**: **비디오 재생**을 선택합니다.
 - **FileID로 재생** 탭을 클릭합니다.
 - **fileID**: 이전 단계의 FileId(387xxxxx8142975036)를 입력합니다.
 - **appID**: 파일이 속한 appId 즉, 이전 단계에서 플레이어 서명 생성 페이지의 appID를 입력합니다.
 - **psign**: 이전 단계에서 생성한 서명 문자열을 입력합니다.

**미리보기**를 클릭하여 비디오를 재생합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/kzkm097_9.png" width="900" />

### 멀티 플랫폼 플레이어 Demo
Player 서명을 받은 후 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android) 및 [iOS](https://github.com/LiteAVSDK/Player_iOS)용 Player Demo를 사용하여 확인할 수 있습니다. 자세한 내용은 Demo 소스 코드를 참고하십시오.


## 요약

이제 비디오를 코드 변환하고 플레이어를 사용하여 재생하는 방법을 이해했습니다.
