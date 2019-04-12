__1. API 설명__ 
이 API(DescribeRoleList)는 지정된 역할의 세부 정보를 획득하는 데 사용됩니다.
요청 도메인 이름: cam.api.qcloud.com

__2. 입력 매개변수__ 
다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

|필드|필수 여부|유형|설명|
| ------------ | ------------ | ------------ | ------------ |
|page|예|int|페이지 번호, 초시값: 1|
|rp|예|int|페이지당 크기, 200보다 클 수 없음|


 __3. 출력 매개변수__ 

| 필드  | 유형  | 설명  |
| ------------ | ------------ | ------------ |
|  totalNum | int  | 이 owner의 총 역할 수 |
|  list | array  | 역할 리스트 |

list 필드의 각 역할은 다음 정보를 표시합니다 
 
| 필드  | 유형  | 설명  |
| ------------ | ------------ | ------------ |
|  roleId | String  | 역할 ID |
|  roleName | String  | 역할 이름 |
|  policyDocument | String  | 역할의 신뢰 전략 |
|  description | String  | 역할 설명 |
|  addTime | String  | 역할 생성 시간 |
|  updateTime | String  | 역할의 최근 수정 시간  |


 __4. 예제__ 
입력
```
https://cam.api.qcloud.com/v2/index.php?Action=DescribeRoleList&page=1&rp=10&<공통 요청 매개변수>
```

출력
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 2,
        "list": [
            {
                "roleId": "4611686018427397919",
                "roleName": "testroleName001",
                "policyDocument": "{\"version\":\"2.0\",\"statement\":[{\"action\":\"name/sts:AssumeRole\",\"effect\":\"allow\",\"principal\":{\"qcs\":[\"qcs::cam::uin/888888888:root\"]}}]}",
                "description": "",
                "addTime": "2017-09-26 11:02:21",
                "updateTime": "2017-09-26 11:02:21"
            },
            {
                "roleId": "4611686018427397919",
                "roleName": "testroleName002",
                "policyDocument": "{\"version\":\"2.0\",\"statement\":[{\"action\":\"name/sts:AssumeRole\",\"effect\":\"allow\",\"principal\":{\"qcs\":[\"qcs::cam::uin/12345678:root\"]}}]}",
                "description": "",
                "addTime": "2017-09-25 15:19:29",
                "updateTime": "2017-09-25 15:19:29"
            }
        ]
    }
}
````

