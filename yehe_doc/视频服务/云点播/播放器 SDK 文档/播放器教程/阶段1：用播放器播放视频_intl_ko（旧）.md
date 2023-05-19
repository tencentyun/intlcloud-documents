## 학습 목표
이 문서는 비디오를 VOD에 업로드 및 처리하고 Player에서 재생하는 방법을 설명합니다.

## 전제 조건
시작하기 전에 다음을 수행하십시오.

### VOD 활성화
VOD를 활성화하려면 다음 단계를 따르십시오.

1. [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985) 및 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)을 완료합니다.
2. VOD 서비스를 구매합니다. 자세한 내용은 [과금 개요](https://intl.cloud.tencent.com/document/product/266/2838)를 참고하십시오.
3. **클라우드 서비스**>**비디오 서비스**>[**VOD**](https://console.cloud.tencent.com/vod)를 선택하여 VOD 콘솔로 이동합니다.

이제 VOD가 활성화됐습니다.

### 링크 도용 방지 비활성화

기본 배포 도메인 이름에 대한 링크 도용 방지가 활성화되어 있지 않은지 확인해야 합니다.

1. VOD 콘솔에 로그인하여 **배포 및 재생 설정** >[ **도메인 이름** ](https://console.cloud.tencent.com/vod/distribute-play/domain)을 선택한 후 ‘기본 배포 도메인’ 항목에서 **설정**을 클릭하여 설정 페이지로 들어갑니다.
<img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. ‘Referer 링크 도용 방지’ 및 ‘Key 링크 도용 방지’의 상태가 모두 ‘비활성화’인지 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/12689eb5bed63fc76cd7d88e38907c09.png)


## 1단계: 비디오 업로드 및 처리
이 단계에서는 비디오를 업로드하고 어댑티브 비트스트림으로 트랜스코딩하고 썸네일 및 이미지 스프라이트를 생성하는 방법을 설명합니다.

1. VOD 콘솔에 로그인하고 **미디어 자산**>[ **비디오 관리** ](https://console.cloud.tencent.com/vod/media)를 선택하고 **비디오 업로드**를 클릭합니다.
![](https://main.qcloudimg.com/raw/b1ad4f0706ad1cd24044c8420a759868.png)
2. 업로드 페이지에서 **로컬 업로드**를 선택하고 **비디오 선택**을 클릭하여 로컬 비디오를 업로드하고 다른 필드를 다음과 같이 설정합니다.
	- **비디오 처리**에서 **업로드 후 자동 처리**를 선택합니다.
	- **처리 유형**은 **태스크 플로우**를 선택합니다.
	- **태스크 플로우 템플릿**에 대해 **LongVideoPreset**을 선택합니다.
>? LongVideoPreset은 어댑티브 비트 레이트 스트리밍, 썸네일 생성 및 이미지 스프라이트 캡처를 위해 템플릿 10을 사용하는 사전 설정 태스크 플로우입니다.

![](https://qcloudimg.tencent-cloud.cn/raw/56e6b4249722884eed34b167d6e6d6ed.png)
3. **업로드**를 클릭하여 ‘업로드 중’ 페이지로 이동하고 업로드가 완료될 때까지 기다립니다.
4. **미디어 자산**>[**비디오 관리**](https://console.cloud.tencent.com/vod/media)를 선택하고 새로 업로드된 비디오를 찾습니다(FileId: 528xxx3757278095). 여기서 ID는 업로드된 비디오의 FileId입니다.
![](https://main.qcloudimg.com/raw/f2b3744a3c42a07863db0b7545dd892f.png)
>? 비디오 상태가 **처리 중**에서 **정상**으로 변경되면 ‘비디오 처리’가 완료된 것입니다. 잠시만 기다려 주십시오.

5. 새로 업로드된 비디오의 ‘작업’ 열에서 **관리**를 클릭하여 관리 페이지로 이동합니다.
 - ‘기본 정보’ 탭을 클릭하면 생성된 썸네일 및 출력 어댑티브 비트스트림(템플릿 ID: 10)을 볼 수 있습니다.
 - 생성된 이미지 스프라이트(템플릿 ID: 10)를 보려면 ‘스크린샷 정보’ 탭을 클릭합니다.

## 2단계: 비디오 재생 미리보기

이전 단계에서 비디오를 업로드하고 처리했습니다. 이제 web, iOS 및 Android용 Player를 사용하여 비디오 재생을 빠르게 미리 볼 수 있습니다.

1. **미디어 자산**>[**비디오 관리**](https://console.cloud.tencent.com/vod/media)를 선택하고 **1단계**에서 업로드 및 처리된 비디오를 찾은 다음 ‘작업’ 열에서 **관리**를 클릭하고 **Player 미리보기**를 선택합니다.
2. **Player 구성**에 대해 default를 선택합니다.
>? default는 템플릿 10으로 어댑티브 비트스트림을 출력하고 템플릿 10으로 이미지 스프라이트를 출력하는 데 사용되는 사전 설정된 Player 구성입니다.

 <img src="https://main.qcloudimg.com/raw/17e2552964195c6919239d2d13a0d012.png" width="660" />
4. **Web 플레이어**에서 플레이어 중앙에 있는 버튼을 클릭하면 Web에서 동영상을 재생할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />
5. **모바일 플레이어**에서 **코드 스캔하여 다운로드**를 클릭하여 ‘Tencent Cloud Toolkit’을 설치합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/439e632cb867b96a3334eb2823b2e235.png" width="522" />
6. 휴대폰에서 Tencent Cloud Toolkit을 열고 **Player**를 선택하고 오른쪽 상단 모서리를 클릭하여 QR 코드를 스캔하면 휴대폰에서 비디오를 재생할 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/06e77f14c2e1020e8936ce1ab30a6ca3.png" width="422" />

## 3단계: Demo 체험

[Web](https://tcplayer.vcube.tencent.com/intl/index.html), [Android](https://github.com/LiteAVSDK/Player_Android) 및 [iOS](https://github.com/LiteAVSDK/Player_iOS) Player Demo를 사용하여 확인을 진행할 수 있습니다. 자세한 내용은 Demo 소스 코드를 참고하십시오.
>?콘솔의 **미디어 자산** >[ **비디오 관리** ](https://console.cloud.tencent.com/vod/media)> **Player 미리 보기**에서 참고용으로 비디오 미리 보기에 해당하는 Web 플레이어 소스 코드를 얻을 수 있습니다.
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## 결론

이제 VOD에 비디오를 업로드 및 처리하고 Player에서 재생하는 방법을 학습 완료했습니다.

또한:
- [2단계: 링크 도용 방지가 활성화된 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38292)의 설명에 따라 비디오 재생을 위한  Key 링크 도용 방지를 활성화합니다.
- [3단계: 재생 콘텐츠 및 스타일 사용자 정의](https://intl.cloud.tencent.com/document/product/266/38293)에 설명된 대로 동영상 재생 콘텐츠 및 스타일을 사용자 정의합니다.
- [4단계: 암호화된 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38294)의 설명에 따라 동영상을 암호화하고 암호화된 동영상을 재생합니다.
