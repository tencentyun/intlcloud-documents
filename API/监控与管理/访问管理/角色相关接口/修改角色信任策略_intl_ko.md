## API 설명
이 API(UpdateAssumeRolePolicy)는 역할의 신뢰 전략을 수정하는 데 사용됩니다.
요청 도메인 이름: cam.api.qcloud.com

## 입력 매개변수
다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

|필드|필수 여부|유형|설명|
| ------------ | ------------ | ------------ | ------------ |
|policyDocument|예|String|역할의 신뢰 전략|
|roleId|아니요|String|역할 ID, 역할을 지정하는 데 사용됩니다. 입력 매개변수 roleId 및 roleName 둘 중에 하나를 선택합니다|
|roleName|아니요|String|역할 이름, 역할을 지정하는 데 사용됩니다. 입력 매개변수 roleId 및 roleName 둘 중에 하나를 선택합니다|

## 출력 매개변수

| 필드  | 유형  | 설명  |
| ------------ | ------------ | ------------ |
| code | Int | 공통 오류 코드, 0은 성공을 의미하고 다른 값은 실패를 나타냅니다. 자세한 내용은 오류 코드 페이지의 <a href='https://cloud.tencent.com/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81' title='공통 오류 코드'>공통 오류 코드</a>를 참조하십시오.|
| message | String | 모듈 오류 메시지 설명, API와 관련됩니다.|
| codeDesc | String | 영어 오류 설명 |

## 예제
입력
```
https://cam.api.qcloud.com/v2/index.php?Action=UpdateAssumeRolePolicy&roleName=testroleName
&policyDocument=%7B%22version%22%3A%222.0%22%2C%22statement%22%3A%5B%7B%22action%22%3A%22name%2Fsts%3AAssumeRole%22%2C%22effect%22%3A%22allow%22%2C%22principal%22%3A%7B%22qcs%22%3A%5B%22qcs%3A%3Acam%3A%3Auin%2F909619400%3Aroot%22%5D%7D%7D%5D%7D&<공통 요청 매개변수>
```
그중에 policyDocument 필드 값:
{"version":"2.0","statement":[{"action":"name/sts:AssumeRole","effect":"allow","principal":{"qcs":["qcs::cam::uin/909619400:root"]}}]}

출력
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": []
}

````
