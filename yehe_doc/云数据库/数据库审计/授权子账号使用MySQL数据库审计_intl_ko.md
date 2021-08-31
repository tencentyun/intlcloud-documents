
디폴트 상태에서, 서브 계정은 MySQL 데이터베이스 감사 기능 사용 권한이 없습니다. 서브 계정의 데이터베이스 감사 기능 사용을 허용하는 정책을 생성해야 합니다. 
서브 계정에 대해 MySQL 데이터베이스 감사 관련 리소스 CAM이 필요하지 않으면 본 문서는 무시하시기 바랍니다. 

[CAM](https://intl.cloud.tencent.com/document/product/598/10583)(Cloud Access Management, CAM)은 Tencent Cloud에서 제공하는 웹 서비스로, 사용자가 Tencent Cloud 계정의 리소스에 대한 액세스 권한을 안전하게 관리하는 데 주로 사용합니다. CAM으로 사용자(그룹)를 생성, 관리 및 폐기할 수 있으며, 신분 관리 및 정책 관리를 통해 누가 어떤 Tencent Cloud 리소스를 사용할지 제어할 수 있습니다.

CAM 사용 시, 정책과 사용자 (그룹)를 연결하여 사용자 (그룹)가 지정된 자원으로 관련 작업을 완성하도록 인증하거나 거부할 수 있습니다. CAM 정책 관련 더 많은 정보는 [정책 구문]   (https://intl.cloud.tencent.com/document/product/598/10603)을 참고하세요. 


## 서브 계정 권한부여
1. 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인한 뒤 사용자 리스트에서 해당 서브 계정을 선택하고 [인증]을 클릭합니다. 
![](https://main.qcloudimg.com/raw/a406ba643c22f2733699cf881ab336fb.png)
2. 팝업 대화 상자에서 [QcloudCDBFullAccess CDB 전체 읽기/쓰기 액세스 권한] 혹은 [QcloudCDBInnerReadOnlyAccess CDB 읽기 전용 액세스 권한]정책 사전 설정을 선택하고 [확인]을 클릭하면 서브 계정 인증이 완료됩니다. 
>?MySQL 데이터베이스 감사는 MySQL 데이터베이스의 하위 모듈로 앞서 말한 MySQL 두 개의 권한 사전 설정 정책에 MySQL 데이터베이스 감사에 필요한 권한 정책이 포함되어 있습니다. 서브 계정에 MySQL 데이터베이스 감사에 필요한 권한만 설정하고 싶다면 [사용자 정의 MySQL 데이터베이스 감사 정책] (#zdymsjksjcl)을 참고하세요. 
>
![](https://main.qcloudimg.com/raw/8500ea99c00fd496139e8535f45dadd2.png)


## [정책 구문] (id:clyf)
MySQL 데이터베이스 감사의 CAM 정책은 다음과 같습니다.  
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
- **영향 effect**: 필수 작성 항목입니다. 선언으로 발생한 결과가 '허용'인지 '명시적 거절'인지 설명합니다. allow(허용) 및 deny(명시적 거절) 두 가지 상황을 포함합니다.
1. **작업 action**: 필수 작성 항목입니다. 허용 또는 거절의 작업을 설명하는데 사용합니다. 작업은 API(접두사 name으로 표시) 또는 기능 집합(특정한 API 조합, 접두사 permid로 표시)이 가능합니다.
- **자원 resource**: 필수 작성 항목입니다. 인증의 구체적인 데이터를 설명합니다. 


## API  작업
CAM 정책 명령에서 CAM 작업을 지원하는 모든 서비스에서 임의로 API 작업을 지정할 수 있습니다. 데이터베이스 감사 기능 API의 접두사는 name/cdb:을 사용하시기 바랍니다. 단일 명령어에서 다수의 작업을 지정할 경우, 쉼표로 다음과 같이 구분해 주시기 바랍니다.
```
"action":["name/cdb:action1","name/cdb:action2"]
```

와일드카드를 사용해서 여러 항목의 작업을 지정할 수 있습니다. 예를 들어, 다음과 같이 명칭이 단어 “Describe”로 시작하는 모든 작업을 지정할 수 있습니다.
```
"action":["name/cdb:Describe*"]
```


## 리소스 경로
리소스 경로의 일반 형식은 다음과 같습니다.
```
qcs::service_type::account:resource
```

- service_type: 제품 약칭. 여기에서는 cdb.
- account: uin/326xxx46과 같은 리소스 소유자의 루트 계정 정보
- resource: 제품의 리소스 상세 내용, MySQL 인스턴스 (instanceId) 한 개가 리소스 한 개에 해당합니다. 

예시는 다음과 같습니다.
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"]
```
그중, cdb-kf291vh3이 MySQL 인스턴스 리소스 ID이며 여기에서는 CAM 정책 명령의 리소스 resource입니다.  

## 예시
다음은 CAM 사용법 예시입니다. MySQL 데이터베이스 감사 관련 전체 API는 [API 문서] (https://cloud.tencent.com/document/product/236/45460)을 참고하시기 바랍니다.  

```
{
    "version": "2.0",
    "statement":[
        {
            "effect": "allow",
            "action": [
                "name/cdb: DescribeAuditRules"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/cdb: CreateAuditPolicy"
            ],
            "resource": [
                "*"
            ]
        },
       
        {
            "effect": "allow",
            "action": [
                "name/cdb: DescribeAuditLogFiles"
            ],
            "resource": [
                "qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"
            ]
        }
    ]
}
```

## [사용자 정의 MySQL 데이터베이스 감사 정책] (id:zdymsjksjcl)
1. 루트 계정으로 [CAM 콘솔] (https://console.cloud.tencent.com/cam/policy)에 로그인한 후 정책 리스트에서 [사용자 정의 정책 생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/772bd2ef82786ef54086307849606b9d.png)
2. 팝업 대화 상자에서 [정책 생성기에서 생성]을 선택합니다. 
3. 서비스와 작업 선택 페이지에서 각 항목의 설정을 선택하고 [성명서 추가]를 클릭한 후 [다음 단계]를 클릭합니다.  
 - 서비스 (Service): [TencentDB for MySQL]을 선택합니다. 
 - 작업 (Action): MySQL  데이터베이스 감사의 모든 API 선택은 [API 문서] (https://cloud.tencent.com/document/product/236/45449)를 참고하세요. 
  - 자원 (Resource): [리소스 설명 방식] (https://intl.cloud.tencent.com/document/product/598/10606)을 참고하세요. *를 입력하면 모든 MySQL 인스턴스를 작업할 수 있는 감사 로그를 보여줍니다.  
![](https://main.qcloudimg.com/raw/ebd4dd9cc00e6caaac6c59ba397fb842.png)
4. 정책 편집 페이지에서 이름 생성 규칙을 누르고 ‘정책 명칭’ (예시: SQLAuditFullAccess)과 ‘설명’을 입력한 후 [완료]를 클릭합니다. 
![](https://main.qcloudimg.com/raw/cb5d0db2683cd54114c5d29685cd1da4.png)
5. 정책 리스트로 돌아가면 방금 생성한 사용자 정의 정책을 조회할 수 있습니다. 
![](https://main.qcloudimg.com/raw/050e310f11386c1b795410150af73b52.png)

