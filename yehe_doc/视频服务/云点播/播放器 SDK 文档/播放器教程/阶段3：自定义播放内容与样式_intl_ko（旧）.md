## 학습 목표

본 문서에서는 다음을 포함하여 Player가 재생하는 비디오의 콘텐츠와 스타일을 사용자 정의하는 방법을 설명합니다.

* 재생할 서브스트림의 해상도를 480p ~ 1080p 범위로 설정합니다.
* 비디오 스크린샷을 비디오 썸네일로 사용합니다.
* 진행률 표시줄의 미리보기 축소판 간격을 20%로 조정합니다.

본 문서를 읽기 전에 Player 가이드의 [1단계: Player로 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38098) 및 [2단계: 링크 도용 방지가 활성화된 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38292)을 읽었는지 확인하십시오. 본 문서는 [1단계](https://intl.cloud.tencent.com/document/product/266/38098)에서 활성화된 계정과 업로드된 동영상을 사용하며 [2단계](https://intl.cloud.tencent.com/document/product/266/38292)에 따라 링크 도용 방지를 활성화합니다.

## 1단계: 어댑티브 비트 레이트 스트리밍 템플릿 만들기

1. VOD 콘솔에 로그인하여 [비디오 처리]>[[템플릿 설정]](https://console.cloud.tencent.com/vod/video-process/template)을 선택한 후 ‘어댑티브 비트레이트 스트리밍’ 탭에서 [템플릿 생성]을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/19f292b6dbd89cf702ba27b3e9adf042.png" width="800" />
2. ‘템플릿 설정’ 페이지에서 [서브스트림 추가]를 클릭하여 서브스트림 1, 2, 3을 생성하고 다음과 같이 매개변수를 입력합니다.
	- **기본 정보 모듈**:
	  - [템플릿 이름]: MyTestTemplate를 입력합니다.
	  - [암호화 유형]: [암호화되지 않음]을 선택합니다.
	  - [저해상도에서 고해상도로 전환]: 이 옵션을 비활성화합니다.

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

<img src="https://qcloudimg.tencent-cloud.cn/raw/995fcae82a8d2f1a27f0b128147c285b.png" width="500" />
3. [생성]을 클릭합니다. 3개의 서브스트림을 포함하는 어댑티브 비트 레이트 스트리밍 템플릿이 생성되고 템플릿 ID는 125866가 됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1b1ffba4a8c37c8d81132e8f93c801b6.png)

## 2단계: 이미지 스프라이트 템플릿 생성

1. VOD 콘솔에 로그인하여 [비디오 처리]>[[템플릿 설정]](https://console.cloud.tencent.com/vod/video-process/template)을 선택한 후, ‘스크린샷’ 탭에서 [스크린샷 템플릿 생성]을 클릭합니다.
2. ‘템플릿 설정’ 페이지에서 템플릿 매개변수를 입력합니다.
 * [템플릿 이름]: MyTestTemplate.
 * [스크린샷 유형]: [이미지 스프라이트 스크린샷].
 * [이미지 크기]: 726px × 240px.
 * [샘플링 간격]: 20%.
 * [행]: 10.
 * [열]: 10.
![](https://qcloudimg.tencent-cloud.cn/raw/7ec21a1d127a0b5284a491fcac90c3a9.png)
3. [생성]을 클릭합니다. ID가 41377인 이미지 스프라이트 템플릿이 생성됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4cf44757d6dbb339aa29c3c29fc480d7.png)

## 3단계: 태스크 플로우 생성 및 처리 시작

어댑티브 비트 레이트 스트리밍 템플릿(ID: 125866) 및 이미지 스프라이트 템플릿(ID: 41377)을 생성한 후 작업 흐름을 생성해야 합니다.

1. VOD 콘솔에 로그인하고 [비디오 처리]>[[태스크 플로우 설정]](https://console.cloud.tencent.com/vod/video-process/taskflow)을 선택하고 [태스크 플로우 생성]을 클릭합니다.
 * [태스크 플로우 이름]: MyTestProcedure를 입력합니다.
 * [구성 항목]: [어댑티브 비트 레이트 스트리밍], [스크린샷 작업] 및 [커버 스크린샷]을 선택합니다.
	 * [어댑티브 비트 레이트 스트리밍 작업 구성] 영역에서 [템플릿 추가]를 클릭하고 ‘어댑티브 비트 레이트 스트리밍 템플릿/ID’에 대해 **1단계**에서 만든 사용자 정의 어댑티브 비트 레이트 스트리밍 템플릿 MyTestTemplate(126866)을 선택합니다.
	 *  [스크린샷 작업 구성] 영역에서 [템플릿 추가]를 클릭하고 ‘스크린샷 캡처 방법’에 대해 [이미지 스프라이트]를 선택하고 ‘스크린샷/ID’에 대해 **2단계**에서 만든 사용자 정의 이미지 스프라이트 템플릿 MyTestTemplate(41377)을 선택합니다.
	 *  [커버 스크린샷 캡처 작업 구성] 영역에서 [템플릿 추가]를 클릭하고 ‘스크린샷 템플릿/ID’로 [TimepointScreenshot]을 선택한 후, [퍼센트]를 선택하고 50%를 입력합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d91b5aeb8c2fe41d844e4c36c0a3d12.png" width="900" />
2. [제출]을 클릭합니다. MyTestProcedure라는 태스크 플로우가 생성됩니다.
![](https://main.qcloudimg.com/raw/e33008c55dcc18bed3b41f96d88c5c8c.png)
3. 콘솔에서 [미디어 자산]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)를 선택하고 대상 비디오(FileId: 528xxx3757278095)를 선택한 후 [비디오 처리]를 클릭합니다.
4. 비디오 처리 팝업 창에서:
 * [처리 유형]에 대해 [태스크 플로우]를 선택합니다.
 * [태스크 플로우 템플릿]에 대해 [MyTestProcedure]를 선택합니다.<span></span>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/649b07dfd248670d057795f3498b61ee.png" width="500" />
5. [확인]을 클릭하고 **비디오 상태**가 ‘처리 중’에서 ‘정상’으로 변경될 때까지 기다리십시오. 이는 비디오 처리가 완료되었음을 나타냅니다.
![](https://main.qcloudimg.com/raw/2894b49729ef223941360f2f814a63fa.png)
6. 비디오의 ‘작업’ 열에서 [관리]를 클릭하여 관리 페이지로 들어갑니다.
 * [기본 정보] 탭에서 생성된 썸네일 및 출력 어댑티브 비트스트림(템플릿 ID: 125866)을 볼 수 있습니다.
 * [스크린샷 정보] 탭에서 생성된 이미지 스프라이트(템플릿 ID: 41377)를 볼 수 있습니다.

## 4단계: Player 구성 생성

사용자 정의 어댑티브 비트스트림 및 이미지 스프라이트를 재생하려면 사용자 정의 플레이어 구성을 사용해야 합니다.

1. VOD 콘솔에 로그인하고 [배포 및 재생 설정]>[[Player 구성]](https://console.cloud.tencent.com/vod/distribute-play/super-player)을 선택하고 [생성]을 클릭합니다.
2. Player 구성 페이지에서 [어댑티브 비트 레이트 스트리밍 템플릿 추가]와 [이미지 스프라이트 템플릿을 추가]를 클릭합니다.
 * [템플릿 이름]: MyTestCfg.
 * ‘어댑티브 비트 레이트 스트리밍 템플릿/ID’에 대해 MyTestTemplate(125866)을 선택합니다.
 * ‘스크린샷 템플릿’으로 MyTestTemplate(41377)을 선택합니다.
<img src="https://main.qcloudimg.com/raw/2459be6bd365e9a5143146d88d44a43c.png" width="400" />
3. [확인]을 클릭하여 Player 구성 MyTestCfg를 생성합니다.

##   5단계: 비디오 재생 미리보기

이전 단계에서 비디오를 처리했습니다. 이제 Web, iOS 및 Android용 Player를 사용하여 비디오 재생을 빠르게 미리 볼 수 있습니다.

1. [[비디오 관리]](https://console.cloud.tencent.com/vod/media)에서 ‘업로드됨’ 탭을 선택하고 이전 단계에서 업로드 및 처리된 비디오를 찾은 다음 ‘작업’ 열에서 [관리]를 클릭하고 ‘Player 미리보기’ 탭을 선택합니다.
2. [재생 구성]에 대해 MyTestCfg를 선택합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4a9ea4b96588c9a2fef0ac82c5ae27e7.png" width="522" />
3. 기본 배포 도메인 이름에 대해 링크 도용 방지가 활성화되어 있으므로 [재생 제어] 탭에서 링크 도용 방지 만료 시간 및 미리 보기 기간을 설정할 수 있습니다. 여기에서 기본 매개변수 설정을 사용할 수 있습니다(재생 링크 도용 방지의 기본 만료 시간은 1일이며 재생에 허용된 미리보기 기간 및 최대 IP 수는 비어 있음).
 <img src="https://qcloudimg.tencent-cloud.cn/raw/b5d25e5c5cd9f55cf14be336f4abd967.png" width="522" />
4. [Web 플레이어]에서 플레이어 중앙에 있는 버튼을 클릭하면 Web에서 동영상을 재생할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />
5. [모바일 플레이어]에서 [코드 스캔하여 다운로드]를 클릭하여 ‘Tencent Cloud Toolkit’을 설치합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0e72b414ee3dc8084dda39d8a5d5c91.png" width="522" />
6. 휴대폰에서 Tencent Cloud Toolkit을 열고 [Player]를 선택하고 오른쪽 상단 모서리를 클릭하여 QR 코드를 스캔하면 휴대폰에서 비디오를 재생할 수 있습니다.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/06e77f14c2e1020e8936ce1ab30a6ca3.png" width="422" />

##  6단계: 검증을 위해 Demo 사용

링크 도용 방지가 활성화된 후 Player는 비디오를 재생하기 위해 유효 기간 내에 서명이 필요합니다. 서명 툴을 사용하여 아래와 같이 서명을 빠르게 생성할 수 있습니다.

1. [Player - 서명 생성 툴](https://vods.cloud.tencent.com/signature/super-player-sign.html) 페이지로 이동하고 다음 매개변수를 입력합니다.
 * [사용자 appId]: 비디오 1400xxx357의 appId(서브 애플리케이션을 사용하는 경우 서브 애플리케이션의 appId 입력).
 * [비디오 fileId]: 비디오 fileId, 즉 528xxx3757278095입니다.
 * [현재 Unix 타임스탬프]: 툴에 의해 자동으로 생성된 현재 Unix 시간으로, 수동으로 입력할 필요가 없으며 여기에서 1591756516입니다.
 * [Player 구성]: 사용자 정의 Player 구성 이름(여기서는 MyTestCfg)입니다.
 * [서명 만료 Unix 타임스탬프]: 서명 만료 시간으로, 비워둘 수 있습니다. 서명은 기본적으로 하루 후에 만료됩니다.
 * [링크 만료 시간]: 6시간 후 16진법 Unix 시간으로 설정할 수 있는 Key 링크 도용 방지의 만료 시간: 5ee09b44.
 * [링크 도용 방지 Key]: 이전에 획득한 링크 도용 방지 Key인 2WExxx48eW입니다.
2. [서명 생성]을 클릭하면 생성된 서명이 ‘서명 생성 결과’ 텍스트 상자에 표시됩니다.

Player 서명을 받은 후 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android) 및 [iOS](https://github.com/LiteAVSDK/Player_iOS)용 Player Demo를 사용하여 확인할 수 있습니다. 자세한 내용은 Demo 소스 코드를 참고하십시오.
>? 콘솔의 [미디어 자산]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)>[Player 미리 보기]에서 참고용으로 비디오 미리 보기에 해당하는 Web 플레이어 소스 코드를 얻을 수 있습니다.
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## 결론

이제 Player가 재생하는 비디오의 콘텐츠와 스타일을 사용자 정의하는 방법을 학습 완료했습니다.
동영상을 암호화하고 암호화된 동영상을 재생하려면 [4단계: 암호화된 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38294)을 참고하십시오.
