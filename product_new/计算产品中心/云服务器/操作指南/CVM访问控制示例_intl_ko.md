## 사용 시나리오

액세스 관리(Cloud Access Management, CAM) 정책을 통해 사용자는 클라우드 서버(Cloud Virtual Machine. CVM) 콘솔에서 특정 리소스를 조회 및 사용하는 권한을 가질 수 있습니다. 본 문서는 특정 리소스를 조회 및 사용하는 권한 예시를 제공하여 사용자가 콘솔의 특정 부분 정책을 어떻게 사용하는지 알려드립니다.

## 작업 예시
### CVM의 전체 읽기 및 쓰기 정책
사용자에게 CVM 인스턴스 생성 및 관리하는 권한을 부여하는 경우 해당 사용자에게 QcloudCVMFullAccess 정책을 사용할 수 있습니다. 해당 정책은 사용자가 각각 CVM, VPC (Virtual Private Cloud), CLB (Cloud Load Balance) 및 MONITOR의 모든 리소스에 대해 작업 권한을 부여함으로써 목적을 달성합니다.
구체적인 작업 순서는 다음과 같습니다.
사전에 설정된 정책 QcloudCVMFullAccess에 권한을 부여하려면 [라이선스 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.

### CVM 읽기 전용 정책
사용자가 CVM 인스턴스를 쿼리할 수 있는 권한은 있지만 작성, 삭제 및 시작/종료 권한이 없는 경우 해당 사용자에게 QcloudCVMInnerReadOnlyAccess 정책을 사용할 수 있습니다. 해당 정책은 사용자가 CVM에서 단어 "Describe" 및 단어 "Inquiry"로 시작하는 모든 작업에 대해 구체적인 작업 권한을 부여함으로써 목적을 달성합니다. 구체적인 작업 순서는 다음과 같습니다.
사전에 설정된 정책 QcloudCVMInnerReadOnlyAccess에 권한을 부여하려면 [라이선스 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.

### CVM 관련 리소스의 읽기 전용 정책
사용자가 CVM 인스턴스 및 관련 리소스(VPC, CLB)를 쿼리할 수 있는 권한만 부여하고 작성, 삭제 및 시작/종료 등 작업 권한을 부여하지 않을 경우 해당 사용자에게 QcloudCVMReadOnlyAccess 정책을 사용할 수 있습니다. 해당 정책은 사용자가 각각 다음과 같은 작업에 대해 권한을 부여함으로써 목적을 달성합니다.
- CVM에서 단어 "Describe" 및 "Inquiry"로 시작하는 모든 작업
- VPC에서 단어 "Describe", "Inquiry" 및 "Get"로 시작하는 모든 작업
- CLB에서 단어 "Describe"로 시작하는 모든 작업
- Monitor의 모든 작업

구체적인 작업 순서는 다음과 같습니다.
사전에 설정된 정책 QcloudCVMReadOnlyAccess에 권한을 부여하려면 [라이선스 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.

### 엘라스틱 CBS 관련 정책

CVM 콘솔에서 CBS에 대한 정보 조회, 생성 및 사용 등 권한을 사용자에게 부여할 경우 다음과 같은 작업을 정책에 추가한 후 사용자와 연결할 수 있습니다.
- **CreateCbsStorages:** CBS를 생성합니다.
- **AttachCbsStorages:** 지정된 엘라스틱 CBS를 지정된 클라우드 서버에 마운트합니다.
- **DetachCbsStorages:** 지정된 엘라스틱 CBS 언마운트합니다.
- **ModifyCbsStorageAttributes:** 지정된 CBS의 이름 및 프로젝트 ID를 수정합니다.
-**DescribeCbsStorages:** CBS의 세부 정보를 쿼리합니다.
- **DescribeInstancesCbsNum:** 클라우드 서버가 마운트된 엘라스틱 CBS 수와 마운트 가능한 총 엘라스틱 CBS 수를 쿼리합니다.
- **RenewCbsStorage:** 지정된 엘라스틱 CBS를 연장합니다.
- **ResizeCbsStorage:** 지정된 엘라스틱 CBS 용량을 확장합니다.

구체적인 작업 순서는 다음과 같습니다.
1. [정책](https://intl.cloud.tencent.com/document/product/598/10601)에 따라 CVM 콘솔에서 CBS 정보 조회, 생성 및 사용 등 다른 권한의 사용자 정의 정책을 생성할 수 있습니다.
정책 내용은 다음 정책 구문을 참조하여 설정할 수 있습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cvm:CreateCbsStorages",
                "name/cvm:AttachCbsStorages",
                "name/cvm:DetachCbsStorages",
                "name/cvm:ModifyCbsStorageAttributes",
                "name/cvm:DescribeCbsStorages"
            ],
            "resource": [
                "qcs::cvm::uin/1410643447:*"
            ]
        }
    ]
}
```
2. 생성된 정책을 확인하고 해당 정책 행의 "작업" 열에서 [사용자/그룹 연결]을 클릭하십시오.
3. [사용자/사용자 그룹 연결] 팝업창에서 권한을 부여할 사용자/그룹을 선택하고 [확인]을 클릭하십시오.


### 보안 그룹 관련 정책

사용자가 CVM 콘솔에서 보안 그룹을 조회 및 사용하려면 다음과 같은 작업을 정책에 추가한 후 사용자와 연결할 수 있습니다.
- **DeleteSecurityGroup:**보안 그룹을 삭제합니다.
- **ModifySecurityGroupPolicys：**보안 그룹의 모든 정책을 교체합니다.
- **ModifySingleSecurityGroupPolicy:**보안 그룹의 단일 정책을 수정합니다.
- **CreateSecurityGroupPolicy:**보안 그룹 정책을 생성합니다.
- **DeleteSecurityGroupPolicy:**보안 그룹 정책을 삭제합니다.
- **ModifySecurityGroupAttributes:**보안 그룹 속성을 수정합니다.

구체적인 작업 순서는 다음과 같습니다.
1. [정책](https://intl.cloud.tencent.com/document/product/598/10601)에 따라 CVM 콘솔에서 보안 그룹을 생성, 삭제 및 수정 등 다른 권한의 사용자 정의 정책을 생성할 수 있습니다.
정책 내용은 다음 정책 구문을 참조하여 설정할 수 있습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:ModifySecurityGroupPolicys",
                "name/cvm:ModifySingleSecurityGroupPolicy",
                "name/cvm:CreateSecurityGroupPolicy",
                "name/cvm:DeleteSecurityGroupPolicy"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
2. 생성된 정책을 확인하고 해당 정책 행의 "작업" 열에서 [사용자/그룹 연결]을 클릭하십시오.
3. [사용자/사용자 그룹 연결] 팝업창에서 권한을 부여할 사용자/그룹을 선택하고 [확인]을 클릭하십시오.


### EIP 주소 관련 정책

사용자가 CVM 콘솔에서 EIP 주소를 조회 및 사용하려면 다음과 같은 작업을 정책에 추가한 후 사용자와 연결할 수 있습니다.
- **AllocateAddresses：**VPC 또는 CVM에 주소를 할당합니다.
- **AssociateAddress: **EIP 주소, 인스턴스 또는 네트워크 인터페이스를 연결합니다.
- **DescribeAddresses: **CVM 콘솔에서 EIP 주소를 조회합니다.
- **DisassociateAddress:** EIP 주소, 인스턴스 또는 네트워크 인터페이스를 연결을 취소합니다.
- **ModifyAddressAttribute: **EIP 주소의 속성을 수정합니다.
- **ReleaseAddresses:** EIP 주소를 해제합니다.

구체적인 작업 순서는 다음과 같습니다.
1. [정책](https://intl.cloud.tencent.com/document/product/598/10601)에 따라 사용자 정의 정책을 생성합니다.
해당 정책은 사용자가 CVM 콘솔에서 EIP 주소 조회 및 인스턴스 할당을 연결할 수 있지만 EIP 주소의 속성 수정, 연결 해제 및 권한 해제는 실행할 수 없습니다. 정책 내용은 다음 정책 구문을 참조하여 설정할 수 있습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:DescribeAddresses",
                "name/cvm:AllocateAddresses",
                "name/cvm:AssociateAddress"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
2. 생성된 정책을 확인하고 해당 정책 행의 "작업" 열에서 [사용자/그룹 연결]을 클릭하십시오.
3. [사용자/사용자 그룹 연결] 팝업창에서 권한을 부여할 사용자/그룹을 선택하고 [확인]을 클릭하십시오.

### 사용자에게 특정 CVM에 대한 작업 권한을 부여하기 위한 정책
사용자에게 특정 CVM에 대한 작업 권한을 부여할 경우 다음과 같은 정책을 해당 사용자와 연결할 수 있습니다. 구체적인 작업 순서는 다음과 같습니다.
1. [정책](https://intl.cloud.tencent.com/document/product/598/10601)에 따라 사용자 정의 정책을 생성합니다.
해당 정책을 통해 사용자에게 ID가 ins-1이고 리전이 광저우 CVM 인스턴스에 대한 작업 권한을 부여할 수 있습니다. 정책 내용은 다음 정책 구문을 참조하여 설정할 수 있습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:ap-guangzhou::instance/ins-1",
            "effect": "allow"
        }
    ]
}
```
2. 생성된 정책을 확인하고 해당 정책 행의 "작업" 열에서 [사용자/그룹 연결]을 클릭하십시오.
3. [사용자/사용자 그룹 연결] 팝업창에서 권한을 부여할 사용자/그룹을 선택하고 [확인]을 클릭하십시오.


