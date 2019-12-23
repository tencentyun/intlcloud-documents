## 개요
접근 정책은 COS 리소스 접근 권한 부여에 사용됩니다. 접근 정책은 JSON 에 기반한 접근 정책 언어를 사용합니다. 접근 정책 언어를 통해 지정 의뢰인에게 권한을 부여하여 지정 COS 리소스에 지정 작업을 실행하도록 합니다.

접근 정책 언어는 버킷 정책(Bucket Policy)의 기본 요소와 방법을 설명합니다. 정책 언어에 관련된 설명은 [CAM 정책 관리](https://intl.cloud.tencent.com/document/product/598/10600)를 참조하십시오.

## 접근 정책 요소

접근 정책 언어는 다음 기본 의미의 요소를 포함합니다.
- 의뢰인: 정책 권한 부여를 설명하는 엔터티입니다. 예를 들면, 사용자(개발 업체, 서브 계정, 익명 사용자), 사용자 그룹 등이 있습니다. 이 요소는 버킷 접근 정책에 유효하며 사용자 접근 정책에는 추가하지 말아야 합니다.
- 어구: 한 개 또는 여러 개의 권한을 서술한 세부 정보입니다. 이 요소는 효력, 작업, 리소스, 조건 등 여러 다른 요소를 포함한 권한 또는 권한 집합입니다. 하나의 정책에는 오직 하나의 어구 요소만 존재합니다.
  - 효력: 선언 발생 결과가 "허용" 또는 "명시적 거부"인지를 설명하며 allow와 deny 두 가지 상황을 포함합니다. 이 요소는 필수 입력 항목입니다.
  - 작업: 허용 또는 거절에 대한 작업을 설명하는데 사용됩니다. 작업은 API(name은 접두사임)나 기능 세트(한 그룹의 특정 API, permid 접두사로 설명)로 할 수 있습니다. 해당 요소는 필수 항목입니다.
  - 리소스: 권한 부여에 대한 구체적인 데이터를 설명하는 데 사용됩니다. 리소스는 육단식으로 설명됩니다. 제품마다 리소스 정의에 대한 세부 내용은 일정한 차이가 있습니다. 리소스 정보를 어떻게 지정하는지에 대해서는,귀하가 작성하신 리소스 선언에 해당하는 제품 문서를 참조하십시오. 해당 요소는 필수 항목입니다.
  - 조건: 정책 적용에 대한 제약 조건을 설명하는 데 사용됩니다. 조건은 작업 기호, 작업 키와 작업 값으로 구성되었습니다. 조건값은 시간, IP 주소 등의 정보를 포함하고 있습니다. 일부 서비스는 조건에 다른 값을 지정하는 것을 허용합니다. 해당 요소는 필수 항목이 아닙니다.

## 요소 사용 방법
### 의뢰인 지정
의뢰인 요소는 리소스 접근이 허용 또는 거부되는 사용자, 계정, 서비스 또는 기타 엔터티를 지정하는 데 사용됩니다. 요소 의뢰인은 버킷에서만 역할을 합니다. 사용자 정책은 직접 특정 사용자에게 추가되므로 지정할 필요가 없습니다. 다음은 의뢰인 예시입니다.
```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1:uin/1"
  ]
}
```
익명 사용자 권한 부여:
```json
"principal": {
  "qcs": [
    "qcs::cam::anonymous:anonymous"
  ]
}
```
루트 계정 UIN 1200000313 권한 부여:
```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1200000313:uin/1200000313"
  ]
}
```
서브 계정 UIN 3030313(루트 계정 UIN은 1200000313) 권한 부여:
>**주의:**
> 작업 전, 서브 계정이 기본 계정의 서브 계정 리스트에 추가되었는지 확인하십시오.

```json
"principal": {
  "qcs": [
    "qcs::cam::uin/1200000313:uin/3030313"
  ]
}
```

### 효력 지정
만약 리소스 접근 권한을 명시적 허용(allow)하지 않은 경우, 암시적 접근 거부입니다. 리소스 접근을 명시적 거부(Deny)할 수 있으며 이렇게 사용자가 이 리소스에 접근할 수 없음을 확보하고 다른 정책에서 접근 권한을 부여한 상황에서도 마찬가지입니다. 다음은 허용 효력 지정 예시입니다.
```json
"effect" : "allow"
```

### 작업 지정
COS는 정책에서 지정한 하나의 지정 COS 작업을 정의하였습니다. 지정한 작업과 시작한 API 요청은 완전히 일치합니다.
#### 버킷 작업
| 설명                    | 해당 API                |
| --------------------- | ------------------------ |
| name/cos:GetService   | GET Service              |
| name/cos:GetBucket    | GET Bucket (List Object) |
| name/cos:PutBucket    | PUT Bucket               |
| name/cos:DeleteBucket | DELETE Bucket            |

#### 객체 작업
| 설명                    | 해당 API           |
| --------------------- | ------------- |
| name/cos:GetObject    | GET Object    |
| name/cos:PutObject    | PUT Object    |
| name/cos:HeadObject   | HEAD Object   |
| name/cos:DeleteObject | DELETE Object |

작업 허용의 지정 예시는 다음과 같습니다.
```json
"action": [
  "name/cos:GetObject",
  "name/cos:HeadObject"
]
```

### 리소스 지정
리소스 요소는 COS 버킷 또는 객체 등 한 개 또는 여러 개 작업 대상을 설명합니다. 모든 리소스는 아래 여섯 가지의 설명 방식을 채택할 수 있습니다.
```json
qcs:project_id:service_type:region:account:resource
```

그 중:
1. qcs는 Tencent Cloud 서비스의 약칭입니다.
2. project_id는 프로젝트 정보를 설명하며 단지 CAM 초기 로직의 호환을 위한 것입니다. 여기서는 입력하지 마십시오.
3. service_type는 제품 약칭을 설명합니다. 예: COS
4. region은 지역 정보를 설명합니다. Tencent Cloud COS가 지원하는 [가용 영역](https://cloud.tencent.com/document/product/436/6224)을 참조하십시오.
5. account는 리소스 소유자의 루트 계정 정보를 설명합니다. 현재 두 가지 방식으로 설명한 리소스 소유자를 지원합니다. 한가지 방식은 uin 방식, 즉, 루트 계정의 qq 번호이며 uin/${uin}로 표시됩니다. 예: uin/164256472. 다른 한가지 방식은 uid 방식, 즉, 루트 계정의 appid이며 uid/${appid}로 표시됩니다. 예: uid/1000382392. 현재 COS의 리소스 소유자는 일괄적으로 uid 방식을 사용하여 표시합니다. 즉, 루트 계정의 개발 업체 appid입니다.
6. resource는 구체적 리소스 세부 정보를 설명하며 COS 서비스에서 버킷 XML API 접근 도메인 이름으로 설명합니다.

다음은 지정된 버킷 burningtest-1251500699 예시입니다.
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/*"]
```

다음은 지정된 버킷 burningtest-1251500699의 /test/ 폴더에 있는 모든 객체의 예시입니다.
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/test/*"]
```

다음은 지정된 버킷 burningtest-1251500699의 /test/1.txt 객체의 예시입니다.
```json
"resource": ["qcs::cos:ap-guangzhou:uid/1251500699:burningtest-1251500699/test/1.txt"]
```

### 조건 지정
접근 정책 언어는 권한 부여 시 조건을 지정합니다. 예: 사용자 접근 출처의 제한, 권한 부여 시간 제한 등. 다음은 현재 지원하는 조건 연산자 리스트 및 일반적으로 사용되는 조건 키와 예시 등 정보를 나열한 것입니다.

| 조건 연산자                   | 설명     | 조건 이름              | 예시                                       |
| ----------------------- | ------ | ---------------- | ---------------------------------------- |
| ip_equal                | IP는 다음과 같음  | qcs:ip           | {"ip_equal":{"qcs:ip ":"10.121.2.0/24"}} |
| ip_not_equal            | IP는 다음과 같지 않음 | qcs:ip           | {"ip_not_equal":{"qcs:ip ":["10.121.1.0/24", "10.121.2.0/24"]}} |
| date_not_equal          | 시간은 다음과 같지 않음  | qcs:current_time | {"date_not_equal":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than       | 시간은 다음보다 큼   | qcs:current_time | {" date_greater_than ":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_greater_than_equal | 시간은 다음과 같거나 큼 | qcs:current_time | {" date_greater_than_equal ":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |
| date_less_than          | 시간은 다음보다 작음  | qcs:current_time | {" date_less_than ":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal    | 시간은 다음과 같거나 작음 | qcs:current_time | {" date_less_than ":{"qcs:current_time":"2016-06-01T 00:01:00Z"}} |
| date_less_than_equal    | 시간은 다음과 같거나 작음 | qcs:current_time | {"date_less_than_equal ":{"qcs:current_time":"2016-06-01T00:01:00Z"}} |

다음은 접근 IP가 10.121.2.0/24 IP 주소 범위를 충족하는 예시입니다.

```json
"ip_equal":{"qcs:ip ":"10.121.2.0/24"}
```

다음은 접근 IP 가 101.226.\*\*\*.185와 101.226.\*\*\*.186를 충족하는 예시입니다.

```json
"ip_equal": {
  "qcs:ip": [
    "101.226.***.185",
    "101.226.***.186"
  ]
}
```

## 실제 사례

루트 계정이 익명 사용자를 허용하고 접근 출처 IP가 101.226.\*\*\*.185/101.226.\*\*\*.186 일 때, 화남 지역의 버킷 burningtest-1251500699 중의 객체에 GET(다운로드)와 HEAD 작업을 실행하며 인증이 필요하지 않습니다. 더 많은 사례는 [권한 설정 관련 사례](https://cloud.tencent.com/document/product/436/12514)를 참조하십시오.

```json
{
   "version": "2.0",
   "principal": {
      "qcs": [
         "qcs::cam::anonymous:anonymous"
      ]
   },
    "statement": [
        {
            "action": [
                "name/cos:GetObject",
                "name/cos:HeadObject"
            ],
            "condition": {
                "ip_equal": {
                    "qcs:ip": [
                        "101.226.***.185",
                        "101.226.***.186"
                    ]
                }
            },
            "effect": "allow",
            "resource": [
                "qcs::cos:cn-south:uid/1251500699:burningtest-1251500699.cn-south.myqcloud.com/*"
            ]
        }
    ]
}
```

