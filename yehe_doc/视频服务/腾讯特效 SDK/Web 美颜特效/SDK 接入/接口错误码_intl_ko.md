
## SDK 내장 API 에러 코드
`webar.qcloud.com/sdk/xxx`에서 반환된 에러 코드(예: `https://webar.qcloud.com/sdk/verify`).
Response 구조는 다음과 같습니다.

```js
{
    "Code": xxx,
    "Message": "xxx"
}
```


### 성공한 요청 
 Code가 0이면 요청이 성공하고 Data에 정보가 반환됩니다.

```json
{
    Code: 0,
    Data:{...}
}
```


### 인증 오류
 Code가 100 –- 104 사이의 값이면 인증 오류가 발생한 것입니다. response Status 코드는 401입니다.
```json
{
  "100":{
    zh: "인증 매개변수 누락"
  },
  "101":{
    zh: "signature 시간 초과"
  },
  "102":{
    zh: "사용자를 찾을 수 없음"
  },
  "103":{
    zh: "signature 오류"
  },
  "104":{
    zh: "referer 또는 WeChatAppId 불일치"
  }
}
 

```

### 요청 매개변수 오류
Code = -2이면 요청 매개변수 오류가 발생한 것입니다. 자세한 내용은 Message의 값을 참고하십시오.

```json

{
    "Code": -2,
    "Message": "LicenseKey는 문자열이어야 함"
}
```

### 비즈니스 인증 오류
Code > 1000이면 비즈니스 인증 오류가 발생한 것입니다. 자세한 내용은 Message의 값을 참고하십시오.

```json
{
    "Code": 2007,
    "Message": "프로젝트가 존재하지 않음"
}
```

### 알 수 없는 오류
Code = -1이면 알 수 없는 오류가 발생한 것입니다.
```json
{
    "Code": -1,
    "Message": "알 수 없는 오류"
}
```
