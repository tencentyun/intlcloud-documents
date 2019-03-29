### API 설명
이 API(UpdateSAMLProvider)는 SAML ID 공급업체 설명 또는 메타 데이터 문서를 업데이트하는 데 사용됩니다.
요청 도메인 이름: cam.api.qcloud.com
요청 방식: HTTP POST

### 입력 매개변수
다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 나머지 공통 매개변수 리스트는 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/15692)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| name | 예 | String | SAML ID 공급업체 이름 |
| desc | 아니요 | String | ID 공급업체 설명 |
| SAMLMetadataDocument | 아니요 | String | SAML ID 공급업체 메타 데이터 문서. Base64로 인코딩해야 하며 최대 64KB를 지원합니다. |

비고: IdP 메타 데이터 문서가 상한을 초과하는 경우 메타 데이터 XML 문서에서 IDPSSODescriptor를 제외한 다른 XML 노드를 삭제할 수 있습니다.

### 출력 매개변수

없음.


### 예제

IdP라는 SAML ID 공급업체 설명의 업데이트 및 메타 데이터 문서

##### 입력 예제:

```
POST /v2/index.php HTTP/1.1
Host: cam.api.qcloud.com
Accept: */*
Content-Length: 3927
Content-Type: application/x-www-form-urlencoded

Action=UpdateSAMLProvider&name=idp&SAMLMetadataDocument=U0FNTE1ldGFkYXRhRG9jdW1lbnQgdjI=&desc=descriptor2&<공통 요청 매개변수>
```
##### 출력 예제:

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": [
    ]
}
```

### 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| InvalidParameter.ProviderNotExist| ID 공급업체가 존재하지 않습니다 |
| InvalidParameter.SAMLMetadataDocument | SAML ID 공급업체 메타 데이터 문서 오류 |