### 사용자에게 특정 리전 CVM에 대한 작업 권한을 부여하기 위한 정책
사용자에게 특정 리전 CVM에 대한 작업 권한을 부여할 경우 다음과 같은 정책을 사용자와 연결할 수 있습니다. 구체적인 작업 순서는 다음과 같습니다.
1. [정책](https://intl.cloud.tencent.com/document/product/598/10601)에 따라 사용자 정의 정책을 생성합니다.
해당 정책을 통해 사용자에게 광저우 리전의 CVM 기기에 대해 작업 권한을 부여할 수 있습니다. 정책 내용은 다음 정책 구문을 참조하여 설정할 수 있습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```
2. 생성된 정책을 확인하고 해당 정책 행의 "작업" 열에서 [사용자/그룹 연결]을 클릭하십시오.
3. [사용자/사용자 그룹 연결] 팝업창에서 권한을 부여할 사용자/그룹을 선택하고 [확인]을 클릭하십시오.


### 라이선스 서브 계정에는 CVM에 대한 모든 권한 보유, 결제 권한은 비포함

기업 계정(CompanyExample, ownerUin은 12345678 임)에 서브 계정(Developer)이 있다고 가정할 경우, 해당 서브 계정은 기업 계정의 CVM 서비스에 대한 모든 관리 권한 (생성, 관리 등 전체 작업)을 필요로 하지만 결제 권한은 포함하지 않습니다(주문할 수 있지만 결제할 수 없습니다).
다음과 같은 두 가지 솔루션을 통해 실행할 수 있습니다.
- **솔루션 A**
기업 계정 CompanyExample에서 직접 사전에 설정된 정책 QcloudCVMFullAccess를 서브 계정 Developer에 권한을 부여합니다. 권한 부여 방식은 [라이선스 관리](https://intl.cloud.tencent.com/document/product/598/10602)에서 참조하십시오.
- **솔루션 B**
 1. 다음 정책 구문에 따라 [사용자 정의 정책](# CAMCustomPolicy)을 생성합니다.
```
 {
    "version": "2.0",
    "statement":[
         {
             "effect": "allow",
             "action": "cvm:*",
             "resource": "*"
         }
    ]
}
```
 2.해당 정책을 서브 계정에 권한을 부여합니다. 권한 부여 방식은 [라이선스 관리](https://intl.cloud.tencent.com/document/product/598/10602)에서 참조하십시오.


### 서브 계정에 프로젝트 관리의 작업 권한 부여
기업 계정(CompanyExample, ownerUin은 12345678임)에 서브 계정(Developer)이 있다고 가정할 경우, 프로젝트 라이선스 서브 계정을 기반으로 콘솔에서 리소스를 관리해야 합니다.
구체적인 작업 순서는 다음과 같습니다.
1. 서비스 권한에 따라 프로젝트 관리의 사용자 정의 정책을 작성합니다.
자세한 내용은 [정책](https://intl.cloud.tencent.com/document/product/598/10601)을 참조하십시오.
2. 생성된 사용자 정의 정책을 서브 계정에 권한을 부여하려면 [라이선스 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.
서브 계정이 프로젝트를 관리할 때 스냅샷, 미러 이미지, VPC 및 EIP 등 제품을 조회할 경우 권한이 없다고 제시됩니다. 사전에 서브 계정 QcloudCVMAccessForNullProject, QcloudCVMOrderAccess 및 qcloudCVMLaunchToVPC에 대해 정책 권한을 부여할 수 있습니다. 권한 부여 방식은 [라이선스 관리](https://intl.cloud.tencent.com/document/product/598/10602)에서 참조하십시오.

<span id="CAMCustomPolicy"></span>
### 사용자 정의 정책

사전에 설정된 정책이 사용자의 요구 사항을 충족하지 못할 경우 사용자 정의 정책의 생성을 통해 목적을 달성할 수 있습니다.
구체적인 작업 순서는 [정책](https://intl.cloud.tencent.com/document/product/598/10601)을 참조하십시오.
CVM 관련 정책 구문에 대한 자세한 내용은 [라이선스 정책 구문](https://intl.cloud.tencent.com/document/product/213/10313)을 참조하십시오.

