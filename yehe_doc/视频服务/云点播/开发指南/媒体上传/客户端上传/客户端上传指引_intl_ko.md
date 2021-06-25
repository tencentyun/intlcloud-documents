## 작업 시나리오
클라이언트 비디오 업로드란 App의 최종 사용자가 로컬 비디오를 VOD 플랫폼에 업로드하는 것을 의미하며, 프로세스는 아래 이미지와 같습니다. 본 문서에서는 클라이언트를 사용한 비디오 업로드 방법에 대해 소개합니다.
![](https://main.qcloudimg.com/raw/6d4c9f32e257ca84fda505d5307c856e.png)

## 전제 조건

#### 1. 서비스 활성화

VOD 서비스 활성화에 대한 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/266/39506)를 참조하십시오.

#### [](id:p3)2. Tencent Cloud API 키 획득
 
SecretId와 SecretKey와 같은 서버 API 호출에 필요한 보안 자격 증명을 가져옵니다. 자세한 방법은 다음과 같습니다.
1. 콘솔에 로그인하고 [클라우드 서비스]>[CAM]>[[API 키 관리]](https://console.cloud.tencent.com/cam/capi)를 선택해 ‘API 키 관리’ 페이지로 이동합니다.
2. Tencent Cloud API 키를 받습니다. 아직 키를 생성하지 않은 경우, [키 생성]을 클릭하면 한 쌍의 SecretId와 SecretKey가 생성됩니다.
  
## 작업 순서
### 1. 서명 업로드 신청
클라이언트는 App의 서명 배포 서버에 서명 업로드를 신청해야 합니다. 서명 생성 순서는 [클라이언트 서명 업로드](https://intl.cloud.tencent.com/document/product/266/33922)를 참조하십시오. 다음은 다양한 프로그래밍 언어의 서명 생성 예시입니다:
- [PHP 서명 예시](https://intl.cloud.tencent.com/document/product/266/33923)
- [Java 서명 예시](https://intl.cloud.tencent.com/document/product/266/33923)
- [Node.js 서명 예시](https://intl.cloud.tencent.com/document/product/266/33923)
- [C# 서명 예시](https://intl.cloud.tencent.com/document/product/266/33923)
- [Python 서명 예시](https://intl.cloud.tencent.com/document/product/266/33923)

>?
>- 클라이언트 업로드는 비디오 파일을 클라이언트에서 VOD 플랫폼으로 직접 업로드하는 것으로, App 서비스를 거칠 필요가 없습니다. 따라서 VOD는 반드시 요청을 전송한 클라이언트에 대한 인증을 진행해야 합니다.
>- SecretKey 권한이 너무 커 App이 해당 정보를 클라이언트에 유출할 수 없습니다. 그렇지 않으면 심각한 보안 문제를 야기할 수 있으므로 클라이언트는 업로드를 시작하기 전에 서명 업로드를 신청해야 합니다.


### 2. SDK를 사용한 비디오 업로드

VOD는 클라이언트에서 편리하게 비디오를 업로드할 수 있도록 멀티 플랫폼 SDK를 제공하여 클라이언트가 손쉽게 액세스할 수 있도록 합니다. 자세한 내용은 다음을 참조하십시오.
- [Android 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33925)
- [iOS 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33926)
- [Web 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33924)

#### FAQ 
- **비디오 업로드 완료 후 자동으로 트랜스 코딩을 시작하려면 어떻게 해야 하나요**?
클라이언트 업로드 서명의 `procedure` 매개변수를 통해 업로드 완료 후의 처리 방식을 지정합니다. 자세한 내용은 [업로드 시 작업 프로세스 지정](#p1)을 참조하십시오.
- **App 백그라운드에서 비디오 업로드 완료 공지 수신 후 업로드한 클라이언트를 식별하는 방법은 무엇인가요**?
클라이언트 업로드 서명에 `sourceContext` 매개변수를 추가하면 해당 매개변수가 사용자의 신상정보를 전달하며 업로드 완료 공지가 해당 매개변수를 App 백그라운드로 전달합니다. 자세한 내용은 [이벤트 공지](#p2)를 참조하십시오.

### [](id:p2)3. 이벤트 공지

비디오 업로드가 완료되면 VOD는 App 백그라운드에 [이벤트 공지 - 비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950)를 전송하고, App 백그라운드는 해당 이벤트를 통해 동영상 업로드 동작을 인식하게 됩니다. 이벤트 공지를 수신하려면 App의 [콘솔 - 콜백 설정](https://console.cloud.tencent.com/vod/callback)에서 이벤트 공지를 활성화해야 합니다. [이벤트 공지 - 비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950)에는 주로 다음과 같은 정보가 포함되어 있습니다.
- 새로운 비디오 파일의 FileId와 URL
- VOD는 비디오 업로드 시 통과 필드 지정을 지원하며 이벤트 완료 시 통과 필드를 App 백그라운드에 공지합니다. 이벤트 공지에는 다음 필드가 포함됩니다.
	- `SourceType`: 해당 필드는 Tencent Cloud에서 `ServerUpload`로 고정되며 업로드 출처가 서버 업로드임을 나타냅니다.
	- `SourceContext`: 사용자 정의 통과 필드는 App 백그라운드가 서명을 배포할 때 지정하는 통과 필드 사항으로, 서명의 `sourceContext` 매개변수에 해당합니다.
- VOD는 비디오 업로드 완료 시 자동 영상 처리를 지원합니다. 업로드 시 [비디오 처리 작업 프로세스](https://intl.cloud.tencent.com/document/product/266/33931)를 지정한 경우, 이벤트 공지 내용에 작업 ID가 포함되며, 이는 이벤트 공지의 `data.procedureTaskId`필드에 해당합니다.

더 자세한 정보는 다음을 참조하십시오.
- [작업 관리 및 이벤트 공지](https://intl.cloud.tencent.com/document/product/266/33931)
-[이벤트 공지 - 비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950)

## 고급 기능

- ### [](id:p1) 업로드 시 작업 프로세스 지정
개발자가 비디오 업로드 완료 후 자동으로 [비디오 처리 작업 프로세스](https://intl.cloud.tencent.com/document/product/266/33931)(예: 트랜스 코딩, 캡처 등)를 시작해야 하는 경우, [업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922) 생성 시 `procedure` 매개변수를 통해 구현 가능하며, 매개변수 값은 작업 프로세스 템플릿의 이름입니다. VOD는 [작업 프로세스 템플릿 생성](https://intl.cloud.tencent.com/document/product/266/14058)과 템플릿 이름 지정을 지원하며, 작업 프로세스 시작 시 작업 프로세스 템플릿 이름을 통해 시작할 작업을 표시할 수 있습니다.
- ### 업로드 시 스토리지 리전 지정
VOD에서 기본 제공되는 스토리지 리전은 충칭으로 설정되어 있습니다. 다른 리전에 저장하려면 콘솔에서 다른 스토리지 리전을 추가할 수 있습니다. 자세한 내용은 [업로드 스토리지 설정](https://intl.cloud.tencent.com/document/product/266/18874)을 참조하십시오. 설정 완료 후 [업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922) 생성 시 `storageRegion` 매개변수를 통해 지정하며, 매개변수 값은 스토리지 리전의 [영문 약칭](https://intl.cloud.tencent.com/document/product/266/9760)입니다.
- ### 업로드 시 표지 첨부
VOD는 비디오 업로드 과정에서 표지를 첨부하여 업로드하는 것을 허용합니다. 즉, 업로드 SDK 인터페이스에서 관련 표지 경로를 입력할 수 있습니다. 자세한 내용은 다음을 참조하십시오.
	- [Android 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33925)
	- [iOS 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33926)
	- [Web 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33924)
- ### [](id:p4) 1회 유효 서명
비디오 업로드 과정 중 App 백그라운드에서 배포한 서명은 기본적으로 유효기간 내에 여러 번 사용할 수 있습니다. 비디오 업로드에 대한 App의 보안성 요구가 까다로운 경우에는 서명을 1회만 유효하도록 지정할 수 있습니다.
1회 유효 서명 사용 방법: App 백그라운드에서 서명 배포 시 `oneTimeValid` 매개변수를 1로 설정하면 됩니다. 자세한 내용은 [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 참조하십시오.
>?1회 유효 서명은 1회만 사용할 수 있습니다. 해당 서명 방식은 보안성은 우수하지만 App에서 별도의 문제 처리 작업이 필요합니다. 예를 들어, 업로드 오류 발생 시 간편하게 SDK를 중복 사용하여 비디오를 업로드할 수 없고 업로드 서명을 재차 신청해야 합니다.
- ### 중단 지점부터 업로드 재개
비디오 업로드 중에 예기치 않게 업로드가 중단되어 해당 파일을 다시 업로드하는 경우, 중단된 지점부터 이어서 업로드가 재개됩니다.
>?중단 지점부터 업로드 재개 시 유효 기간은 1일입니다. 즉 영상 업로드가 중단된 뒤 1일 이내에는 중단된 지점부터 그대로 다시 업로드할 수 있으나 1일 경과 후에는 비디오 전체를 다시 업로드해야 합니다.
>
App에서 중단 지점부터 업로드 재개 기능을 활성화 하는 방법은 다음과 같습니다.
	- [Android 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33925), 업로드 시 `enableResume` 필드를 True로 설정합니다.
	- [iOS 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33926), 업로드 시 `enableResume` 필드를 True로 설정합니다.
	- [Web 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33924), 중단 지점부터 업로드 재개 기능이 내장되어 있어 사용자의 별도 조작이 필요치 않습니다.
- ### 업로드 일시정지/재개/취소
비디오 업로드 과정에서 VOD SDK는 업로드 일시정지, 재개, 취소를 지원합니다. 자세한 내용은 다음을 참조하십시오.
	- [Android 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33925)
	- [iOS 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33926)
	- [Web 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33924)
