### API 설명

이 API(ListSAMLProviders)는 SAML ID 공급업체 리스트를 획득하는 데 사용됩니다.
요청 도메인 이름: cam.api.qcloud.com

### 입력 매개변수
다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 나머지 공통 매개변수 리스트는 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/15692)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명|
|---------|---------|---------|---------|
|page | 예 | Integer | 페이지 번호 |
|rp | 예 |Integer | 페이지 크기 |

### 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| total | Integer | ID 공급업체의 총 수 |
| list | Array Of SAMLProvider | SAML ID 공급업체 리스트 |

SAMLProvider 필드는 다음과 같습니다.

| 이름 | 유형 | 설명 |
|---------|---------|---------|
| name | String | ID 공급업체 이름 |
| desc | String | ID 공급업체 설명|
| createTime | Date | ID 공급업체 생성 시간 |
| modifyTime | Date| ID 공급업체 업데이트 시간 |


###  예제

SAMl ID 공급업체 리스트를 조회합니다.

##### 입력 예제:

```
https://cam.api.qcloud.com/v2/index.php?Action=ListSAMLProviders
&page=1
&rp=5
&<공통 요청 매개변수>
```

##### 출력 예제:

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "total": 9,
        "list": [
            {
                "name": "api-test-v2",
                "desc": "API 테스트 12121",
                "createTime": "2018-10-30 14:43:37",
                "modifyTime": "2018-10-30 14:57:35"
            },
            {
                "name": "api-test",
                "desc": "API 테스트",
                "createTime": "2018-10-30 11:40:19",
                "modifyTime": "2018-10-30 11:40:19"
            },
            {
                "name": "aaaaaaaaaaa",
                "desc": "테스트",
                "createTime": "2018-10-17 17:16:17",
                "modifyTime": "2018-10-17 17:16:17"
            },
            {
                "name": "test1112222",
                "desc": "111111",
                "createTime": "2018-10-15 21:30:08",
                "modifyTime": "2018-10-15 21:30:08"
            },
            {
                "name": "test111",
                "desc": "111111",
                "createTime": "2018-10-12 18:09:19",
                "modifyTime": "2018-10-12 18:09:19"
            }
        ]
    }
}
```

###  오류 코드
다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.
