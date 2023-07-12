## Overview
This API is used to enable or suspend versioning for a bucket.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketVersioning&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>



#### Notes

- If you have never enabled versioning for the bucket, GET Bucket versioning will not return a versioning state value.
2. Once enabled, versioning can only be suspended but cannot be disabled.
3. Set the versioning state value to Enabled or Suspended to enable or suspend versioning, respectively.
4. To set versioning for a bucket, you need to have the permission to write to the bucket.

## Request
#### Sample request

```shell
PUT /?versioning HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

```shell
<VersioningConfiguration>
  <Status></Status>
</VersioningConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --------------------------------------- | --------------------- | --------- | ------- |
| VersioningConfiguration | None | Describes the detailed information on versioning | Container |
| Status |    VersioningConfiguration  | Whether to enable versioning. Valid values: `Suspended`, `Enabled`  | Enum         |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).



## Samples
#### Request
```shell
PUT /?versioning HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Content-Type: application/xml
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9Sm****&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=versioning&q-header-list=host&q-signature=47ec2b80c73788ecd394d3b9ad90e120a32f****
Content-Length: 83

<VersioningConfiguration>
    <Status>Enabled</Status>
</VersioningConfiguration>
```

#### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Aug 2017 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****
```
