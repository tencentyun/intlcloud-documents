## 작업 시나리오
서버에서 비디오 업로드는 App 백엔드에서 VOD 플랫폼에 비디오를 업로드하는 것을 의미하며, 본문은 서버 API를 사용하여 비디오를 업로드하는 방법을 설명합니다.

## 전제 조건

#### 1. 서비스 활성화

VOD 서비스 활성화에 대한 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/266/39506)를 참고하십시오.

#### 2. Tencent Cloud API 키 가져오기

SecretId, SecretKey와 같은 서버 API 호출에 필요한 보안 자격 증명을 가져옵니다. 자세한 방법은 다음과 같습니다.
1. 콘솔에 로그인하고 [클라우드 서비스]>[CAM]>[[API 키 관리]](https://console.cloud.tencent.com/cam/capi)를 선택해 ‘API 키 관리’ 페이지로 이동합니다.
2. Tencent Cloud API 키를 받습니다. 아직 키를 생성하지 않은 경우, [키 생성]을 클릭하면 한 쌍의 SecretId와 SecretKey가 생성됩니다.

## 작업 단계
### 1. 업로드 시작

업로드는 SDK 또는 API를 통해 시작할 수 있습니다.

#### SDK를 통한 업로드 시작

개발 환경에서 업로드 기능을 용이하게 하기 위해 VOD는 다양한 프로그래밍 언어에 대한 SDK를 제공합니다. 각 언어에 대한 SDK는 해당 Demo와 함께 제공됩니다. 자세한 내용은 다음을 참고하십시오.
- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916)
- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)
- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918)
- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919)
- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915)

#### API를 통한 업로드 시작

VOD에서 제공하는 업로드 SDK가 App 백엔드에서 사용하는 프로그래밍 언어에 적용되지 않는 경우 App 백엔드는 동영상 업로드를 위해 VOD 서버 API를 호출해야 합니다(이 방법은 더 복잡하고 권장하지 않습니다). 업로드 프로세스는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/005ec15acf74e0a428e8d328ffd2da2f.png)
API 기반 업로드는 업로드 신청, 파일 업로드 등의 단계를 직접 구현해야 하므로 SDK 기반 업로드만큼 편리하지 않습니다. 또한 대용량 파일을 업로드하려면 멀티파트 업로드 로직을 개발해야 합니다. 자세한 내용은 다음을 참고하십시오.

- [서버 API - 업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120)
- [서버 API - 파일 업로드](https://intl.cloud.tencent.com/document/product/266/33913)
- [서버 API - 업로드 확인](https://intl.cloud.tencent.com/document/product/266/34119)

#### 고급 기능

- **업로드 중 태스크 플로우 지정**
비디오 업로드 완료 시 트랜스코딩 및 화면 캡처와 같은 [비디오 처리 태스크 플로우](https://intl.cloud.tencent.com/document/product/266/33931)를 자동으로 시작하려면 서버 API [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120)을 호출할 때 `Procedure` 매개변수를 지정할 수 있으며 매개변수 값은 원하는 태스크 플로우 템플릿의 이름이어야 합니다. VOD는 [태스크 플로우 템플릿 생성](https://intl.cloud.tencent.com/document/product/266/14058) 및 이름 지정을 지원합니다. 태스크 플로우를 시작할 때 태스크 플로우 템플릿 이름을 사용하여 원하는 작업을 나타낼 수 있습니다. 다양한 프로그래밍 언어에 대해 VOD에서 제공하는 모든 SDK는 태스크 플로우 매개변수 지정을 지원합니다. 자세한 내용은 다음을 참고하십시오.
	- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Node.js SDKSDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
- **업로드 시 스토리지 리전 지정**
VOD에서 제공하는 스토리지 리전은 기본적으로 싱가포르이며, 다른 리전에 파일을 저장하려면 콘솔에서 활성화해야 합니다. 자세한 내용은 [스토리지 설정 업로드](https://intl.cloud.tencent.com/document/product/266/18874)를 참고하십시오. 설정 후 서버 API [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120) 호출 시 `StorageRegion` 파라미터로 스토리지지 리전을 지정할 수 있으며, 파라미터 값은 리전 [영어 약칭](https://intl.cloud.tencent.com/document/product/266/9760)이어야 합니다. 다양한 프로그래밍 언어에 대해 VOD에서 제공하는 모든 SDK는 업로드 시 스토리지 리전 지정을 지원합니다. 자세한 내용은 다음을 참고하십시오.
	- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Node.js SDKSDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	
### 2. 이벤트 알림

비디오 업로드가 완료되면 VOD는 App 백엔드에 [이벤트 알림 - 비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950)를 전송하고, App 백엔드는 해당 이벤트를 통해 동영상 업로드 동작을 인식하게 됩니다. 이벤트 알림을 수신하려면 App의 [콘솔 - 콜백 설정](https://console.cloud.tencent.com/vod/callback)에서 이벤트 공지를 활성화해야 합니다. [이벤트 공지 - 비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950)에는 주로 다음과 같은 정보가 포함되어 있습니다.
- 새로운 비디오 파일의 FileId와 URL.
- VOD는 비디오 업로드 시 통과 필드 지정을 지원하며 이벤트 완료 시 통과 필드를 App 백그라운드에 공지합니다. 이벤트 공지에는 다음 필드가 포함됩니다.
	- `SourceType`: 해당 필드는 필드는 항상 `ServerUpload`이며 업로드가 서버에서 시작되었음을 나타냅니다.
	- `SourceContext`: 서명의 `sourceContext` 매개변수에 해당하는 서명 배포 중 애플리케이션 백엔드에서 지정한 사용자 지정 통과 필드입니다.
- VOD는 비디오 업로드 완료 시 자동 영상 처리를 지원합니다. 업로드 시 [비디오 처리 태스크 플로우](https://intl.cloud.tencent.com/document/product/266/33931)를 지정한 경우, 이벤트 공지 내용에 작업 ID가 포함되며, 이는 이벤트 알림의 `data.procedureTaskId`필드에 해당합니다.

더 자세한 정보는 다음을 참고하십시오.
- [작업 관리 및 이벤트 알림](https://intl.cloud.tencent.com/document/product/266/33931)
- [이벤트 알림 - 비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950)



