
Cloud Object Storage(COS)는 객체 업로드 시 업로드하는 객체의 파일 크기를 제한하여 스토리지 용량을 더 효율적으로 관리할 수 있으며, 너무 크거나 작은 파일의 업로드로 인한 스토리지 용량 및 네트워크 대역폭이 낭비되지 않도록 방지합니다. 다음 두 사례를 예시로 파일 업로드 크기를 정교하게 관리하는 방법에 대해 소개합니다.

## 준비 작업

다음 사례에서는 아래와 같은 정보를 사용합니다.
- 루트 계정의 APPID: 1250000000
- 버킷 이름: examplebucket-1250000000

실제 사용 시에는 사용자 루트 계정 및 버킷으로 대체하여 사용하십시오.


## 사례1: POST Object로 객체 업로드 시 객체 크기 범위 지정

POST Object로 객체 업로드 시 테이블에 'content-length-range' 필드를 추가하여 해당 요청의 객체 크기를 제한할 수 있습니다. 포맷은 다음과 같습니다.

```plaintext
[ "content-length-range", minNum, maxNum ]
```

예시는 다음과 같습니다.

```plaintext
[ "content-length-range", 1, 10]
```

해당 필드는 JSON 형식으로 POST 요청 테이블의 정책(policy) - 조건(condition)에 추가합니다. 해당 필드를 추가한 전체 정책(policy)은 다음과 같습니다.

```plaintext
 {
    "expiration": "2021-12-31T12:00:00Z",
    "conditions": [
        { "bucket": "examplebucket-1250000000" },
        [ "starts-with", "$key", "exampleobject" ],
        { "q-ak": "AKIDQjz3ltompVjBni5LitkWHFlFpwkn****" },
        { "q-sign-algorithm": "sha1" },
        { "q-sign-time": "1567150692;1567157892" },
        [ "content-length-range", 1, 10 ]
    ]
}
```

전체 요청 구성 방법은 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) API 문서를 참조하십시오.

#### 응답

업로드하는 객체 파일 크기가 조건을 만족하면 반환에 성공합니다. 예시는 다음과 같습니다.

```plaintext
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Wed, 23 Aug 2020 08:14:53 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxMzZfMmViMDJhMDlfY2NjOF84NGQz****
```

업로드하는 객체 파일 크기가 지정 범위를 초과하면 반환에 실패합니다.

객체가 너무 큰 경우 다음과 같이 응답합니다.

```plaintext
HTTP/1.1 400 Bad Request
Content-Type: application/xml
Content-Length: 498
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****



<?xml version='1.0' encoding='utf-8' ?>
<Error>
        <Code>EntityTooLarge</Code>
        <Message>Condition key content-length-range doesn‘t match the value </Message>
        <Resource>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject</Resource>
        <RequestId>NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****</RequestId>
</Error>
```

객체가 너무 작은 경우 다음과 같이 응답합니다.

```plaintext
HTTP/1.1 400 Bad Request
Content-Type: application/xml
Content-Length: 498
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****



<?xml version='1.0' encoding='utf-8' ?>
<Error>
        <Code>EntityTooSmall</Code>
        <Message>Condition key content-length-range doesn‘t match the value </Message>
        <Resource>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject</Resource>
        <RequestId>NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****</RequestId>
</Error>
```



## 사례2: 임시 키 신청 시 객체 크기 범위 지정

사례1은 사용이 간편하다는 것이 장점이며, 요청 테이블에 매개변수만 넣으면 구현할 수 있습니다. 그러나 POST Object 인터페이스만 지원하고 PUT Object 인터페이스는 지원하지 않으며, 요청자가 요청 생성 시 제한 매개변수를 수정할 수 있어 업로드 제한 범위 이외의 객체 크기를 업로드하기 때문에 통합 관리가 어렵다는 단점이 있습니다.

버킷 관리자는 임시 키 신청 시 다음 필드를 사용해 객체 크기를 제한할 수 있으며, COS 객체 크기를 cos:content_length로 고정하여 사용할 수 있습니다.

| 조건 필드                   | 의미         | 예시                                                         |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| numeric_greater_than       | < 값     | {"numeric_greater_than": {"cos:content_length": 1}}, 객체가 반드시 1byte보다 커야 함 |
| numeric_greater_than_equal | <= 값 | {"numeric_greater_than_equal": {"cos:content_length": 1}}, 객체가 반드시 1byte 이상이어야 함 |
| numeric_less_than          | > 값     | {"numeric_less_than": {"cos:content_length": 1}}, 객체가 반드시 10byte보다 작아야 함 |
| numeric_less_than_equal    | >= 값 | {"numeric_less_than_equal": {"cos:content_length": 1}}, 객체가 반드시 10byte 이하여야 함 |

전체 요청은 STS의 임시 액세스 자격 증명 획득 API 문서를 참조하십시오. 전체 정책(policy)은 다음과 같습니다.

```plaintext
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:PutObject",
                "cos:PostObject",
            ],
            "resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],

            "condition": {
                "numeric_greater_than_equal": {"cos:content_length": 1}
                , "numeric_less_than": {"cos:content_length": 10}
            }
        }
    ]
}
```

이 정책을 사용해 신청한 임시 인증은 PUT Object와 POST Object 인터페이스를 사용해 버킷 examplebucket-1250000000에 객체를 업로드할 수 있습니다. 단, 객체 크기 제한 범위는 [1, 10) byte가 됩니다.

>!이 정책은 현재 `cos:PutObject`, `cos:PostObject` 이 두 가지 action에만 적용되며, 기타 action(예: `cos:GetObject`)에는 적용되지 않습니다.

이러한 메커니즘을 통해 버킷 관리자 또는 '인증 센터'에서 통합적으로 STS에 임시 키를 신청할 수 있으며, 신청 시 객체 크기를 한정하고 다시 임시 키를 작업자 또는 서비스 모듈에 발급할 수 있습니다. 이 방식으로 사용자 요구에 맞는 객체를 업로드하고 요청 매개변수가 변조되지 않도록 방지합니다.

#### 응답

업로드하는 객체가 제한 크기에 부합하는 경우 업로드 요청에 성공하며 200 또는 204가 반환됩니다. 업로드하는 객체가 제한 범위를 초과하는 경우 403 실패를 반환합니다. 예시는 다음과 같습니다.

```plaintext
HTTP/1.1 403 Forbidden
Content-Type: application/xml
Content-Length: 298
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****
```

