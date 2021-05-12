>!본 문서는 **TRTC** CAM 기능에 대한 내용을 소개합니다. 기타 제품의 CAM 관련 내용은 [CAM 지원 제품](https://intl.cloud.tencent.com/document/product/598/10588)을 참조하십시오.

[CAM](https://intl.cloud.tencent.com/document/product/598)(Cloud Access Management, **CAM**)은 Tencent Cloud에서 제공하는 웹서비스로, 사용자가 Tencent Cloud 계정의 리소스에 대한 액세스 권한을 안전하게 관리하는 데 주로 사용합니다. CAM으로 사용자(그룹)를 생성, 관리 및 폐기할 수 있으며, 신분 관리 및 정책 관리를 통해 누가 어떤 Tencent Cloud 리소스를 사용할지 제어할 수 있습니다.

TRTC가 **CAM**에 이미 연결된 경우, 개발자는 필요에 따라 서브 계정에 적합한 TRTC 액세스 권한을 할당할 수 있습니다. 

## 시작하기

TRTC CAM 사용 시, 사전에 CAM과 TRTC의 기본 개념을 모두 이해해야 합니다. 관련 개념은 다음 문서를 참조하십시오.

- CAM 관련: [사용자](https://intl.cloud.tencent.com/document/product/598/32633), [정책](https://intl.cloud.tencent.com/document/product/598/10601) 
- TRTC 관련: [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714), [SDKAppID](https://intl.cloud.tencent.com/document/product/647/37714)

## 적용 시나리오

### Tencent Cloud 제품 차원의 권한 격리
기업에서 여러 부서가 Tencent Cloud를 사용 중이며 A 부서는 TRTC 연결만 담당하고 있습니다. A 부서의 직원은 TRTC 액세스 권한은 필요하지만, 다른 Tencent Cloud 제품의 액세스 권한은 가질 수 없습니다. 이 경우, 해당 기업은 루트 계정을 통해 A 부서를 위한 서브 계정을 생성하고 해당 서브 계정에 대해서만 TRTC 관련 권한을 부여한 다음 A 부서에 제공할 수 있습니다.

### TRTC 애플리케이션 차원의 권한 격리
기업에서 여러 비즈니스에 TRTC를 사용 중이라면 비즈니스 간 격리가 필요하며, 격리에는 리소스 격리와 권한 격리 두 가지 방법이 있습니다. 리소스 격리는 TRTC 애플리케이션 시스템에서 제공하며, 권한 분리는 TRTC CAM으로 구현됩니다. 해당 기업은 각 비즈니스당 하나의 서브 계정을 생성하고, 관련된 애플리케이션에만 액세스할 수 있도록 TRTC 애플리케이션 권한을 부여할 수 있습니다.

### TRTC 작업 차원의 권한 격리
기업의 어느 비즈니스에서 TRTC를 사용 중이라면, 해당 비즈니스의 제품 운영자는 TRTC 콘솔에 액세스하여 사용량 통계 정보를 가져와야 함과 동시에 오작업으로 비즈니스에 영향을 미칠 가능성이 있는 중요 작업(예: 릴레이 푸시 스트림 수정, 클라우드 녹화 설정 수정 등)은 할 수 없습니다. 이 경우, 먼저 TRTC 콘솔 로그인 및 사용량 통계와 관련된 API 액세스 권한을 가진 사용자 정의 정책을 생성합니다. 그 다음 서브 계정을 생성하여 위의 정책을 바인딩하고 해당 서브 계정을 제품 운영자에게 제공할 수 있습니다.

## 권한 부여 단위
CAM의 핵심 기능은 **특정 리소스에 대한 특정 계정의 특정 작업 수행 허용 또는 금지**입니다. TRTC CAM은 [리소스 레벨 권한 부여](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B)를 지원하며, 리소스는 [TRTC 애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714) 단위로, 작업은 [서버 API](https://intl.cloud.tencent.com/document/product/647/34260) 및 TRTC 콘솔 액세스 시 사용하는 API를 포함한 [클라우드 API](https://intl.cloud.tencent.com/product/api) 단위로 분할됩니다. 자세한 설명은 [권한을 부여할 수 있는 리소스 및 작업](https://intl.cloud.tencent.com/document/product/647/39549)을 참조하십시오.



## 기능 제한
- TRTC CAM의 리소스는 [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714) 단위로 분할되며, 더 작은 단위의 리소스(예: 애플리케이션 정보, 설정 정보 등)에는 권한 부여를 지원하지 않습니다.
- TRTC CAM은 프로젝트를 지원하지 않습니다. [태그](https://intl.cloud.tencent.com/document/product/651/13335)를 통한 클라우드 서비스 리소스 관리를 권장합니다.
