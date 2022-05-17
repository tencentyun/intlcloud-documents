## 학습 목표

본 문서에서는 비디오를 암호화하고 Superplayer를 사용하여 암호화된 비디오를 재생하는 방법을 설명합니다.

본 문서를 읽기 전에 Superplayer 가이드의 [1단계: Superplayer로 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38098) 및 [2단계: 링크 도용 방지가 활성화된 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38292)을 읽었는지 확인하십시오. 이 문서는 [1단계](https://intl.cloud.tencent.com/document/product/266/38098)에서 활성화된 계정과 업로드된 동영상을 사용하며 [2단계](https://intl.cloud.tencent.com/document/product/266/38292)에 따라 링크 도용 방지를 활성화합니다.

## 1단계: 비디오 암호화
1. VOD 콘솔에서 [미디어 자산]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)를 선택하고 대상 비디오(FileId: 528xxx3757278095)를 선택한 후 [비디오 처리]를 클릭합니다.
2. 비디오 처리 페이지에서:
 * [처리 유형]에 대해 [작업 흐름]을 선택합니다.
 * [작업 흐름 템플릿]에 대해 [SimpleAesEncryptPreset]을 선택합니다.
<img src="https://main.qcloudimg.com/raw/4cc8649c21b5c60305b925120f84d7e6.png" width="" /><span>
>? 
>- SimpleAesEncryptPreset은 어댑티브 비트레이트 스트리밍을 위한 템플릿 12, 썸네일 생성을 위한 템플릿 10, 이미지 스프라이트 캡처를 위한 템플릿 10을 사용하는 사전 설정 작업 흐름입니다.
>- 템플릿 12를 사용한 어댑티브 비트 레이트 스트리밍은 암호화된 다중 비트 레이트 스트림을 출력하는 것입니다.
3. [확인]을 클릭하고 ‘비디오 상태’가 ‘처리 중’에서 ‘정상’으로 변경될 때까지 기다리십시오. 이는 비디오 처리가 완료되었음을 나타냅니다.
![](https://main.qcloudimg.com/raw/885b68427d36faefe8f2bb5b489e1e19.png)
4. 비디오의 ‘작업’ 열에서 [관리]를 클릭하여 관리 페이지로 들어갑니다.
 * ‘기본 정보’ 탭을 클릭하면 생성된 썸네일 및 출력 암호화된 적응 비트스트림(템플릿 ID: 12)을 볼 수 있습니다.
 * ‘스크린샷 정보’ 탭을 클릭하면 생성된 이미지 스프라이트(템플릿 ID: 10)를 볼 수 있습니다.


##  2단계: 비디오 재생 미리보기

이전 단계에서 비디오를 업로드하고 처리했습니다. 이제 Web, iOS 및 Android용 Superplayer를 사용하여 비디오 재생을 빠르게 미리 볼 수 있습니다.

1. [미디어 자산]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)를 선택하고 **1단계**에서 업로드 및 처리된 비디오를 찾은 다음 ‘작업’ 열에서 [관리]를 클릭하고 [Superplayer 미리보기]를 선택합니다.
2. [Superplayer 구성]은 basicDrmPreset을 선택합니다.

 >? 템플릿 12가 있는 어댑티브 비트스트림과 템플릿 10이 있는 이미지 스프라이트를 출력하는 데 사용되는 Superplayer를 구성합니다.
3. 기본 배포 도메인 이름에 대해 링크 도용 방지가 활성화되어 있으므로 [재생 제어] 탭에서 링크 도용 방지 만료 시간 및 미리 보기 기간을 설정할 수 있습니다. 여기에서 기본 매개변수 설정을 사용할 수 있습니다(재생 링크 도용 방지의 기본 만료 시간은 1일이며 재생에 허용된 미리보기 기간 및 최대 IP 수는 비어 있음).
 
4. [Web 플레이어]에서 플레이어 중앙에 있는 버튼을 클릭하면 Web에서 동영상을 재생할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />


## 3단계: 검증을 위해 Demo 사용

Superplayer는 암호화된 비디오를 재생하기 위해 유효 기간 내에 서명이 필요합니다. 서명 툴을 사용하여 아래와 같이 서명을 빠르게 생성할 수 있습니다.

1. [Superplayer - 서명 생성 툴](https://vods.cloud.tencent.com/signature/super-player-sign.html) 페이지로 이동하고 다음 매개변수를 입력합니다.
 * [사용자 appId]: 비디오 1400xxx357의 appId(서브 애플리케이션을 사용하는 경우 서브 애플리케이션의 appId 입력).
 * [비디오 fileId]: 비디오 fileId, 즉 528xxx3757278095입니다.
 * [현재 Unix 타임스탬프]: 툴에 의해 자동으로 생성된 현재 Unix 시간(1591756516)으로, 수동으로 입력할 필요가 없습니다.
 * [Superplayer 구성]: 사전 설정 Superplayer 구성 이름: basicDrmPreset.
 * [서명 만료 Unix 타임스탬프]: 서명 만료 시간으로, 비워둘 수 있습니다. 서명은 기본적으로 1일 후에 만료됩니다.
 * [URL 만료 시간]: 6시간 후 16진법 Unix 시간으로 설정할 수 있는 Key 링크 도용 방지 만료 시간: 5ee09b44.
 * [링크 도용 방지 Key]: 이전에 획득한 링크 도용 방지 Key인 2WExxx48eW입니다.
>!basicDrmPreset은 템플릿 12로 어댑티브 비트스트림을 출력하고 템플릿 10으로 이미지 스프라이트를 출력하는 데 사용되는 사전 설정된 Superplayer 구성입니다.
2. [서명 생성]을 클릭하면 생성된 서명이 [서명 생성 결과] 텍스트 상자에 표시됩니다.


Superplayer 서명을 받은 후 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/tencentyun/SuperPlayer_Android) 및 [iOS](https://github.com/tencentyun/SuperPlayer_iOS)용 Superplayer Demo를 사용하여 확인할 수 있습니다. 자세한 내용은 Demo 소스 코드를 참고하십시오.
>?콘솔의 [미디어 자산]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)>[Superplayer 미리 보기]에서 참고용으로 비디오 미리 보기에 해당하는 Web 플레이어 소스 코드를 얻을 수 있습니다.
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## 결론

이제 비디오를 암호화하고 Superplayer를 사용하여 암호화된 비디오를 재생하는 방법을 학습 완료했습니다.
