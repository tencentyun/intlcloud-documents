## API 설명
이 API(GetFederationToken)는 페더레이션 ID에 대한 임시 액세스 증명을 획득하는 데 사용됩니다.
요청 도메인 이름:

```
sts.api.qcloud.com
```

## 입력 매개변수
다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

|필드|필수 여부|유형|설명|
| ------------ | ------------ | ------------ | ------------ |
|name|예|String|페더레이션 ID를 가진 사용자의 별명|
|policy|예|String|전략 설명</br>**주의: **</br>1. policy를 URL 인코딩해야 합니다(GET 방법으로 클라우드 API를 요청할 경우 요청을 보내기 전에 모든 매개변수는 클라우드 API 사양에 따라 다시 한 번 URL 인코딩해야 합니다). </br>2. 전략 구문은 [CAM 전략 구문](https://intl.cloud.tencent.com/document/product/598/10603)을 참조하십시오. </br>3.전략에는 principal 요소를 포함할 수 없습니다.|
|durationSeconds|아니요|Int|임시 인증서의 유효 기간(초), 기본값은 1800초이며 최대 유효 기간은 7200초입니다|

## 출력 매개변수

| 필드  | 유형  | 설명  |
| ------------ | ------------ | ------------ |
|  credentials | [credentials](#dataStructure)  | 개체에는 token, tmpSecretId, tmpSecretKey 트리플 포함  |
|  expiredTime | Int  | 인증서 만료 시간(Unix 타임스탬프로 표시, 단위: 초)  |

<span id="dataStructure"></span>
## 자격 증명 데이터 구조

| 필드  | 유형  | 설명  |
|---------|---------|---------|
| token | String | token 값 |
| tmpSecretId | String | 임시 보안 인증서 ID |
| tmpSecretKey | String | 임시 보안 인증서 Key |

 ## 예제
### 입력

```
https://sts.api.qcloud.com/v2/index.php?Action=GetFederationToken&name=nickName&policy=%7b%22version%22%3a%222.0%22%2c%22statement%22%3a%5b%7b%22action%22%3a%5b%22name%2fqcisa%3aGetInfoByFields%22%5d%2c%22resource%22%3a%5b%22qcs%3a%3aqcisa%3a%3auin%2f90000000000%3aqcisa%2fbigCustomerDetail%22%2c%22qcs%3a%3aqcisa%3a%3auin%2f90000000000%3aqcisa%2fuserDetail%22%2c%22qcs%3a%3aqcisa%3a%3auin%2f90000000000%3aqcisa%2fauthDetail%22%5d%2c%22effect%22%3a%22allow%22%7d%5d%7d&durationSeconds=1800&<공통 요청 매개변수>
```

### 출력

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "credentials": {
            "sessionToken": "9586a03c55b6cc088fb63461e88b4d4b5ceaeebf3",
            "tmpSecretId": "AKIDTs591htUbXKwmQryzpTvBF7nHZgdOlvv",
            "tmpSecretKey": "xjJhtujMq8E8tTcfbTFuRq8JMI7pQtHY"
        },
        "expiredTime": 1494309923
    }
}
```
