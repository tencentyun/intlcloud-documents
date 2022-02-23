## 작업 시나리오 
서브 계정을 사용하여 구독 작업을 만들고 관리할 수 있습니다. 데이터 구독을 위한 SDK Demo에서 서브 계정의 AccessKey 및 AccessKeySecret을 사용할 수도 있습니다. 

CAM(Cloud Access Management)을 사용할 때 정책을 사용자 또는 사용자 그룹과 연결하여 지정 작업을 완료하기 위해 지정 리소스 사용을 허용 또는 금지할 수 있습니다. CAM 정책에 대한 자세한 내용은 [정책 구문](https://intl.cloud.tencent.com/document/product/598/10603)을 참고하십시오. 

## 서브 계정 권한 부여
1. [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인합니다.
2. **사용자** > **사용자 리스트** 페이지에서 권한을 부여할 서브 계정을 찾고 아래와 같이 오른쪽의 작업 열에서 **권한 부여**를 클릭합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/d8e55e9eb52693885c08586115770b6d.png)
3. 팝업창에서 ‘DTS’를 검색하여 부여할 권한을 선택합니다.
    - QcloudDTSFullAccess: 읽기 및 쓰기 권한을 부여함을 나타냅니다.
    - QcloudDTSReadOnlyAccess: 읽기 전용 권한을 부여함을 나타냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8ea8cea9907f9b22cc33896d01d9ac56.png)
4. **확인**을 클릭하여 권한 부여를 완료합니다.

## 정책 구문
DTS에 대한 CAM 정책은 다음과 같이 설명됩니다.
```
 {     
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"]
           } 
       ] 
} 
```

- **버전 version**: 필수 작성 항목입니다. 현재는 ‘2.0’만 허용합니다.
- **명령 statement**: 하나 또는 다수의 권한과 관련한 자세한 정보를 설명하는 데 사용합니다. 이 요소에는 effect, action, resource 등 기타 여러 요소의 권한 또는 권한 집합이 포함됩니다. 하나의 정책은 하나의 statement 요소만 가집니다.
>?DTS의 데이터베이스 작업을 위해 DTS 작업 관련 데이터베이스 리소스에 대한 서브 계정 액세스 권한을 별도로 부여해야 합니다(읽기 권한, 즉, ‘Describe\*’ 필요). 이 권한 부여 작업은 본문에 포함되어 있지 않습니다.
- **영향 effect**: 필수 작성 항목입니다. 선언으로 발생한 결과가 '허용'인지 '명시적 거절'인지 설명합니다. allow(허용) 및 deny(명시적 거절) 두 가지 상황을 포함합니다.
```
"effect": "allow"
```
- **작업 action**: 필수 작성 항목입니다. 허용 또는 거절의 작업을 설명하는데 사용합니다. 작업은 API(접두사 name으로 표시) 또는 기능 집합(특정한 API 조합, 접두사 permid로 표시)이 가능합니다.
- **리소스 resource**: 필수 작성 항목입니다. 인증의 구체적인 데이터를 설명합니다. 

## DTS 작업
CAM 정책 설명에서 CAM을 지원하는 모든 서비스의 API 작업을 지정할 수 있습니다. name/dts: 접두사가 붙은 API는 DTS에 사용해야 합니다. 단일 문에 여러 작업을 지정하려면 아래와 같이 쉼표로 구분합니다. 
```
"action":["name/dts:action1","name/dts:action2"]
```

와일드카드를 사용해서 여러 항목의 작업을 지정할 수 있습니다. 예를 들어, 다음과 같이 명칭이 단어 ‘Describe’로 시작하는 모든 작업을 지정할 수 있습니다.
```
"action":["name/dts:Describe*"]
```

DTS에서 모든 작업을 지정하려면 아래와 같이 * 와일드카드를 사용합니다.
```
"action"：["name/dts:*"]
```

## DTS 리소스 경로
리소스 경로의 일반 형식은 다음과 같습니다.
```
 qcs::service_type::account:resource
```
- service_type: 제품 약칭. 여기에서는 dts.
- account: uin/32xxx546과 같은 리소스 소유자의 루트 계정 정보
- resource: 서비스의 리소스 상세 정보입니다. 각 DTS 작업(task)이 리소스입니다.

예시는 다음과 같습니다:
```
 "resource": ["qcs::dts::uin/32xxx546:task/dts-kf291vh3"]
```
여기서 dts-kf291vh3은 DTS 작업의 ID, 즉 CAM 정책 설명의 resource입니다.

## 예시
>?다음 예시는 CAM의 사용법만을 보여줍니다. DTS 작업 및 해당 API의 전체 프로세스는 [API 소개](https://intl.cloud.tencent.com/document/product/571/18135)를 참고하십시오.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/dts:DescribeAccessKeys"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/dts:CreateAccess*"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/dts:DescribeMigrateJobs"
            ],
            "resource": [
                "qcs::dts::uin/32xxx546:task/dts-kf291vh3"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/dts:CreateMigrateCheckJob"
            ],
            "resource": [
                "qcs::dts::uin/32xxx546:task/dts-kf291vh3"
            ]
        }
    ]
}
```

