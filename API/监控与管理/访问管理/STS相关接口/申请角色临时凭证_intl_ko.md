## API 설명
이 API(AssumeRole)는 역할에 대한 임시 자격 증명을 신청하는 데 사용됩니다.
요청 도메인 이름:

```
sts.api.qcloud.com
```

## 입력 매개변수
다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

|필드|필수 여부|유형|설명|
| ------------ | ------------ | ------------ | ------------ |
|roleArn|예|String|역할 리소스에 대한 설명. 예: qcs::cam::uin/12345678:role/4611686018427397919, qcs::cam::uin/12345678:roleName/testRoleName|
|roleSessionName|예|String|임시 세션 이름(사용자 지정)|
|durationSeconds|아니요|Int|임시 인증서의 유효 기간(초), 기본값은 1800초이며 최대 유효 기간은 7200초입니다|

## 출력 매개변수

| 필드  | 유형  | 설명  |
| ------------ | ------------ | ------------ |
|  credentials | [credentials](#dataStructure)  | 개체에는 token, tmpSecretId, tmpSecretKey 트리플 포함  |

<span id="dataStructure"></span>
## 자격 증명 데이터 구조

| 필드  | 유형  | 설명  |
|---------|---------|---------|
| token | String | token 값 |
| tmpSecretId | String | 임시 보안 인증서 ID |
| tmpSecretKey | String | 임시 보안 인증서 Key |

## 예제
#### 입력

```
https://sts.api.qcloud.com/v2/index.php?Action=AssumeRole&roleArn=qcs%3a%3acam%3a%3auin%2f12345678%3arole%2f4611686018427397919
&roleSessionName=abc&durationSeconds=1800&<공통 요청 매개변수>
```

#### 출력

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "credentials": {
            "sessionToken": "5e776c4216ff4d31a7c74fe194a978a3ff2a42864",
            "tmpSecretId": "AKIDcAZnqgar9ByWq6m7ucIn8LNEuY2MkPCl",
            "tmpSecretKey": "VpxrX0IMCpHXWL0Wr3KQNCqJix1uhMqD"
        },
        "expiredTime": 1506433269,
        "expiration": "2017-09-26T13:41:09Z"
    }
}
```
