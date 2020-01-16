Tencent Cloud의 CVM(Cloud Virtual Machine), VPC, 데이터 베이스 등의 서비스를 이용합니다. 이러한 서비스가 여러 사람에 의해 관리되는데 사용자의 클라우드 계정 키를 공유할 경우 아래와 같은 문제가 존재합니다.
- 사용자의 키를 여러 사람과 공유할수록 누출될 위험도 높아집니다.
- 다른 사람의 액세스 권한을 제한할 수 없으므로 오작동 및 보안 위험이 발생할 가능성이 높아집니다.

이러한 경우 서브 계정을 통해 여러 사람이 각각 다른 서비스를 관리하여 위의 문제를 피할 수 있습니다. 기본적으로 서브 계정은 CVM 권한 또는 CVM 관련 리소스를 사용할 권한이 없습니다. 그러므로 서브 계정이 필요한 리소스나 권한을 사용하는 것을 허용하는 정책을 생성해야 합니다.

CAM(Cloud Access Management)은 Tencent Cloud에서 제공하는 웹서비스로써, 사용자가 Tencent Cloud 계정에서 리소스 액세스 권한에 대한 보안을 관리하는 데 주로 사용합니다. CAM을 통하여 사용자(그룹)을 생성, 관리 및 폐기 할 수 있으며, 신분 관리 및 정책 관리를 통해 누가 어떤 Tencent Cloud 리소스를 사용하게 할지 제어할 수 있습니다.

CAM을 사용할 경우 사용자 또는 사용자 그룹과 정책을 연결할 수 있으며, 정책을 통해 사용자가 지정된 리소스로 지정된 작업을 완료할 수 있도록 권한을 부여하거나 거부할 수 있습니다. CAM 정책과 관련된 더 자세한 기본 정보는 [정책 구문](https://intl.cloud.tencent.com/document/product/598/10603), 사용 정보에 대한 내용은 [정책](https://intl.cloud.tencent.com/document/product/598/10601)을 참조하십시오.

서브 계정을 통한 CVM 관련 리소스 CAM 진행이 필요하지 않을 경우 이 섹션을 건너뛸 수 있습니다. 이 섹션을 건너뛰더라도 문서의 나머지 섹션을 이해하고 사용하는 데 영향을 미치지 않습니다.

#### 입문

CAM 정책은 반드시 하나 또는 그 이상의 CVM 작업 사용에 권한을 부여하거나 거부해야 합니다. 동시에 작업에 사용할 수 있는 리소스(모든 리소스일 수도 있고, 일부 리소스일 수도 있음)를 지정해야 하며, 정책에 작업 리소스에서 설정한 조건을 포함할 수 있습니다.

CVM의 일부 API 작업은 리소스 수준의 권한을 지원합니다. 따라서 이 유형의 API 작업에서는 작업에 사용할 특정 리소스를 지정할 수 없으며, 모든 리소스를 지정해 사용해야 한다는 것을 의미합니다.

| 작업 | 링크 | 
|---------|---------|
| 정책의 기본 구성에 대한 이해 | [정책 구문](https://intl.cloud.tencent.com/document/product/213/10313)|
| 정책에서의 작업 정의 | [CVM 작업](https://intl.cloud.tencent.com/document/product/213/10313) | 
| 정책에서의 리소스 정의 | [CVM의 리소스 경로](https://intl.cloud.tencent.com/document/product/213/10313)|
| 조건을 사용해 정책 제한 | [CVM의 조건부 키](https://intl.cloud.tencent.com/document/product/213/10313)|
| CVM이 지원하는 리소스 수준의 권한 | [CVM이 지원하는 리소스 수준 권한](https://intl.cloud.tencent.com/document/product/213/10314)|
| 콘솔 사례 | [콘솔 사례](https://intl.cloud.tencent.com/document/product/213/10312)|
