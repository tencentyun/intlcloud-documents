## TencentDB CAM 정책 예시
CAM 정책을 통해 사용자에게 CDB 콘솔에서 특정 리소스에 대한 조회 및 사용 권한을 부여할 수 있습니다. 이 예시는 사용자가 콘솔에서 특정 정책을 사용할 수 있도록 설정하는 방법에 관해 설명합니다.

>?TDSQL for MySQL은 이전에 dcdb로 알려졌으므로 CAM의 API 키워드는 dcdb입니다.

### 사용자 정의 정책 생성 구문
1. [정책 구문](https://console.cloud.tencent.com/cam/policy) 설정 페이지로 이동하여 **사용자 정의 정책 생성**을 클릭합니다.
2. 팝업 창에서 **정책 구문으로 생성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/cda7a1b0ec6256b620bcbd9290fd60fd.png)
3. 빈 템플릿을 선택하고 **다음**을 클릭합니다.
![](https://main.qcloudimg.com/raw/9c6bcdc90c02059a5abb67e73a74d739.png)
4. 해당 정책 구문을 입력합니다.
![](https://main.qcloudimg.com/raw/0938ab4115dc67b2e952aa1eaa1283cb.png)

### 서브 계정/협업 파트너 연결 및 확인
정책을 만든 후 사용자/그룹과 연결합니다. 연결이 완료되면 다른 브라우저(또는 서버)를 이용하여 서브 계정/협력자가 정상적으로 작동하는지 확인합니다. 정책 구문이 올바르게 작성되면 다음을 관찰할 수 있습니다.
- 의도한 타깃 제품 및 리소스에 대한 일반적인 액세스 권한이 있으며 예상되는 모든 기능을 사용할 수 있습니다.
- 다른 승인되지 않은 제품이나 리소스에 액세스할 때 **이 작업을 수행할 권한이 없습니다**라는 메시지가 표시됩니다.

>?여러 정책의 상호 영향을 방지하려면 한 번에 하나의 정책만 서브 계정에 연결하는 것이 좋습니다.
>계정 접근 권한에 대한 변경 사항은 1분 이내에 적용됩니다.

## 부록: 일반적으로 사용되는 정책 구문
### 모든 TencentDB 인스턴스의 모든 기능 사용을 승인하기 위한 정책
사용자에게 TencentDB 인스턴스를 만들고 관리할 수 있는 권한을 부여하려면 사용자에 대해 QcloudDCDBFullAccess라는 정책을 구현합니다.
정책 구문은 아래와 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dcdb:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

### 모든 TencentDB 인스턴스의 쿼리 권한 부여 정책
사용자에게 TencentDB 인스턴스를 볼 수 있는 권한을 부여하되 생성, 삭제 또는 수정하지 않으려면 사용자에 대해 QcloudDCDBInnerReadOnlyAccess라는 정책을 구현합니다.

정책 구문은 아래와 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dcdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
상기 정책은 사용자가 CAM 정책으로 TencentDB에서 ‘Describe’로 시작하는 모든 작업의 사용을 별도로 권한을 부여함으로써 목적을 달성합니다.

>?현재 모든 기능적 API를 다루는 것은 아니므로 일부 작업이 CAM에 포함되지 않은 것을 볼 수 있습니다. 이는 정상적인 현상입니다.

### 사용자에게 특정 리전 CDB 작업 권한을 부여하는 정책
사용자에게 특정 리전의 CDB에 대한 작업 권한을 부여할 경우, 아래 정책을 해당 사용자에게 연결할 수 있습니다. 아래 정책은 사용자에게 광저우 리전의 CDB 디바이스에 대한 작업 권한을 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:*",
            "resource": "qcs::dcdb:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

### 여러 특정 리전에서 TencentDB 인스턴스를 조작할 수 있는 사용자 권한 부여 정책
특정 리전에서 TencentDB 인스턴스를 조작할 수 있는 권한을 사용자에게 부여하려면 다음 정책을 사용자와 연결합니다. 예를 들어, 아래 정책은 사용자가 광저우 및 청두에서 TencentDB 인스턴스를 조작하도록 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:*",
            "resource": "qcs::dcdb:ap-guangzhou::*","qcs::dcdb:ap-chengdu::*",
            "effect": "allow"
        }
    ]
}
```

### 하나의 특정 TencentDB 인스턴스를 조작할 수 있는 사용자 권한 부여 정책
사용자에게 특정 데이터베이스를 조작할 수 있는 권한을 부여하려면 다음 정책을 사용자와 연결합니다. 예를 들어, 아래 정책은 사용자가 광저우에서 TencentDB 인스턴스 dcdb-xxx를 조작하도록 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dcdb:*"
            ],
            "resource": "qcs::dcdb:ap-guangzhou::instance/dcdb-xxx",
            "effect": "allow"
        }
    ]
}
```

### 여러 TencentDB 인스턴스를 조작할 수 있는 사용자 권한 부여 정책
사용자에게 TencentDB 인스턴스를 일괄적으로 조작할 수 있는 권한을 부여하려면 다음 정책을 사용자와 연결하십시오. 예를 들어, 아래 정책은 사용자가 광저우의 TencentDB 인스턴스 dcdb-xxx 및 dcdb-yyy 및 베이징의 dcdb-zzz를 조작하도록 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:*",
            "resource": ["qcs::dcdb:ap-guangzhou::instance/dcdb-xxx", "qcs::dcdb:ap-guangzhou::instance/dcdb-yyy", "qcs::dcdb:ap-beijing::instance/dcdb-zzz"],
            "effect": "allow"
        }
    ]
}
```

### 사용자에게 여러 TencentDB 인스턴스를 조작할 수 있는 다른 권한을 부여하는 정책
사용자에게 TencentDB 인스턴스를 일괄적으로 조작할 수 있는 권한을 부여하려면 다음 정책을 사용자와 연결하십시오. 예를 들어, 아래 정책은 사용자가 광저우의 TencentDB 인스턴스 dcdb-xxx 및 dcdb-yyy 및 베이징의 dcdb-zzz를 조작하도록 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:Describe*","dcdb:Create*",
            "resource": ["qcs::dcdb:ap-guangzhou::instance/dcdb-xxx", "qcs::dcdb:ap-guangzhou::instance/dcdb-yyy", "qcs::dcdb:ap-beijing::instance/dcdb-zzz"],
            "effect": "allow"
        }
    ]
}
```

### TencentDB 계정 생성에 대한 사용자 권한 거부
TencentDB 계정 생성에 대한 사용자 권한을 거부하려면 `’effect’: ‘deny’`를 구성하십시오.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:CreateAccount",
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```

### 기타 사용자 정의 정책
사전 설정된 정책이 요구 사항을 충족할 수 없는 경우 아래와 같이 사용자 정의 정책을 만들 수 있습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "Action"
            ],
            "resource": "Resource",
            "effect": "Effect"
        }
    ]
}
```

- Action에서 허용 또는 거부할 작업으로 변경합니다.
- Resource에서 권한을 부여할 구체적인 리소스로 변경합니다.
- Effect에서 허용 또는 거부로 변경합니다.

