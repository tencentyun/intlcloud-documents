## API 설명

이 API(ListAttachedRolePolicies)는 역할에 바인딩된 전략 리스트를 획득하는 데 사용됩니다.
요청 도메인 이름:

```
cam.api.qcloud.com
```

## 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

| 매개변수 이름   | 유형   | 필수 여부 | 설명                                                         |
| ---------- | ------ | ---- | ------------------------------------------------------------ |
| roleId     | String | 아니요   | 역할 ID. 역할을 지정하는 데 사용됩니다. 입력 매개변수 roleId 및 roleName 둘 중에 하나를 선택합니다        |
| roleName   | String | 아니요   | 역할 이름. 역할을 지정하는 데 사용됩니다. 입력 매개변수 roleId 및 roleName 둘 중에 하나를 선택합니다         |
| page       | int    | 아니요   | 페이지 번호, 초시값: 1, 기본값: 1                                  |
| rp         | int    | 아니요   | 페이지당 크기. 기본값: 20                                        |
| policyType | String | 아니요   | 가능한 값 User는 사용자 지정 전략만 조회한다는 것을 의미하며 QCS는 미리 설정 전략만 조회하고 값을 지정하지 않으면 모든 전략을 조회한다는 것을 의미합니다 |

## 출력 매개변수

| 필드     | 유형  | 설명                                                         |
| -------- | ----- | ------------------------------------------------------------ |
| totalNum | int   | 총 전략 수                                                     |
| list     | array | 전략 배열, 배열의 각 멤버는 다음 필드가 포함됩니다. <li>policyId: 전략 ID<li>policyName: 전략 이름<li>addTime: 전략 생성 시간<li>description: 전략 설명<li> createMode: 1은 비즈니스 권한에 의해 생성된 전략을 의미하며 다른 값은 전략 구문을 확인하고 전략 구문을 통해 전략을 업데이트할 수 있는 것을 의미합니다|

## 예제
### 입력
```
https://cam.api.qcloud.com/v2/index.php
?roleName=testRole
&page=1
&rp=20
&SignatureMethod=HmacSHA256
&Action=ListAttachedRolePolicies
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=33994
&Timestamp=1508492653
&RequestClient=SDK_PHP_1.1
&Signature=YQflvL9ZCPDfTJNum84oXRQex6iKKTNi2fwgLUh2qZE%3D
```

### 출력

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 3,
        "list": [
            {
                "policyId": 524497,
                "policyName": "testpppName323",
                "addTime": "2017-10-20 17:26:16",
                "policyType": "User",
                "createMode": 2
            },
            {
                "policyId": 296232,
                "policyName": "QcloudCCSInnerFullAccess",
                "addTime": "2017-10-20 17:11:19",
                "policyType": "QCS",
                "createMode": 2
            },
            {
                "policyId": 219851,
                "policyName": "QcloudCLBReadOnlyAccess",
                "addTime": "2017-09-04 16:40:15",
                "policyType": "QCS",
                "createMode": 2
            }
        ]
    }
}
```

## 오류 코드
[오류 코드](https://intl.cloud.tencent.com/document/product/598/13884)를 참조하십시오.
