## Overview
This API is used to write a permission policy for a bucket. The policy passed in this API will overwrite the existing one (if any) in the bucket.


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketPolicy&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


## Request

#### Sample request

```shell
PUT /?policy HTTP/1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
Content-Type:application/json
Content-MD5:MD5
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body
In the following example, the root account (100000000001) grants permission to its sub-account (100000000011) to query the list of objects in the `examplebucket-1250000000` bucket. For more information about the elements used in access policy settings, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023). For the policy-granting example, please see [Working with COS API Access Policies](https://intl.cloud.tencent.com/document/product/436/30580).

```shell
{
  "Statement": [
    {
      "Principal": {
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000011"
        ]
      },
      "Effect": "allow",
      "Action": [
        "name/cos:GetBucket"
      ],
      "Resource": [
        "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body
The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example
#### Request

```shell
PUT /?policy HTTP/1.1
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484813288;32557709288&q-key-time=1484813288;32557709288&q-header-list=host&q-url-param-list=policy&q-signature=05f7fc936369f910a94a0c815e1f1752f034****
Content-Type: application/json
Content-Length: 233

{
  "Statement": [
    {
      "Principal": {
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000001"
        ]
      },
      "Effect": "allow",
      "Action": [
        "name/cos:GetBucket"
      ],
      "Resource": [
        "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```

#### Response

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu Jan 19 16:19:22 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc2OGFfNDUyMDRlXzc3NTlf****
```
