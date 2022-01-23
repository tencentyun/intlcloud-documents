>!본 문서는 **VOD** CAM 기능에 대한 내용을 소개합니다. 기타 제품의 CAM 관련 내용은 [CAM 지원 제품](https://intl.cloud.tencent.com/document/product/598/10588)을 참고하십시오.

VOD에 Tencent Cloud [CAM](https://intl.cloud.tencent.com/document/product/598)(Cloud Access Management)이 통합되었습니다. 필요에 따라 서브 계정에 지정된 VOD 권한을 부여할 수 있습니다. VOD 액세스 관리 기능은 VOD 서비스가 활성화되면 바로 사용할 수 있습니다.
본문은 사용자가 이미 Tencent Cloud CAM 및 VOD의 서브 애플리케이션 시스템에 대한 지식이 있다고 가정합니다. 이 문서와 관련된 주요 개념은 다음과 같습니다.

- CAM: [사용자 유형](https://intl.cloud.tencent.com/document/product/598/32633), [API 키](https://intl.cloud.tencent.com/document/product/598/32675), [정책](https://intl.cloud.tencent.com/document/product/598/10601), [정책 구문](https://intl.cloud.tencent.com/document/product/598/10603)
- VOD: [서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987)

## 응용 시나리오
VOD 액세스 관리의 일반적인 응용 시나리오는 다음과 같습니다.

- **Tencent Cloud 제품 수준에서 권한 격리**
Tencent Cloud를 사용하는 다양한 기업 내부 부서 중 A 부서에서 VOD 서비스를 담당합니다. A 부서 직원은 VOD 액세스 권한이 필요하지만 다른 Tencent Cloud 제품에는 액세스할 수 없습니다. 이를 위해 서브 계정을 생성하여 VOD 관련 권한만 부여한 후 A 부서에 제공할 수 있습니다.
- **VOD 서브 애플리케이션 수준에서 권한 격리**
기업 내 여러 부서에서 VOD를 사용하는 경우 일반적으로 격리가 필요합니다. 격리는 리소스 격리 및 권한 격리를 포함하며 전자는 VOD의 서브 애플리케이션 시스템에 의해 활성화되고, 후자는 VOD 액세스 관리에 의해 구현됩니다. 이 경우 각 부서에 서브 계정을 생성하고 해당 서브 애플리케이션에 대한 권한을 부여하여 각 부서가 지정된 서브 애플리케이션에만 액세스할 수 있도록 할 수 있습니다.
- **VOD 운영 수준에서 권한 격리**
기업 내 한 부서에서 VOD를 사용하는 경우, 운영 직원은 통계 정보(예: 트래픽의 지리적 분포 및 재생 횟수)를 얻기 위해 VOD 콘솔에 액세스해야 하지만 민감한 작업(예: 파일 삭제 또는 도메인 비활성화)을 수행하는 것은 금지되어야 합니다. 잘못된 운영으로부터 비즈니스를 보호하기 위한 목적입니다. 이러한 요구 사항을 충족하기 위해 VOD 콘솔에 로그인하고 통계 API를 호출할 수 있는 권한이 있는 사용자 정의 정책을 생성한 후, 서브 계정을 생성하여 해당 정책에 바인딩한 다음, 서브 계정 정보를 제품 운영 직원에게 전달할 수 있습니다.

## 리소스 세분성 및 작업 세분성
CAM의 핵심 기능은 **계정이 일부 작업을 수행하거나 일부 리소스를 조작하는 것을 허용하거나 금지하는 것입니다.** VOD의 경우 리소스 세분성은 서브 애플리케이션이며, 작업 세분성은 서버 API입니다.

## 기능 제한
- VOD 액세스 관리는 서브 애플리케이션 수준에서의 권한 부여를 지원하지만 더 세분화된 리소스 수준(예: 미디어 파일 및 도메인 이름)에서는 지원하지 않습니다.

## 리소스 수준에서 권한 부여를 지원하는 API

VOD 액세스 관리는 [리소스 수준의 권한 부여](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/598/10588)를 지원하며, 특별한 제한이 있는 API를 제외한 모든 API는 리소스 수준의 권한 부여를 지원합니다. 자세한 내용은 아래를 참고하십시오.

### 리소스 수준에서 권한 부여를 지원하지 않는 API 리스트

| API 이름                                        | API 기능       | 설명                                                         |
| :---------------------------------------------- | -------------- | ------------------------------------------------------------ |
| [DescribeSubAppIds](https://intl.cloud.tencent.com/document/product/266/34177)    | 서브 애플리케이션 목록 쿼리 | 모든 서브 계정는 권한 부여 없이 이 API를 호출할 수 있는 권한이 있으며 서브 애플리케이션을 지정할 필요가 없습니다. |
| [ModifySubAppIdStatus](https://intl.cloud.tencent.com/document/product/266/34173) | 서브 애플리케이션의 상태 수정 | 이 API는 지정된 서브 애플리케이션을 비활성화할 수 있으므로 매우 위험합니다. 따라서 전체 VOD 권한(예: [사전 설정 정책](https://intl.cloud.tencent.com/document/product/266/33971)에 설명된 `QcloudVODFullAccess`)가 있는 서브 계정만 사용할 수 있습니다. 특정 서브 애플리케이션에 대한 쓰기 권한이 부여되었지만 `QcloudVODFullAccess`가 아닌 서브 계정는 이 API를 호출할 수 없습니다. |

### 리소스 수준에서 권한 부여를 지원하는 API 리스트

상기 목록의 API를 제외하고 [API 개요](https://intl.cloud.tencent.com/document/product/266/34110)에 설명된 모든 API는 리소스 수준에서 권한 부여를 지원합니다. 정책 구문에서 이러한 API에 대한 리소스 설명은 모두 `qcs::vod::uin/$uin:subAppId/$subAppId` 형식입니다.

