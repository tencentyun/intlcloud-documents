## 학습 목표
본문은 다음을 포함하여 어댑티브 비트레이트 스트리밍 비디오를 재생하는 방법에 대해 설명합니다.

* 재생할 서브스트림의 해상도를 480p ~ 1080p 범위로 설정합니다.
* 비디오 스크린샷을 비디오 썸네일로 사용합니다.
* 진행률 표시줄의 미리보기 축소판 간격을 20%로 조정합니다.

본 문서를 읽기 전에 Player 가이드의 [Stage 1. Play back a source video](https://www.tencentcloud.com/document/product/266/51564)를 읽으십시오. 이 문서는 활성화된 계정과 [1단계](https://intl.cloud.tencent.com/document/product/266/38098)에서 업로드한 비디오를 사용합니다.

## 1단계: 어댑티브 비트 레이트 스트리밍 템플릿 만들기
1. VOD 콘솔에 로그인하여 [비디오 처리]>[[템플릿 설정]](https://console.cloud.tencent.com/vod/video-process/template)을 선택한 후 ‘어댑티브 비트레이트 스트리밍’ 탭에서 [템플릿 생성]을 클릭합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/PEXG353_1.png" width="900" />

2. ‘템플릿 설정’ 페이지에서 [서브스트림 추가]를 클릭하여 서브스트림 1, 2, 3을 생성하고 다음과 같이 매개변수를 입력합니다.
	- **기본 정보 모듈**:
	  - [템플릿 이름]: MyTestTemplate을 입력합니다.
	  - [먹싱 형식]: [HLS]를 선택합니다.
	  - [암호화 유형]: [암호화되지 않음]을 선택합니다.
	  - [저해상도에서 고해상도로 전환]: 이 옵션을 비활성화합니다.
	  - [트랜스코딩 방법]: [일반 트랜스코딩]을 선택합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/9InI915_2.png" width="722" />

 - **서브스트림 정보 모듈**:
<table>
<thead>
<tr>
<th>서브스트림 ID</th>
<th>비디오 비트 레이트</th>
<th>해상도</th>
<th>프레임 레이트</th>
<th>오디오 비트 레이트</th>
<th>사운드 채널</th>
</tr>
</thead>
<tbody><tr>
<td>서브스트림1</td>
<td>512kbps</td>
<td> 비디오 긴 면: 0px, 비디오 짧은 면: 480px</td>
<td>24fps</td>
<td>48kbps</td>
<td>듀얼 사운드 채널</td>
</tr>
<tr>
<td>서브스트림2</td>
<td>512kbps</td>
<td> 비디오 긴 면: 0px, 비디오 짧은 면: 720px</td>
<td>24fps</td>
<td>48kbps</td>
<td>듀얼 사운드 채널</td>
</tr>
<tr>
<td>서브스트림3</td>
<td>1024kbps</td>
<td> 비디오 긴 면: 0px, 비디오 짧은 면: 1080px</td>
<td>24fps</td>
<td>48kbps</td>
<td>듀얼 사운드 채널</td>
</tr>
</tbody></table>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/MxKn964_3.jpg" width="700" />

3. [생성]을 클릭합니다. 3개의 서브스트림을 포함하는 어댑티브 비트 레이트 스트리밍 템플릿이 생성되고 템플릿 ID는 `1429212`가 됩니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/1b1ffba4a8c37c8d81132e8f93c801b6.png" style="zoom:150%;" />

## 2단계: 이미지 스프라이트 템플릿 생성
1. VOD 콘솔에 로그인하여 [비디오 처리]>[[템플릿 설정]](https://console.cloud.tencent.com/vod/video-process/template)을 선택한 후, ‘스크린샷’ 탭에서 [스크린샷 템플릿 생성]을 클릭합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/hrUE650_5.png" width="900" />

2. ‘템플릿 설정’ 페이지에서 템플릿 매개변수를 입력합니다.
 * [템플릿 이름]: MyTestTemplate.
 * [스크린샷 유형]: [이미지 스프라이트 스크린샷].
 * [작은 이미지 크기]: 726px × 240px.
 * [샘플링 간격]: 20%.
 * [행]: 10.
 * [열]: 10.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/LIw5399_6.png)

3. [생성]을 클릭합니다. ID가 `131342`인 이미지 스프라이트 템플릿이 생성됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/4cf44757d6dbb339aa29c3c29fc480d7.png)

## 3단계: 태스크 플로우 생성 및 처리 시작
어댑티브 비트 레이트 스트리밍 템플릿(ID: 1429212) 및 이미지 스프라이트 템플릿(ID: 131342)을 생성한 후 태스크 플로우를 생성해야 합니다.

1. VOD 콘솔에 로그인하고 [비디오 처리]>[[태스크 플로우 설정]](https://console.cloud.tencent.com/vod/video-process/taskflow)을 선택하고 [태스크 플로우 생성]을 클릭합니다.
 * [태스크 플로우 이름]: MyTestProcedure를 입력합니다.
 * [구성 항목]: [어댑티브 비트 레이트 스트리밍], [스크린샷 작업] 및 [커버 스크린샷]을 선택합니다.
	 * [어댑티브 비트 레이트 스트리밍 작업 구성] 영역에서 [템플릿 추가]를 클릭하고 ‘어댑티브 비트 레이트 스트리밍 템플릿/ID’에 대해 **1단계**에서 만든 사용자 정의 어댑티브 비트 레이트 스트리밍 템플릿 MyTestTemplate(1429212)을 선택합니다.
	 *  [스크린샷 작업 구성] 영역에서 [템플릿 추가]를 클릭하고 ‘스크린샷을 찍는 방법’에 대해 [이미지 스프라이트]를 선택하고 ‘스크린샷/ID’에 대해 **2단계**에서 만든 사용자 정의 이미지 스프라이트 템플릿 MyTestTemplate(131342)을 선택합니다.
	 *  [커버 스크린샷 캡처 작업 구성] 영역에서 [템플릿 추가]를 클릭하고 ‘스크린샷 템플릿/ID’로 [TimepointScreenshot]을 선택한 후, [퍼센트]를 선택하고 50%를 입력합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Q6nQ449_8.png" width="900" />

2. [제출]을 클릭합니다. MyTestProcedure라는 태스크 플로우가 생성됩니다.

![](https://main.qcloudimg.com/raw/e33008c55dcc18bed3b41f96d88c5c8c.png)

3. 콘솔에서 [미디어 자산]>[[오디오/비디오 관리]](https://console.cloud.tencent.com/vod/media)를 선택하고 대상 비디오(FileId: 387xxxxx8142975036)를 선택한 후 [비디오 처리]를 클릭합니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Mpj9208_10.jpg" width="722" />

4. 비디오 처리 팝업 창에서:

 * [처리 유형]에 대해 [태스크 플로우]를 선택합니다.
 * [태스크 플로우 템플릿]에 대해 [MyTestProcedure]를 선택합니다.

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ctNZ059_11.png" width="700" />

5. **확인**을 클릭하고 [오디오/비디오 처리](https://console.cloud.tencent.com/vod/task) 탭 목록의 ‘작업 상태’가 ‘처리 중’에서 ‘완료’로 변경되어 비디오 처리가 완료되었음을 표시할 때까지 기다립니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/IuU9256_12.jpg" width="900" />

6. **미디어 자산**>[**오디오/비디오 관리**](https://console.cloud.tencent.com/vod/media)로 이동하고 대상 비디오 오른쪽에 있는 **관리**를 클릭하여 관리 페이지로 들어갑니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/UBpg014_13.png" width="900" />

**기본 정보** 탭을 선택합니다.
 - 어댑티브 비트레이트 스트리밍(템플릿 ID: 1429212)의 생성된 썸네일 및 출력을 볼 수 있습니다.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/gtLx554_14.jpg" width="722" />
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/358v600_15.jpg" width="900" />

 **스크린샷 정보** 탭을 선택합니다.
 - 생성된 이미지 스프라이트를 볼 수 있습니다(템플릿 ID: 131342).

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/KiVV307_16.jpg" width="900" />

## 4단계: Player 서명 생성
이 단계에서는 서명 툴을 사용하여 플레이어가 비디오를 재생할 서명을 빠르게 생성할 수 있습니다.
**배포 및 재생**>[**플레이어 서명 툴**](https://console.cloud.tencent.com/vod/distribute-play/signature)을 선택하고 다음 정보를 입력합니다.
 - **비디오 fileId**: **3단계**에서 사용한 FileId(387xxxxx8142975036)를 입력합니다.
 - **서명 만료 시간**: 플레이어 서명 만료 시간을 입력합니다. 비워두면 서명이 만료되지 않습니다.
 - **재생 가능한 비디오 유형**: **암호화되지 않은 어댑티브 비트레이트**를 선택합니다.
 - **재생 가능한 어댑티브 비트레이트 스트리밍 템플릿**: `MyTestTemplate(1429212)`을 선택합니다.
 - **썸네일 미리보기용 이미지 스프라이트 템플릿**: `MyTestTemplate (131342)`을 선택합니다.

**생성**을 클릭하여 서명 문자열을 가져옵니다.



## 5단계: 비디오 재생
4단계 후에는 비디오 재생에 필요한 세 가지 매개변수인 `appId`, `fileId` 및 `psign`(플레이어 서명)을 얻었습니다. 다음은 Web에서 비디오를 재생하는 방법을 설명합니다.

### Web에서 재생
[Web 플레이어 데모](https://tcplayer.vcube.tencent.com/)를 열고 다음과 같이 구성합니다.
 - **플레이어 기능**: **비디오 재생**을 선택합니다.
 - **FileID로 재생** 탭을 클릭합니다.
 - **fileID**: 이전 단계에서 FileId(387xxxxx8142975036)를 입력합니다.
 - **appID**: 파일이 속한 appId 즉, 이전 단계에서 플레이어 서명 생성 페이지의 appID를 입력합니다.
 - **psign**: 이전 단계에서 생성한 서명 문자열을 입력합니다.

**미리보기**를 클릭하여 비디오를 재생합니다.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/V98D696_18.png" width="900" />

### 멀티 플랫폼 플레이어 Demo
Player 서명을 받은 후 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android) 및 [iOS](https://github.com/LiteAVSDK/Player_iOS)용 Player Demo를 사용하여 확인할 수 있습니다. 자세한 내용은 Demo 소스 코드를 참고하십시오.

## 요약
이제 어댑티브 비트레이트 스트리밍 비디오를 재생하는 방법을 이해했습니다.
동영상을 암호화하고 암호화된 동영상을 재생하려면 [4단계: 암호화된 비디오 재생](https://www.tencentcloud.com/document/product/266/51556)을 참고하십시오.
