
## Overview

This API (`PUT Bucket StrictSignature`) is used to configure the strict signature mode for a bucket. In this mode, you can specify the request headers and parameters that must be signed for certain requests.

> !
>
> - COS allows you to create up to 10 strict signature mode rules for each bucket.
> - The strict signature mode takes effect only for signed requests but not anonymous requests.
> - When calling this API, make sure that you have the permission to manipulate the bucket's strict signature mode. The bucket owner has this permission by default. If you don't have it, request it from the owner. For the authorization process, see [COS Authorization and Identity Verification Process](https://intl.cloud.tencent.com/document/product/436/45228).


## Request

#### Sample request

```shell
PUT /?strict-signature HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-MD5: MD5
```

>? 
>
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
>- Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

You can use the XML language to set specific configuration information for the strict signature mode in the request body, including the rule name, applicable actions, and request headers and parameters that must be signed.


```shell
<StrictSignatureConfiguration>
    <Rule>
        <ID></ID>
        <actionlist>
            <action></action>
            <action></action>
        </actionlist>
        <headerlist>
            <header></header>
            <header></header>
        </headerlist>
        <paramlist>
            <param></param>
            <param></param>
        </paramlist>
    </Rule>
</StrictSignatureConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ---------------------------- | -------------------------------------------- | ------------------------------------------------------------ | --------- | -------- |
| StrictSignatureConfiguration | None | Strict signature mode configuration | Container | Yes |
| Rule | StrictSignatureConfiguration | Rule description. Up to 10 rules are supported. | Container | Yes |
| ID | StrictSignatureConfiguration.Rule | Unique rule ID, which can contain up to 255 letters, digits, hyphens, underscores, and dots. | String | Yes |
| actionlist | StrictSignatureConfiguration.Rule | Action list, which can contain up to 200 actions. | Container | No |
| action | StrictSignatureConfiguration.Rule.actionlist | The action specified by the rule, which should be named in the same way as authorized actions in CAM and supports wildcards, such as `Put*`. | String | No |
| headerlist | StrictSignatureConfiguration.Rule | The list of up to 20 headers that must be signed as required by the rule. | Container | No |
| headerlist | StrictSignatureConfiguration.Rule.headerlist | Request headers that must be signed. For specific request headers, see [Supported request headers](https://www.tencentcloud.com/document/product/436/53892). | String | No |
| paramlist | StrictSignatureConfiguration.Rule | The list of up to 20 request parameters that must be signed as required by the rule. | Container | No |
| param | StrictSignatureConfiguration.Rule.paramlist | Request parameters that must be signed. For specific request parameters, see [Supported request parameters](https://www.tencentcloud.com/document/product/436/53892). | String | No |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Sample 1: Setting the strict signature mode for requests related to modifying ACL

#### Request

This example adds a strict signature mode rule named `limit_acl` to the `examplebucket-1250000000` bucket.

- This rule takes effect for `PutObjectACL` and `PutBucketACL` requests.
- It specifies that the request header `Host` and the request parameter `acl` must be signed in the signature, so as to prevent malicious users from stealing the signatures of other buckets or requests to modify buckets and object ACLs.

```shell
PUT /?strict-signature HTTP/1.1
Date: Date
Authorization: Auth String
Content-MD5: Content-MD5
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1024

<StrictSignatureConfiguration>
    <Rule>
        <ID>limit_acl</ID>
        <actionlist>
            <action>PutObjectACL</action>
            <action>PutBucketACL</action>
        </actionlist>
        <headerlist>
            <header>Host</header>
        </headerlist>
        <paramlist>
            <param>acl</param>
        </paramlist>
    </Rule>
</StrictSignatureConfiguration>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Date
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF8****
```

#### Sample 2: Specifying that `Host` and request parameters must be signed for `Put` requests

#### Request

This example adds a strict signature mode rule named `test` to the `examplebucket-1250000000` bucket.

- This rule takes effect for all `Put` requests, i.e., `Put*`.
- It specifies that the request header `Host` and all request parameters must be signed in the signature, so as to prevent malicious users from stealing the signatures of other buckets or requests.

```shell
PUT /?strict-signature HTTP/1.1
Date: Date
Authorization: Auth String
Content-MD5: Content-MD5
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1024

<StrictSignatureConfiguration>
    <Rule>
        <ID>test</ID>
        <actionlist>
            <action>Put*</action>
        </actionlist>
        <headerlist>
            <header>Host</header>
        </headerlist>
        <paramlist>
            <param>all</param>
        </paramlist>
    </Rule>
</StrictSignatureConfiguration>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Date
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF8****
```

