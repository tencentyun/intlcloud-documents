## 기존 문제
Tencent Cloud 계정 키를 공유하는 다른 사용자가 관리하는 CVM, VPC 및 TencentDB와 같은 여러 Tencent Cloud 서비스를 사용하는 경우 다음과 같은 문제가 발생할 수 있습니다.
- 여러 사용자가 키를 공유하므로 유출 리스크가 높습니다.
- 다른 사용자의 액세스 권한을 제한할 수 없으므로 오작업으로 인한 보안 리스크 발생 가능성이 높습니다.

## 솔루션
상기 문제를 피하기 위해 다른 사용자가 서브 계정을 통해 다른 서비스를 관리하도록 할 수 있습니다. 기본적으로 서브 계정에는 Tencent Cloud 서비스 또는 관련 리소스를 사용할 수 있는 권한이 없습니다. 따라서 서브 계정에 필요한 권한을 부여하는 정책을 생성해야 합니다.

[CAM](https://intl.cloud.tencent.com/document/product/598/10583)(Cloud Access Management)은 Tencent Cloud 리소스에 대한 액세스 권한을 안전하게 관리하고 제어하는 데 도움이 되는 Web 기반 Tencent Cloud 서비스입니다. CAM을 사용하여 사용자(그룹)를 생성, 관리 및 종료할 수 있으며 ID 및 정책 관리를 통해 지정된 사용자가 사용할 수 있는 Tencent Cloud 리소스를 제어할 수 있습니다.

CAM을 사용하여 정책을 사용자 또는 사용자 그룹과 연결하여 지정된 리소스를 사용하여 지정된 작업을 완료하는 것을 허용하거나 금지할 수 있습니다. CAM 정책 관련 더 많은 정보는 [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603)를 참고하십시오.

서브 계정에 대한 TencentDB 리소스에 대한 액세스 권한을 관리할 필요가 없는 경우 이 장을 건너뛸 수 있습니다. 이는 설명서의 다른 부분에 대한 이해 및 사용에 영향을 미치지 않습니다.

### 시작하기
CAM 정책은 하나 이상의 CDB 작업 사용을 승인 또는 거부해야 합니다. 동시에 작업에 사용할 수 있는 리소스(특정 작업에 대한 전체 리소스 또는 부분 리소스일 수 있음)를 지정해야 합니다. 정책에는 작업된 리소스에 대해 설정된 조건도 포함될 수 있습니다.

>?
>- CAM 정책을 통해 CDB 리소스를 관리하고 CDB 작업을 승인하는 것이 좋습니다. 프로젝트별로 권한이 부여된 기존 사용자의 경험은 동일하게 유지되지만 프로젝트 기반 방식으로 리소스를 계속 관리하고 작업에 권한을 부여하는 것은 권장되지 않습니다.
>- 현재 CDB에 대한 유효성 조건을 설정할 수 없습니다.

| 작업 | 링크 | 
|---------|---------|
| 정책의 기본 구성에 대한 이해 | [정책 구문](https://intl.cloud.tencent.com/document/product/236/14466)|
| 정책에서의 작업 정의 | [TencentDB에서의 작업](https://intl.cloud.tencent.com/document/product/236/14466) | 
| 정책에서의 리소스 정의 | [CDB의 리소스 경로](https://intl.cloud.tencent.com/document/product/236/14466)|
| CDB가 지원하는 리소스 수준의 권한 | [CDB가 지원하는 리소스 수준 권한](https://intl.cloud.tencent.com/document/product/236/14467)|
| 콘솔 사례 | [콘솔 사례](https://intl.cloud.tencent.com/document/product/236/14468)|
