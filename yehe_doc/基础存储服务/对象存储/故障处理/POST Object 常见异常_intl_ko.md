## 장애 현상

COS API를 사용하여 POST 요청 시 다음 예외 오류 코드가 반환됩니다.
- [Condition key q-ak doesn&apos;t match the value XXXXXX](#AccessDenied_q-ak)
- [You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817](#AccessDenied_Expiration)
- [The Signature you specified is invalid.](#SignatureDoesNotMatch_POSTSignature)
- [You must provide condition if you specify a policy in post object request.](#InvalidPolicyDocument_JSONFormat)
- [Condition key bucket doesn&apos;t match the value [bucket-appid]](#AccessDenied_BucketNotConsistent)
- [Condition key key doesn&apos;t match the value XXXXX](#AccessDenied_Condition)
- [The body of your POST request is not well-formed multipart/form-data.](#MalformedPOSTRequest_POSTBody)



## 장애 진단 및 처리

<span id="AccessDenied_q-ak"></span>
### Message: “Condition key q-ak doesn&apos;t match the value XXXXXX”

COS API를 사용하여 POST 요청 시 다음 메시지가 나타납니다.

```
<Code>AccessDenied</Code>
<Message>Condition key q-ak doesn&apos;t match the value XXXXXX</Message>
```

#### 예상 원인

q-ak 매개변수 입력 오류.

#### 해결 방법

1. 액세스 관리 콘솔 로그인 후, [[API 키 관리](https://console.cloud.tencent.com/cam/capi)]페이지로 이동하여 키 정보를 확인하십시오.
2. 조회된 키 정보에 따라 q-ak 매개변수가 잘못 입력되었는지 확인합니다.
 - 해당 오류인 경우: q-ak 매개변수를 올바른 SecretId로 수정하십시오.
 - 해당 오류가 아닌 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.

<span id="AccessDenied_Expiration"></span>
### Message: “You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817” 

COS API를 사용하여 POST 요청 시 다음 메시지가 나타납니다.

```
<Code>AccessDenied</Code>
<Message>You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817</Message>
```


#### 예상 원인

Policy의 expiration 값 만료.

#### 해결 방법

Policy 중의 expiration 값을 수정하십시오.
>! expiration 값은 현재 시간 이후여야 하며, 현재 시간 + 30분(UTC 시간)으로 설정하는 것을 권장합니다.
>


<span id="SignatureDoesNotMatch_POSTSignature"></span>
### Message: “The Signature you specified is invalid.”

COS API를 사용하여 POST 요청 시 다음 메시지가 나타납니다.

```
<Code>SignatureDoesNotMatch</Code>
<Message>The Signature you specified is invalid.</Message>
```

## 예상 원인

서명 계산 오류.

#### 해결 방법

[서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하여 POST 서명 문자열 생성 규칙이 올바른지 확인하십시오.
 - 해당 오류일 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.
 - 해당 오류가 아닐 경우: 온라인 보조 툴: COS 서명 툴을 사용하여 POST 요청 서명을 다시 계산하십시오.


<span id="InvalidPolicyDocument_JSONFormat"></span>
### Message: “You must provide condition if you specify a policy in post object request.”

COS API를 사용하여 POST 요청 시 다음 메시지가 나타납니다.

```
<Code>InvalidPolicyDocument</Code>
<Message>You must provide condition if you specify a policy in post object request.</Message>
```


## 예상 원인

Policy 형식 오류.

#### 해결 방법

[POST Object](https://intl.cloud.tencent.com/document/product/436/14690) 문서를 참고하여, Policy 형식을 표준 JSON형식으로 수정하십시오.


<span id="AccessDenied_BucketNotConsistent"></span>
### Message: “Condition key bucket doesn&apos;t match the value [bucket-appid]”

COS API를 사용하여 POST 요청 시 다음 메시지가 나타납니다.

```
<Code>AccessDenied</Code>
<Message>Condition key bucket doesn&apos;t match the value [bucket-appid]</Message>
```


## 예상 원인

Policy의 bucket이 요청 bucket과 불일치함.

#### 해결 방법

Policy의 bucket을 사용하여 요청하십시오.


<span id="AccessDenied_Condition"></span>
### Message: “Condition key key doesn&apos;t match the value XXXXX”

COS API를 사용하여 POST 요청 시 다음 메시지가 나타납니다.

```
<Code>AccessDenied</Code>
<Message>Condition key key doesn&apos;t match the value XXXXX</Message>
```


## 예상 원인

업로드한 콘텐츠가 policy 규칙에 부합하지 않음.

#### 해결 방법

Policy의 Condition에 따라 해당 조건에 부합하는 콘텐츠를 업로드 합니다.


<span id="MalformedPOSTRequest_POSTBody"></span>
### Message: “The body of your POST request is not well-formed multipart/form-data.”

COS API를 사용하여 POST 요청 시 다음 메시지가 나타납니다.

```
<Code>MalformedPOSTRequest</Code>
<Message>The body of your POST request is not well-formed multipart/form-data.</Message>
```

## 예상 원인

규범에 맞지 않는 POST body 형식.

#### 해결 방법

[POST Object](https://intl.cloud.tencent.com/document/product/436/14690) 문서를 참고하여 body형식을 최적화합니다.




