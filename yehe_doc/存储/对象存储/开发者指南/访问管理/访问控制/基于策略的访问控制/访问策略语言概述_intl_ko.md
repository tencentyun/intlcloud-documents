>!서브 계정 또는 협업 파트너에게 액세스 정책을 추가할 때, 반드시 업무상 필요에 따라 최소 권한 원칙에 근거하여 권한을 부여해야 합니다. 서브 계정이나 협업 파트너에게 리소스 `(resource:*)`나 작업 `(action:*)`에 대한 모든 권한을 부여하면 권한 범위가 너무 광범위해 데이터 보안에 리스크가 발생할 수 있습니다.

## 개요

액세스 정책은 COS 리소스에 액세스 권한을 부여하는 데 사용됩니다. 액세스 정책은 JSON 언어를 기반으로 합니다. 액세스 정책 언어를 통해 지정 위탁자(principal)에게 권한을 부여하여 지정 COS 리소스에 지정 작업을 실행할 수 있습니다.

액세스 정책 언어는 버킷 정책(Bucket Policy)의 기본 요소와 용법을 설명합니다. 정책 언어에 관한 자세한 설명은 [CAM 정책 관리](https://intl.cloud.tencent.com/document/product/598/10600)를 참조하십시오.

## 액세스 정책 요소

액세스 정책 언어는 다음의 기본 요소를 포함합니다.

- **위탁자(principal)**: 정책에 의해 권한이 부여되는 엔티티입니다. 예시로 사용자(루트 계정, 서브 계정, 익명 사용자), 사용자 그룹 등이 있습니다. 이 요소는 사용자 액세스 정책이 아닌 버킷 액세스 정책에 유효합니다.
- **명령어(statement)**: 하나 또는 여러 개의 권한의 자세한 정보를 기술하는 데 사용합니다. 이 요소에는 효력, 작업, 리소스, 조건 등의 기타 여러 요소의 권한 또는 권한 집합이 포함됩니다. 하나의 정책에는 하나의 명령 요소만 가지고 있습니다.
- **효력(effect)**: 선언으로 발생한 결과가 “허용”인지 “명시적 거부”인지 기술합니다. allow 및 deny 두 가지 상황을 포함합니다. 이 요소는 필수 항목입니다.
- **작업(action)**: 허용 또는 거부의 작업을 기술하는 데 사용합니다. 작업은 API(접두사 name으로 표시) 또는 기능 집합(특정한 API 구성, 접두사 permid로 표시)이 가능합니다. 이 요소는 필수 항목입니다.
- **리소스(resource)**: 권한 부여의 구체적인 데이터를 기술합니다. 리소스는 6단식 기술을 사용하며, 모든 제품마다 리소스의 정보 정의의 차이가 있습니다. 리소스 정보를 어떻게 지정할 지에 대한 것은 작성한 리소스 선언에 대한 제품 문서를 참조하십시오. 이 요소는 필수 항목입니다.
- **조건(condition)**: 정책의 효력이 발생하는 규제 조건을 기술합니다. 조건에는 오퍼레이터, 작업 키와 작업 값 구성이 포함됩니다. 조건 값은 시간, IP 주소 등의 정보를 포함합니다. 어떤 서비스는 조건에 기타 값을 지정하는 것을 허용합니다. 이 요소는 필수 항목입니다.

## 요소 사용법

### 지정 위탁자

위탁자(principal) 요소는 리소스 사용자, 계정, 서비스 또는 기타 엔티티의 액세스를 허용 또는 거부하는 데 사용됩니다. 위탁자 요소는 버킷에서만 작용합니다. 사용자 정책으로 인해 특정 사용자에게 바로 추가되므로 사용자 정책에서는 지정할 필요가 없습니다. 다음은 위탁자 지정 예시입니다.

```json
"principal": {
"qcs": [
"qcs::cam::uin/100000000001:uin/100000000001"
]
}
```

익명 사용자에 권한 부여

```json
"principal": {
"qcs": [
"qcs::cam::anonymous:anonymous"
]
}
```

루트 계정 UIN 100000000001에 권한 부여

```json
"principal": {
"qcs": [
"qcs::cam::uin/100000000001:uin/100000000001"
]
}
```

서브 계정 UIN 100000000011(루트 계정 UIN은 100000000001)에 권한 부여

> !작업을 수행하기 전 서브 계정이 루트 계정의 서브 계정 리스트에 추가되었는지 확인하십시오.

```json
"principal": {
"qcs": [
"qcs::cam::uin/100000000001:uin/100000000011"
]
}
```

### 지정 효력

리소스 액세스 권한을 명시적으로 부여(허용)하지 않는 경우 액세스가 암묵적으로 거부됩니다. 또한 리소스에 대한 액세스를 명시적으로 거부(deny)할 수 있어 이런 방식으로 사용자 리소스 접근 불가 설정을 할 수 있습니다. 기타 정책으로 액세스 권한을 부여하는 경우에도 마찬가지입니다. 다음은 효력을 허용하도록 지정하는 예시입니다.

```json
"effect" : "allow"
```

### 지정 작업

COS는 정책에서 특정한 COS 작업을 지정할 수 있으며, 지정 작업과 API 요청 발송 작업은 완전히 일치합니다. 다음은 일부 버킷 작업과 객체 작업입니다. 자세한 내용은 [API 작업 리스트](https://intl.cloud.tencent.com/document/product/436/10111) 문서를 참조하십시오.

#### 버킷 작업


| 설명                  | 해당 API 인터페이스 |
| --------------------- | ------------------------ |
| name/cos:GetService   | GET Service              |
| name/cos:GetBucket    | GET Bucket (List Objects) |
| name/cos:PutBucket    | PUT Bucket               |
| name/cos:DeleteBucket | DELETE Bucket            |

#### 객체 작업

| 설명                  | 해당 API 인터페이스 |
| --------------------- | --------------- |
| name/cos:GetObject    | GET Object      |
| name/cos:PutObject    | PUT Object      |
| name/cos:HeadObject   | HEAD Object     |
| name/cos:DeleteObject | DELETE Object   |

허용된 작업의 예시는 다음과 같습니다.

```json
"action": [
"name/cos:GetObject",
"name/cos:HeadObject"
]
```

### 지정 리소스

리소스(resource)요소는 하나 또는 여러 작업 객체를 기술합니다. 예시로 COS 버킷 또는 객체 등이 있으며, 모든 리소스는 6단식 기술을 사용합니다.

```json
qcs:project_id:service_type:region:account:resource
```

다음은 매개변수에 대한 설명입니다.

매개변수|설명|필수 여부
--|--|--
qcs |는 qcloud service의 약칭으로 Tencent Cloud의 클라우드 서비스를 의미합니다.|필수
project_id |항목 정보이며 CAM 초기 로직에만 호환됩니다.|옵션
service_type |COS와 같은 제품 약칭입니다.|필수
region |리전 정보입니다. Tencent Cloud COS가 지원하는 [사용 가능 리전](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오.|필수
account |리소스 소유자의 루트 계정 정보이며, 리소스 소유자를 설명하는 두가지 방식을 지원합니다. 첫 번째 방식은 uin 방식, 즉 루트 계정의 UIN 계정이며 `uin/${OwnerUin}`로 표시됩니다(예: uin/100000000001). 또 다른 방식은 uid 방식, 즉 루트 계정의 APPID이며 `uid/${appid}`로 표시됩니다(예: uid/1250000000). 현재 COS의 리소스 소유자는 일괄적으로 uid 방식을 사용해 표시합니다. 즉 루트 계정의 개발사 APPID입니다.|필수
resource |구체적인 리소스 세부 내용입니다. COS 서비스에서는 버킷 XML API 호출 도메인을 사용해 설명합니다.|필수

다음은 지정 버킷 examplebucket-1250000000의 예시입니다.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"]
```

다음은 지정 버킷 examplebucket-1250000000의 /folder/ 폴더에 있는 모든 객체 예시입니다.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/folder/*"]
```

다음은 지정 버킷 examplebucket-1250000000에 있는 /folder/exampleobject 객체 예시입니다.

```json
"resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/folder/exampleobject"]
```

### 지정 조건

권한을 부여 받을 경우 액세스 정책 언어로 조건을 지정할 수 있습니다. 사용자 액세스 제한, 권한 부여 시간 제한 등이 그 예입니다. 다음은 현재 지원하는 조건 오퍼레이터 리스트 및 통용되는 조건 키, 예시 등의 정보입니다.

| 조건 오퍼레이터 | 의미 | 조건 이름 | 예시 |
| ----------------------- | ------------ | ---------------- | ------------------------------------------------------------ |
| ip_equal                | IP 일치      | qcs:ip           | {"ip_equal":{"qcs:ip ":"10.121.2.0/24"}}                     |
| ip_not_equal            | IP 불일치    | qcs:ip           | {"ip_not_equal":{"qcs:ip ":["10.121.1.0/24", "10.121.2.0/24"]}} |


다음은 액세스 IP가 IP 대역 내에 있는 10.121.2.0/24 예시입니다.

```json
"ip_equal":{"qcs:ip ":"10.121.2.0/24"}
```

다음은 액세스 IP가 101.226.\*\*\*.185와 101.226.\*\*\*.186인 예시입니다.

```json
"ip_equal": {
"qcs:ip": [
"101.226.***.185",
"101.226.***.186"
]
}
```

## 실제 사례

루트 계정이 익명 사용자를 허용하고 액세스 출처 IP가 101.226.\*\*\*.185/101.226.\*\*\*.186인 경우 화난지역의 버킷이 examplebucket-1250000000인 객체에 대해 GET(다운로드)과 HEAD 작업을 실행하여 인증할 필요가 없습니다. 자세한 내용은 [권한 제한 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참조하십시오.

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
"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/*"
]
}
]
}
```
