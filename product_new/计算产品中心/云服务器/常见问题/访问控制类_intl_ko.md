### 사용자 정의 정책은 어떻게 생성합니까?

사전에 설정된 정책이 요구 사항을 충족하지 못할 경우 사용자 정의 정책을 생성할 수 있습니다.
사용자 정의 정책 구문은 아래와 같습니다.

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

- Action을 허용하거나 거부할 작업으로 교체하십시오.
- Resource를 권한을 부여할 특정 리소스로 교체하십시오.
- Effect를 허용 또는 거부로 교체하십시오.

### CVM의 읽기 전용 정책은 어떻게 구성합니까?

사용자에게 CVM 인스턴스 생성, 삭제, 시작 또는 종료에 대한 권한 없이 인스턴스를 조회할 수 있는 권한만 부여하고 싶을 경우 사용자에 대해 QcloudCVMInnerReadOnlyAccess라는 정책을 사용할 수 있습니다.

CAM 콘솔에 로그인한 뒤, [정책 관리](https://console.cloud.tencent.com/cam/policy) 인터페이스에서 **CVM**를 검색하여 이 정책을 찾을 수 있습니다.

정책 구문은 아래와 같습니다.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

위의 정책은 **사용자가 다음 작업에 대한 작업 권한을 갖도록 허용함**으로써 목적을 달성합니다.

- 단어 "Describe"로 시작하는 CVM의 모든 작업
- 단어 "Inquiry"로 시작하는 CVM의 모든 작업

### CVM 관련 리소스에 대한 읽기 전용 정책은 어떻게 구성합니까?

사용자에게 CVM 인스턴스 및 관련 리소스(VPC, CLB)를 조회할 수 있는 권한을 부여하고 싶지만 사용자의 생성, 삭제, 시작 및 종료에 대한 권한은 허용하고 싶지 않을 경우 이 사용자에 대해 QcloudCVMReadOnlyAccess라는 정책을 사용할 수 있습니다.

CAM 콘솔에 로그인한 뒤, [정책 관리](https://console.cloud.tencent.com/cam/policy) 인터페이스에서 **CVM**를 검색하여 이 정책을 찾을 수 있습니다.

정책 구문은 아래와 같습니다.

```
 {
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/clb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "name/monitor:*",
            "resource": "*"
        }
    ]
}
```

위의 정책은 **사용자가 다음 작업에 대한 각각의 작업 권한을 갖도록하여** 목적을 달성합니다.

- 단어 "Describe" 및 "Inquiry"로 시작하는 CVM의 모든 작업
- 단어 "Describe", "Inquiry" 및 "Get"으로 시작하는 VPC의 모든 작업
- 단어 "Describe"로 시작하는 CLB의 모든 작업
- Monitor의 모든 작업

