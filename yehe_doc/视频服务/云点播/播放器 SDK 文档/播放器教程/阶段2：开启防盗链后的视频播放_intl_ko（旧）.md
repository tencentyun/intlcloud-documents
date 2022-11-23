## 학습 목표

VOD는 유효 기간, 시청자 수, 재생 시간 등을 설정할 수 있는 링크 도용 방지 구성을 지원합니다. 이 문서에서는 Player를 사용하여 링크 도용 방지가 활성화된 비디오를 재생하는 방법을 설명합니다.

본 문서를 읽기 전에 Player 가이드의 [1단계: Player로 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38098)을 읽었는지 확인하십시오. 이 문서는 활성화된 계정과 [1단계](https://intl.cloud.tencent.com/document/product/266/38098)에서 업로드된 동영상을 사용합니다.

## 1단계: 링크 도용 방지 활성화

아래 예시는 계정 아래의 기본 배포 도메인에 대한 Key 링크 도용 방지를 활성화하는 방법을 보여줍니다.
>! 프로덕션 환경에서 도메인 이름에 대한 링크 도용 방지를 직접 활성화하지 마십시오. 그렇지 않으면 프로덕션 환경에서 비디오 재생이 실패할 수 있습니다.

1. VOD 콘솔에 로그인하여 [배포 및 재생]>[[도메인 이름]](https://console.cloud.tencent.com/vod/distribute-play/domain)을 선택하고 ‘기본 배포 도메인’을 찾아 오른쪽의 [설정]을 클릭합니다.
<img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. ‘Key 링크 도용 방지’ 우측의 [편집]을 클릭하여 [Key 링크 도용 방지]를 열고 [랜덤 Key 생성](2WExxx48eW)합니다. 생성된 키를 복사하고 [확인]을 클릭하여 구성을 저장 및 적용합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## 2단계: 비디오 재생 미리보기

이전 단계에서 기본 배포 도메인 이름에 대해 링크 도용 방지를 활성화했습니다. 이제 Web, iOS 및 Android용 Player를 사용하여 비디오 재생을 빠르게 미리 볼 수 있습니다.

1. [미디어 자산]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)를 선택하고 **1단계**에서 업로드 및 처리된 비디오를 찾은 다음 ‘작업’ 열에서 [관리]를 클릭하고 [Player 미리보기]를 선택합니다.
2. [Player 구성]에 대해 default를 선택합니다.
>? default는 템플릿 10으로 어댑티브 비트스트림을 출력하고 템플릿 10으로 이미지 스프라이트를 출력하는 데 사용되는 사전 설정된 Player 구성입니다.

 <img src="https://qcloudimg.tencent-cloud.cn/raw/e66e46d10480c5fb00a2881b275a9cdc.png" width="660" />
3. 기본 배포 도메인 이름에 대해 링크 도용 방지가 활성화되어 있으므로 [재생 제어] 탭에서 링크 도용 방지 만료 시간 및 미리 보기 기간을 설정할 수 있습니다. 여기에서 기본 매개변수 설정을 사용할 수 있습니다(재생 링크 도용 방지의 기본 만료 시간은 1일이며 재생에 허용된 미리보기 기간 및 최대 IP 수는 비어 있음).
 <img src="https://qcloudimg.tencent-cloud.cn/raw/f08e553a9519fb9974935374f4b4051d.png" width="662" />
4. [Web 플레이어]에서 플레이어 중앙에 있는 버튼을 클릭하면 Web에서 동영상을 재생할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />
5. [모바일 플레이어]에서 [코드 스캔하여 다운로드]를 클릭하여 ‘Tencent Cloud Toolkit’을 설치합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0e72b414ee3dc8084dda39d8a5d5c91.png" width="522" />
6. 휴대폰에서 Tencent Cloud Toolkit을 열고 [Player]를 선택한 후 오른쪽 상단 모서리를 클릭하여 QR 코드를 스캔하면 휴대폰에서 비디오를 재생할 수 있습니다.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/06e77f14c2e1020e8936ce1ab30a6ca3.png" width="422" />

## 3단계: 검증을 위해 Demo 사용

링크 도용 방지가 활성화된 후 Player는 비디오를 재생하기 위해 유효 기간 내에 서명이 필요합니다. 서명 툴을 사용하여 서명을 빠르게 생성할 수 있습니다.

1. [Player - 서명 생성 툴](https://vods.cloud.tencent.com/signature/super-player-sign.html) 페이지로 이동하고 다음 매개변수를 입력합니다.

 * [사용자 appId]: 비디오 1400xxx357의 appId(서브 애플리케이션을 사용하는 경우 서브 애플리케이션의 appId 입력).
 * [비디오 fileId]: 비디오 fileId, 즉 528xxx3757278095입니다.
 * [현재 Unix 타임스탬프]: 도구에 의해 자동으로 생성된 현재 Unix 시간으로, 수동으로 입력할 필요가 없으며 여기서는 1591516390입니다.
 * [서명 만료 Unix 타임스탬프]: 서명 만료 시간으로, 비워둘 수 있습니다. 서명은 기본적으로 하루 후에 만료됩니다.
 * [링크 만료 시간]: 6시간 후 16진법 Unix 시간으로 설정할 수 있는 Key 링크 도용 방지의 만료 시간은 5edcf146입니다.
 * [링크 도용 방지 Key]: 이전 단계에서 얻은 링크 도용 방지 Key인 2WExxx48eW입니다.

2. [서명 생성]을 클릭하면 생성된 서명이 ‘서명 생성 결과’ 텍스트 상자에 표시됩니다.

Player 서명을 받은 후 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html), [Android](https://github.com/LiteAVSDK/Player_Android) 및 [iOS](https://github.com/LiteAVSDK/Player_iOS) Player Demo를 사용하여 확인할 수 있습니다. 자세한 내용은 Demo 소스 코드를 참고하십시오.
>?콘솔의 [미디어 자산]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)>[Player 미리 보기]에서 참고용으로 비디오 미리 보기에 해당하는 Web 플레이어 소스 코드를 얻을 수 있습니다.
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## 결론

이제 Player를 사용하여 링크 도용 방지가 활성화된 비디오를 재생하는 방법을 학습 완료했습니다.

또한:
- [3단계: 재생 콘텐츠 및 스타일 사용자 정의](https://intl.cloud.tencent.com/document/product/266/38293)에 설명된 대로 동영상 재생 콘텐츠 및 스타일을 사용자 정의합니다.
- [4단계: 암호화된 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38294)의 설명에 따라 동영상을 암호화하고 암호화된 동영상을 재생합니다.
