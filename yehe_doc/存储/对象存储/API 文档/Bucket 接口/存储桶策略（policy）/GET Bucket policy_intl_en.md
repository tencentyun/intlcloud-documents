## Description
This API (GET Bucket policy) is used to read the permission policy of a Bucket.

## Request

### Request example:

```shell
GET /?policy HTTP/1.1
Host:<bucketname-APPID>.cos.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

### Request headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

### Request body
The request body of this request is empty.

## Response

### Response headers

This API only uses common response headers. For more information on common request headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special response headers
This response does not use any special response header.

### Response body
The permission policy is returned in the response body.

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

### Error codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Example
### Request

```shell
GET /?policy HTTP/1.1
Host:examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484814099;32557710099&q-key-time=1484814099;32557710099&q-header-list=host&q-url-param-list=policy&q-signature=0523d7c6305b6676611c44798d2c48b659e6****
```

### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 237
Connection: keep-alive
Date: Thu Jan 19 16:21:46 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc3MWFfOWIxZjRlXzZmNDVf****

{
  "Statement": [
    {
      "Principal": {
        "qcs": [
          "qcs::cam::uin/909619481:uin/909619481"
        ]
      },
      "Effect": "allow",
      "Action": [
        "name/cos:GetBucket"
      ],
      "Resource": [
        "qcs::cos:ap-chengdu:uid/1252336075:aaa-1252336075/*"
      ]
    }
  ],
  "version": "2.0"
}
```

