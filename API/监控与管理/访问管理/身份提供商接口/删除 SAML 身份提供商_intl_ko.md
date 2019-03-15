### API 설명

이 API(DeleteSAMLProvider)는 SAML ID 공급업체를 삭제하는 데 사용됩니다.
요청 도메인 이름: cam.api.qcloud.com

### 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 나머지 공통 매개변수 리스트는 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/15692)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| name | 예 | String | SAML ID 공급업체 이름|

### 출력 매개변수

없음.


### 예제

IdP라는 SAML ID 공급업체를 삭제합니다

##### 입력 예제:

```
https://cam.api.qcloud.com/v2/index.php?Action=DeleteSAMLProvider
&name=idp
&<공통 요청 매개변수>
```

##### 출력 예제:

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": []
}
```

### 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| InvalidParameter.ProviderNotExist | ID 공급업체가 존재하지 않습니다|
