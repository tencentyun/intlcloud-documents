## API 설명
이 API(CreateRole)는 역할을 생성하는 데 사용됩니다.
요청 도메인 이름: cam.api.qcloud.com

## 입력 매개변수
다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

|필드|필수 여부|유형|설명|
| ------------ | ------------ | ------------ | ------------ |
|policyDocument|예|String|역할의 신뢰 전략|
|description|아니요|String|역할 설명|
|roleName|예|String|역할 이름|

## 출력 매개변수
 
| 필드  | 유형  | 설명  |
| ------------ | ------------ | ------------ |
|  roleId | String  | 역할 ID |

## 예제
입력
```
https://cam.api.qcloud.com/v2/index.php?Action=CreateRole&roleName=testroleName
&policyDocument=%7B%22version%22%3A%222.0%22%2C%22statement%22%3A%5B%7B%22action%22%3A%22name%2Fsts%3AAssumeRole%22%2C%22effect%22%3A%22allow%22%2C%22principal%22%3A%7B%22qcs%22%3A%5B%22qcs%3A%3Acam%3A%3Auin%12345678%3Aroot%22%5D%7D%7D%5D%7D&<공통 요청 매개변수>
```
그중에 policyDocument 필드 값: 
{"version":"2.0","statement":[{"action":"name/sts:AssumeRole","effect":"allow","principal":{"qcs":["qcs::cam::uin/12345678:root"]}}]}

출력
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "roleId": "4611686018427397919"
    }
}

````

