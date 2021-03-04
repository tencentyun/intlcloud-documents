>!본 문서에서는 **TRTC**의 Cloud Access Management(CAM) 관련 기능을 소개합니다. 기타 제품의 CAM 관련 내용은 [CAM 지원 제품](https://intl.cloud.tencent.com/document/product/598/10588)을 참조하십시오.

[CAM](https://intl.cloud.tencent.com/document/product/598)(Cloud Access Management, **CAM**)은 Tencent Cloud에서 제공하는 웹서비스로써, 사용자가 Tencent Cloud 계정에서 리소스 액세스 권한에 대한 보안을 관리하는 데 주로 사용합니다. CAM을 통하여 사용자(그룹)을 생성, 관리 및 폐기할 수 있으며, 신분 관리 및 정책 관리를 통해 어떤 Tencent Cloud 리소스를 누가 사용할지 제어할 수 있습니다.

TRTC에 이미 **CAM**을 연결한 경우, 개발자는 필요에 따라 서브 계정에 적합한 TRTC 액세스 권한을 할당할 수 있습니다.

## 시작하기

TRTC CAM을 사용하기 전 CAM과 TRTC의 기본 개념을 모두 이해해야 합니다. 관련 개념은 다음 문서를 참조하십시오.

- CAM 관련: [사용자](https://intl.cloud.tencent.com/document/product/598/32633), [정책](https://intl.cloud.tencent.com/document/product/598/10601) 
- TRTC 관련: [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714), [SDKAppID](https://intl.cloud.tencent.com/document/product/647/37714)

## 적용 시나리오

### Tencent Cloud 제품 차원에서의 권한 분리
어떤 기업 내의 여러 부서에서 Tencent Cloud를 사용하고 있고 A부서는 TRTC 연결만 담당하고 있는 있을 때, A부서의 직원은 TRTC 액세스 권한만 가지고 있어야 하며, 다른 Tencent Cloud 제품 권한을 가지고 있어서는 안 됩니다. 해당 기업은 루트 계정이 A부서인 계정에서 서브 계정을 생성하고 해당 서브 계정에 TRTC 관련 권한만 부여하여 해당 서브 계정을 A부서에 사용하도록 제공할 수 있습니다.

### TRTC 애플리케이션 차원에서의 권한 분리
어떤 기업 내의 여러 서비스에서 TRTC를 사용하고 있고 상호 간에 분리되어야 하는 경우, 분리 방법으로는 리소스 분리와 권한 분리 두 가지 방법이 있습니다. 리소스 분리는 TRTC 애플리케이션 시스템에서 제공하며, 권한 분리는 TRTC CAM으로 구현됩니다. 해당 기업은 모든 서비스별로 1개의 서브 계정을 생성하고 관련 TRTC 애플리케이션을 부여하여 서비스별로 관련 애플리케이션만 액세스할 수 있도록 설정할 수 있습니다.

### TRTC 작업 차원에서의 권한 분리
어떤 기업의 한 서비스에서 TRTC를 사용하고, 해당 서비스의 제품 운영자가 TRTC 콘솔에 액세스하여 사용량 통계 정보를 가져와야 하지만 오작업 방지를 위해 중요 작업(예: 릴레이 푸시 스트림, 클라우드 녹화 설정 등 수정)에 대해서는 권한을 허용하지 않을 경우, 먼저 사용자 정의 정책을 생성하고 해당 정책에 TRTC 콘솔 로그인 및 사용량 통계 관련 API 액세스 권한만 부여합니다. 그 후, 서브 계정을 생성하여 해당 정책을 바인딩하고 해당 서브 계정을 제품 운영자에게 제공하면 됩니다.

## 권한 부여 단위
CAM의 핵심 기능은 **특정 계정의 특정 리소스에 대한 특정 작업 허용 또는 금지**라고 표현할 수 있습니다. TRTC CAM은 [리소스 레벨의 권한 부여](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B)를 지원하며, 리소스는 [TRTC 애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714) 단위로, 작업은 [서버 API](https://intl.cloud.tencent.com/document/product/647/34260) 및 TRTC 콘솔 액세스 시 사용하는 API를 포함한 [클라우드 API](https://intl.cloud.tencent.com/product/api) 단위로 분할됩니다.



## 능력 제한
- TRTC CAM의 리소스는 [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714) 단위로 분할되며, 더 작은 단위의 리소스로(예: 애플리케이션 정보, 설정 정보 등) 분할되지 않습니다.
- TRTC CAM은 프로젝트를 지원하지 않으며, [태그](https://intl.cloud.tencent.com/document/product/651/13335)를 통해 클라우드 서비스 리소스를 관리하시기 바랍니다.
