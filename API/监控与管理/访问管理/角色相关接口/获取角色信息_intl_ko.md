## API 설명
이 API(GetRole)는 지정된 역할의 세부 정보를 획득하는 데 사용됩니다.
요청 도메인 이름: cam.api.qcloud.com

## 입력 매개변수
다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

|필드|필수 여부|유형|설명|
| ------------ | ------------ | ------------ | ------------ |
|roleId|아니요|String|역할 ID, 역할을 지정하는 데 사용됩니다. 입력 매개변수 roleId 및 roleName 둘 중에 하나를 선택합니다|
|roleName|아니요|String|역할 이름, 역할을 지정하는 데 사용됩니다. 입력 매개변수 roleId 및 roleName 둘 중에 하나를 선택합니다|

 ## 출력 매개변수

| 필드  | 유형  | 설명  |
| ------------ | ------------ | ------------ |
|  roleId | String  | 역할 ID |
|  roleName | String  | 역할 이름 |
|  policyDocument | String  | 역할의 신뢰 전략 |
|  description | String  | 역할 설명 |
|  addTime | String  | 역할 생성 시간 |
|  updateTime | String  | 역할의 최근 수정 시간  |

## 예제
입력
```
https://cam.api.qcloud.com/v2/index.php?Action=GetRole&roleName=testroleName323&<공통 요청 매개변수>
```

출력
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "roleId": "4611686018427397919",
        "roleName": "testroleName323",
        "policyDocument": "{\"version\":\"2.0\",\"statement\":[{\"action\":\"name/sts:AssumeRole\",\"effect\":\"allow\",\"principal\":{\"qcs\":[\"qcs::cam::uin/2385420691:root\"]}}]}",
        "description": "",
        "addTime": "2017-09-26 11:02:21",
        "updateTime": "2017-09-26 11:02:21"
    }
}

````
