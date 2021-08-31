
<span id = "celueyufa"></span>
## 정책 구문
CAM 정책:
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
- **버전 version**: 필수 작성 항목입니다. 현재는 “2.0”만 허용합니다.
- **명령 statement**: 하나 또는 다수의 권한과 관련한 자세한 정보를 설명하는 데 사용합니다. 이 요소에는 effect, action, resource, condition 등 기타 여러 요소의 권한 또는 권한 집합이 포함됩니다. 하나의 정책은 하나의 statement 요소만 가지고 있습니다.
 - **영향 effect**: 필수 작성 항목입니다. 선언으로 발생한 결과가 '허용'인지 '명시적 거절'인지 설명합니다. allow(허용) 및 deny(명시적 거절) 두 가지 상황을 포함합니다.
 - **작업 action**: 필수 작성 항목입니다. 허용 또는 거절의 작업을 설명하는 데 사용합니다. action은 API(접두사 cdb로 표시)가 가능합니다.
 - **리소스 resource**: 필수 작성 항목입니다. 권한 부여의 구체적인 데이터를 설명합니다. resource는 6단식 기술을 사용하며, 모든 제품마다 리소스의 정보 정의에 차이가 있습니다.
 - **효력 발생 조건 condition**: 필수 작성 항목입니다. 정책의 효력이 발생하는 규제 조건을 설명합니다. condition에는 오퍼레이터, 작업 키와 작업 값 구성이 포함됩니다. 작업 값은 시간, IP 주소 등의 정보를 포함합니다. 어떤 서비스는 조건에 기타 값을 지정하는 것을 허용합니다.

<span id = "caozuo"></span>
## CDB의 작업
CDB 정책 명령어에서 CDB를 지원하는 특정 서비스로부터 임의의 API 작업을 지정할 수 있습니다. CDB의 경우 cdb:는 접두사 API입니다. 예시로 cdb:CreateDBInstance 또는 cdb:CreateAccounts가 있습니다.

만약 단일 명령어에 여러 개의 작업을 지정하고 싶을 경우, 다음과 같이 쉼표를 사용하여 작업을 분리하십시오.
```
"action":["cdb:action1","cdb:action2"]
```
와일드카드를 사용해서도 여러 항목의 작업을 지정할 수 있습니다. 예를 들어, 다음과 같이 표시해 명칭이 단어 “Describe”로 시작하는 모든 작업을 지정할 수 있습니다.
```
"action":["cdb:Describe*"]
```
만약 CDB의 모든 작업을 지정할 경우, 다음과 같이 * 와일드카드를 사용하십시오.
```
"action"：["cdb:*"]
```

<span id = "ziyuanlujing"></span> 
## CDB의 리소스
각 CAM 정책 명령어에는 모두 개별적으로 적용되는 리소스가 있습니다.
리소스의 일반 형식은 아래와 같습니다.
```
qcs:project_id:service_type:region:account:resource
```
- **project_id**: 프로젝트 정보 설명은 CAM 초기 로직을 호환하기 위한 것이므로 입력하지 않아도 됩니다.
- **service_type**: cdb와 같은 제품 약칭
- **region**: ap-guangzhou와 같은 리전 정보
- **account**: uin/653339763과 같은 리소스 소유자의 루트 계정 정보
- **resource**: instanceId/instance_id1 또는 instanceId/*와 같은 각 제품의 구체적인 리소스 정보


예를 들어, 명령 중인 특정 인스턴스(cdb-k05xdcta)를 사용하여 아래와 같이 리소스를 지정할 수 있습니다.
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/cdb-k05xdcta"]
```
* 와일드카드를 사용할 경우에도 아래와 같이 특정 계정의 모든 인스턴스를 지정할 수 있습니다.
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/*"]
```
모든 리소스를 지정해야 하거나 특정 API 작업이 리소스 권한을 지원하지 않을 경우, 아래와 같이 resource 요소에서 * 와일드카드를 사용하십시오.
```
"resource": ["*"]
```
단일 명령어에 동시에 여러 리소스를 지정하고 싶을 경우, 쉼표를 이용해 분리하십시오. 다음은 두 개의 리소스를 지정한 예시를 보여 줍니다.
```
"resource":["resource1","resource2"]
```

아래의 표에서는 CDB가 사용할 수 있는 리소스와 대응하는 리소스의 설명 방법이 나타나 있습니다. 이 중 $가 접두사인 단어는 모두 별명이며 region은 리전, account는 계정 ID입니다.

| 리소스 | 권한 부여 정책 중 리소스 설명 방법 |
|-------|-------|
|인스턴스|  `qcs::cdb:$region:$account:instanceId/$instanceId`|
|VPC|  `qcs::vpc:$region:$account:vpc/$vpcId`|
|보안 그룹|  `qcs::cvm:$region:$account:sg/$sgId`|
