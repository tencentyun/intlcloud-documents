## 기능 설명
PUT Bucket policy 요청은 버킷에 권한 정책을 입력할 수 있습니다. 버킷에 권한 정책이 이미 존재할 경우, 해당 요청 업로드 정책은 기존 권한 정책을 덮어쓰기합니다.

## 요청

### 요청 예제

```shell
PUT /?policy HTTP/1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
Content-Type:application/json
Content-MD5:MD5
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.).


### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728 "공용 요청 헤더") 섹션을 참조하십시오.

#### 요청 매개변수
특별한 요청 매개변수가 없습니다.

### 요청체

```shell
{
    "Statement": [
        {
            "Principal": {
                "qcs": [
                    "qcs::cam::uin/${owner_uin}:uin/${sub_uin}"
                ]
            },
            "Effect": "${effect}",
            "Action": [
                "name/cos:${action}"
            ],
            "Resource": [
                "qcs::cos:${region}:uid/${appid}:${bucket}/*"
            ]
        }
    ],
    "version": "2.0"
}
```

## 응답

### 응답 헤더
#### 공통 응답 헤더

해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.

#### 고유의 응답 헤더

해당 요청 작업은 특별한 응답 헤더 정보가 없습니다.

### 응답 본문
해당 요청 응답 본문은 비어 있습니다.

### 오류 코드

반환한 특별 오류 코드가 없습니다. 일반적인 오류 코드는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

## 실제 사례
### 요청

```shell
PUT /?policy HTTP/1.1
Host:examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484813288;32557709288&q-key-time=1484813288;32557709288&q-header-list=host&q-url-param-list=policy&q-signature=05f7fc936369f910a94a0c815e1f1752f034d47a
Content-Type: application/json
Content-Length: 233

{
  "Statement": [
    {
      "Principal": {
        "qcs": [
          "qcs::cam::uin/1250000000:uin/1250000000"
        ]
      },
      "Effect": "allow",
      "Action": [
        "name/cos:GetBucket"
      ],
      "Resource": [
        "qcs::cos:ap-chengdu:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}

```

### 응답

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu Jan 19 16:19:22 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc2OGFfNDUyMDRlXzc3NTlfZTc4
```
