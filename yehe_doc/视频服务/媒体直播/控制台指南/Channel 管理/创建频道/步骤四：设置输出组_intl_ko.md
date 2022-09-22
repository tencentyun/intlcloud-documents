StreamLive는 다양한 유형의 출력을 지원합니다. 이 문서에서는 출력 및 출력 그룹을 생성하는 방법을 보여줍니다.

## 채널에 대한 다중 출력 그룹 구성
**더하기** 아이콘을 클릭하여 채널에 대해 여러 Output Group을 구성할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3e13eac666167d0f867e51e8a97cc1f0.png)

## 출력 그룹의 이름 및 유형 설정
Output Group의 이름과 유형을 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6b239c37c95f0cc226bc93e12a481395.png)
현재 지원되는 출력 유형은 HLS, DASH, HLS_STREAM_PACKAGE, DASH_STREAM_PACKAGE, HLS_ARCHIVE 및 DASH_ARCHIVE입니다.

- HLS 및 DASH 출력은 HTTP PUT을 통해 Destination으로 전송됩니다.
- HLS_STREAM_PACKAGE 및 DASH_STREAM_PACKAGE 출력은 현재 계정의 [StreamPackage](https://intl.cloud.tencent.com/document/product/1048/45219)로 전송됩니다. 출력을 원본 서버로 사용하여 CDN을 통해 콘텐츠를 스트리밍할 수 있습니다.
- HLS_ARCHIVE 및 DASH_ARCHIVE 출력은 [Tencent Cloud COS](https://intl.cloud.tencent.com/document/product/1048/45218)에 저장됩니다.

## Destinations 구성
- 출력 유형이 HLS 또는 DASH인 경우 푸시할 CDN URL을 입력합니다. URL에 인증이 필요한 경우 인증 정보도 입력하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/e76f39828aade1c04c31b17e521220ed.png)
- 출력 유형이 HLS_STREAM_PACKAGE 또는 DASH_STREAM_PACKAGE인 경우 StreamLive를 푸시할 **StreamPackage Channel Id**를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/05cae1db0fcfe74a723a0d828e3f5485.png)
- 출력 유형이 HLS_ARCHIVE 또는 DASH_ARCHIVE인 경우 **COS Destination**을 입력하여 출력을 저장합니다. StreamLive는 지난 7일 동안의 라이브 스트림을 COS에 저장합니다(다시 시작한 후 데이터를 덮어씁니다)
![](https://qcloudimg.tencent-cloud.cn/raw/15f727c5101320835259eeb4b0f82529.png)

## DRM 설정
StreamLive는 DRM(CustomDRMKeys 및 SDMCDRM)을 지원합니다. 이 기능을 활성화하는 방법에 대한 자세한 지침은 [DRMtoday를 사용하여 채널에 DRM 설정하기](https://intl.cloud.tencent.com/document/product/1048/45217)를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/8d81955db11e160cb0be5e2a8ed9226a.png)

## 트랜스코딩 템플릿 구성
Joint 또는 Separate 트랜스코딩 템플릿을 구성할 수 있습니다. HLS 출력의 경우 Separate 트랜스코딩을 통해 다른 오디오 트랙을 결합할 수 있습니다. 이것이 필요하지 않은 경우 Joint 트랜스코딩 템플릿을 사용하는 것이 좋습니다.
- Joint 트랜스코딩 템플릿에는 오디오 및 비디오 트랜스코딩에 대한 설정이 모두 포함되어 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5567d7eff345ae787a98f4e5c0692bc9.png)
- Separate 트랜스코딩을 사용하는 경우 오디오 및 비디오 트랜스코딩 매개변수를 별도로 설정해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/aa81355608bc2ad72eab06e043a88fb3.png)
![](https://qcloudimg.tencent-cloud.cn/raw/00196f0a0566111d33a4aef484809110.png)
>!  **Top Speed Codec Transcoding**은 Tencent Cloud 비디오 팀에서 개발한 고성능 트랜스코딩 서비스입니다. AI 알고리즘을 활용하여 최상의 인코딩 매개변수를 동적으로 결정함으로써 낮은 비트 레이트, 고품질 트랜스코딩을 제공합니다. **Bitrate Compression Ratio**는 감소될 것으로 예상되는 비디오 비트 레이트의 백분율입니다.

### 출력 구성
- Joint 트랜스코딩 템플릿을 구성하는 경우 각 Output에 대해 하나의 템플릿만 선택할 수 있으며 이는 다중 비트 레이트 스트리밍에서 하나의 스트림으로 사용됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b007445cb3f47a9ec6d827f959cff9ba.png)
- Separate 트랜스코딩 템플릿을 구성하는 경우 각 출력에 대해 하나의 비디오 트랜스코딩 템플릿과 여러 오디오 트랜스코딩 템플릿을 선택할 수 있습니다. 비디오 트랜스코딩 템플릿은 다중 비트 레이트 스트리밍에서 한 스트림에 대한 트랜스코딩 매개변수를 지정하는 반면 오디오 트랜스코딩 템플릿은 스트림이 사용할 수 있는 오디오 트랙에 대한 매개변수를 지정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8b758ded635531a9a24f1aae51eb9828.png)

### 구성 저장
**Done**을 클릭하여 구성을 저장합니다. 이것으로 채널 구성을 마칩니다. 그런 다음 [Start]를 클릭하여 채널을 시작할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a596817ccf73cd4573f83e3d572fcbee.png)