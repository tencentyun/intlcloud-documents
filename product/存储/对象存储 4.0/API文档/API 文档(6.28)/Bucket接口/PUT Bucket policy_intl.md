## Description
This API (PUT Bucket policy) is used to write a permission policy for a Bucket. The policy passed in will overwrite the existing permission policy.

## Request

### Request example

```shell
PUT /?policy HTTP/1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
Content-Type:application/json
Content-MD5:MD5
Authorization: Auth String
```

> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).


### Request headers

#### Common headers

Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728 "公共请求头部").

#### Request parameters
No special request parameter is needed.

### Request body

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

## Response

### Response headers
#### Common response headers

This response uses common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special response headers

No special response header is used for this request operation.

### Response body
The response body is empty.

### Error codes

No special error code is returned. For common error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example
### Request

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

### Response

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu Jan 19 16:19:22 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc2OGFfNDUyMDRlXzc3NTlfZTc4
```

