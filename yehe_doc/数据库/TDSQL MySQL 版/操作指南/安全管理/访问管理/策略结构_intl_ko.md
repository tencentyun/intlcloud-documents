
## 정책 구문
CAM 정책 설정 예시:
```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 
```

- **버전 version**: 버전이 필요합니다. 현재 ‘2.0’만 허용됩니다(이 값은 실제로 CAM에서 허용되는 TencentCloud API의 버전을 나타냅니다.).
- **명령 statement**: 하나 또는 다수의 권한과 관련한 자세한 정보를 설명하는 데 사용합니다. 이 요소에는 effect, action, resource, condition 등 기타 여러 요소의 권한 또는 권한 집합이 포함됩니다. 하나의 정책은 하나의 statement 요소만 가지고 있습니다.
 - **작업 action**: 허용되거나 거부된 작업을 설명합니다. 여기에 입력된 action은 ‘dcdb:’ 접두사가 붙고 [TDSQL for MySQL API](https://intl.cloud.tencent.com/document/product/1042/34422)는 접미사가 붙은 문자열입니다. 필수 입력 항목입니다.
 2. **리소스 resource**: 권한 부여의 구체적인 데이터를 기술합니다. 리소스는 6단식 기술을 사용하며, 모든 제품마다 리소스의 정보 정의의 차이가 있습니다. 리소스 정보를 어떻게 지정할 지에 대한 것은 작성한 리소스 선언에 대한 제품 문서를 참고하십시오. 필수 입력 항목입니다.
 3. **조건 condition**: 정책의 효력이 발생하는 규제 조건을 기술합니다. condition에는 오퍼레이터, 작업 키와 작업 값 구성이 포함됩니다. 작업 값은 시간, IP 주소 등의 정보를 포함합니다. 어떤 서비스는 조건에 기타 값을 지정하는 것을 허용합니다. 필수 입력 항목입니다.
 4. **영향 effect**: 명령문에 의해 생성된 결과가 ‘allow’(허용) 또는 ‘deny’(거부)인지 여부를 설명합니다. 필수 입력 항목입니다.

>!기존 이유로 액세스 관리에서 TDSQL for MySQL의 인터페이스 키워드는 dcdb입니다.

## CDB의 작업

TencentDB 정책 설명에서 TencentDB를 지원하는 모든 서비스의 API 작업을 지정할 수 있습니다. dcdb:CreateDBInstance(인스턴스 생성 - 월간 구독) 또는 dcdb:CloseDBExtranetAccess(공용 네트워크 액세스 비활성화)와 같이 dcdb: 접두사가 붙은 API를 TencentDB에 사용해야 합니다.

- 단일 명령문에 여러 작업을 지정하려면 아래와 같이 영어 쉼표로 구분합니다.
```
"action":["dcdb:action1","dcdb:action2"]
```
2. 와일드카드를 사용해서 여러 항목의 작업을 지정할 수도 있습니다. 예를 들어, 다음과 같이 이름이 ‘Describe’로 시작하는 모든 작업을 지정할 수 있습니다.
```
"action":["dcdb:Describe*"]
```
3. 만약 CDB의 모든 작업을 지정할 경우, 다음과 같이 * 와일드카드를 사용하십시오.
```
"action"：["dcdb:*"]
```

## CDB의 리소스

각각의 CAM 정책 명령어는 모두 자신에게 적용되는 리소스가 있습니다.
리소스의 일반 형식은 아래와 같습니다.
```
qcs:project_id:service_type:region:account:resource
```

- **project_id**: 프로젝트 정보 설명은 CAM 초기 로직을 호환하기 위한 것이므로 입력하지 않아도 됩니다.
- **service_type**: dcdb와 같은 제품 약칭입니다.
- **region**: ap-guangzhou와 같은 리전 정보를 설명합니다. 자세한 내용은 [리전 관련 정보](https://intl.cloud.tencent.com/document/api/213/15708)를 참고하십시오.
- **account**: uin/65xxx763과 같은 리소스 소유자의 루트 계정 정보입니다.
- **resource**: instance/instance_id1 또는 instance/*와 같은 각 제품의 구체적인 리소스 정보.

예시: 
- 명령 중인 특정 인스턴스(dcdb-k05xdcta)를 사용하여 아래와 같이 리소스를 지정할 수 있습니다.
```
"resource":[ "qcs::dcdb:ap-guangzhou:uin/65xxx763:instance/dcdb-k05xdcta"]
```
2. * 와일드카드를 사용할 경우에도 아래와 같이 특정 계정의 모든 인스턴스를 지정할 수 있습니다.
```
"resource":[ "qcs::dcdb:ap-guangzhou:uin/65xxx763:instance/*"]
```
3. 모든 리소스를 지정해야 하거나 특정 API 작업이 리소스 권한을 지원하지 않을 경우, 아래와 같이 Resource 요소에서 * 와일드카드를 사용하십시오.
```
"resource": ["*"]
```
4. 단일 명령어에 동시에 여러 리소스를 지정하고 싶을 경우, 영어 쉼표를 이용해 분리하십시오. 다음은 두 개의 리소스를 지정한 예시를 보여 줍니다.
```
"resource":["resource1","resource2"]
```

아래의 표는 CDB가 사용할 수 있는 리소스와 이에 상응하는 리소스의 기술 방법에 대한 설명입니다.
아래의 표에서 $가 접두사인 단어는 모두 별칭입니다.
- 이 중, region은 리전을 나타냅니다.
- 이 중, account는 계정 ID를 나타냅니다.

| 리소스 | 권한 부여 정책 중 리소스 기술 방법 |
|-------|-------|
| 인스턴스 |  `qcs::dcdb:$region:$account:instance/$instanceId` |
