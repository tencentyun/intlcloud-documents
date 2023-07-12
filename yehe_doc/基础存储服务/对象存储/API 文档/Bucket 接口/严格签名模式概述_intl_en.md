
## Overview

COS allows you to configure the strict signature mode for your buckets. In this mode, you can specify the request headers and parameters that must be signed for certain requests. This prevents malicious users from manipulating your buckets by hijacking normal user requests and stealing the COS signature.

>!
>The strict signature mode takes effect only for signed requests but not anonymous requests.

## Use Cases

This feature can be used to prevent malicious users from manipulating your buckets by stealing the signature in content delivery and UGC scenarios where the signature may be disclosed to a large number of users.

>?The strict signature mode is used to prevent unauthorized access via signature.



## Unauthorized Access via Signature

COS allows you to select the request headers (Header) and parameters (Param) to be signed, which correspond to `q-header-list=HeaderList` and `q-url-param-list=UrlParamList` in the signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).


```plaintext
q-sign-algorithm=sha1
&q-ak=SecretId
&q-sign-time=KeyTime
&q-key-time=KeyTime
&q-header-list=HeaderList
&q-url-param-list=UrlParamList
&q-signature=Signature
```


COS will check whether signed headers and parameters are the same as those in the actual request during signature verification. However, COS cannot verify unsigned headers and parameters against the signature; therefore, the signature may be stolen and used for other requests by malicious users.


### Bad example: `Host` is not signed in the signature

If the request header `Host` is not signed in the signature, unauthorized cross-bucket access may occur.

For example, both buckets A and B contain the object `RAID5.jpg`, and a sub-account has the `GET Object` permission for both buckets. When a user initiates a request to bucket A to download `RAID5.jpg` with the sub-account, the sub-account private key is used to generate two signatures: `autha` and `autha_nohost`, where `Host` is signed and not signed respectively.

The user tries initiating a request to bucket A with the signature `autha` and bucket B with the signature `autha_nohost` to download `RAID5.jpg`. As `Host` is not signed in the signature `autha_nohost`, `Host` cannot be verified during signature verification, and the download request can be successfully initiated to bucket B with `autha_nohost`. As a result, requests that are intended to manipulate bucket A can actually be used to manipulate bucket B, which is insecure.

| No. | Request | Signature | Response | Request Result |
| ---- | ------------------------- | ------------ | ---- | ------------------------------------------------------------ |
| 1    | Gets `RAID5.jpg` from bucket A. | `autha`        | 200  | Success                                                     |
| 2    | Gets `RAID5.jpg` from bucket A. | autha_nohead | 200  | Success                                                     |
| 3    | Gets `RAID5.jpg` from bucket B. | autha        | 403  | As `Host` is signed in `autha` and the `Host` value in the signature is different from that in the actual request, the request fails. |
| 4    | Gets `RAID5.jpg` from bucket B. | autha_nohead | 200  | As `Host` is not signed in `autha_nohost`, `Host` cannot be verified during signature verification, causing unauthorized cross-bucket access via the signature. |

To avoid unauthorized cross-bucket access, you can sign the `Host` header in the signature during signature generation to prevent it from being stolen. In addition, you can set the strict signature mode during signature verification to specify that the signature must contain the `Host` header in signed requests initiated to bucket B; otherwise, requests will be denied. This prevents bucket B from being requested with a stolen signature.

### Bad example 2: `versionid` is not signed in the signature

If the request parameter `versionid` is not signed in the signature, objects may be deleted permanently without authorization. For example, a user generates a signature to delete `/exampleobject`. As versioning is enabled in the bucket where the object is stored, the request will create a delete marker, and the object won't be actually deleted. However, malicious users can use the signature of the request to forge a request `DELETE /exampleobject?versionId=xxx` to permanently delete the historical versions of the object, resulting in data loss.

To avoid this, you need to use the strict signature mode to specify that if an object deletion request initiated to a bucket contains the request parameter `versionid`, then the signature must also contain `versionid`; otherwise, the request will be denied.

## Strict Signature Mode

To avoid unauthorized access via signature, you can take the following measures:

- **Protection during signature generation**: When you generate a signature, you must sign the key request headers and parameters used in the request in the signature, including `Host` and all request parameters. If you use COS SDK, `Host` and all request parameters are automatically signed in signatures generated by the SDK, and you can also pass in other request headers to be signed in the signature as needed.
- **Protection during signature verification**: You can set the strict signature mode for a bucket to specify the headers and parameters that must be signed in the signature for certain requests. When COS receives such a request, if the request contains a specified header or parameter but the signature doesn't, the request will be denied.

In the above cases where the `Host` is missing in the signature, both signing `Host` during signature generation and using the strict signature mode can avoid unauthorized cross-bucket access. However, for the aforementioned unauthorized access due to the lack of `versionid` in the signature, there are no effective protection methods during signature generation; instead, you can only use the strict signature mode.

### Configurable elements in strict signature mode

The strict signature mode allows you to specify the headers and parameters that must be signed in the signature for certain requests and takes effect only for **signed requests**. You can configure up to 10 strict signature mode rules for each bucket, and a rule contains three basic elements: applicable action list, request header list, and request parameter list.

- Applicable action list: It indicates the range of requests for which the strict signature mode rule takes effect. You can specify multiple actions (i.e., operations), which must be written in the same way as the actions in bucket or user policies, such as `PutObject` and `GetObject`.
- Request header list: It indicates the request headers that must be signed in the signature for requests for which the rule takes effect. You can specify multiple request headers.
- Request parameter list: It indicates the request parameters that must be signed in the signature for requests for which the rule takes effect. You can specify multiple request parameters.

#### Applicable action list

It indicates the range of requests for which the strict signature mode rule takes effect. You can specify multiple actions (i.e., operations), which must be written in the same way as the actions in bucket or user policies, such as `PutObject` and `GetObject`.

- You can use a wildcard; for example, you can use `Get*` to represent all GET requests, `Put*` all PUT requests, `Post*` all POST requests, `Delete*` all DELETE requests, and `*` all requests.
- You can add up to 200 actions in a rule.
- Unsupported requests: `PostObject`, batch operation, and `GetService` APIs. If a wildcard is used, such requests will be skipped automatically. If you enter such requests directly in a rule, an error will occur during rule configuration.

#### Supported request headers

The strict signature mode only supports the following COS request headers but not `User-Agent`, `Origin`, or custom request headers:

- **Common request headers**: `Host`, `Content-Length`, `Content-Type`, `Content-MD5`, and `Range`.
- **ACL request headers**: `x-cos-acl`, `x-cos-grant-read`, `x-cos-grant-write`, `x-cos-grant-read-acp`, `x-cos-grant-write-acp`, and `x-cos-grant-full-control`.
- **x-cos-\***: If the rule contains `x-cos-*`, all request headers starting with `x-cos-` must be signed.
- You can add up to 20 headers in a rule.

#### Supported request parameters

The strict signature mode supports the following request parameters. We recommend you directly use `all` to strictly specify that all used request parameters be signed in the signature.

- **COS request parameters**: `versionId`, `response-content-type`, `acl`, etc.
- **Custom request parameters**: A custom parameter can contain up to 255 letters, digits, hyphens, underscores, and dots.
- **All request parameters**: If `all` is entered, all request parameters in a request will be verified in strict signature mode by default. In other words, all request parameters in the request must be signed in the signature; otherwise, the request will be denied.
- You can add up to 20 parameters in a rule.

### Verification process in strict signature mode

After COS receives a request:

- If the request contains a header or parameter specified in a strict signature mode rule, the system will check whether the signature also contains the header or parameter.
  - If the specified header or parameter is missing in the signature, the request will be denied, and the `403 Forbbiden` error will be reported.
  - If the signature also contains the specified header or parameter, the system will proceed to the subsequent signature verification process.
- If the request doesn't contain the specified header or parameter, the system won't check whether the signature contains the header or parameter and will directly proceed to the subsequent signature verification process.

| Use Case | Code | Message |
| ------------------------- | ------------ | --------------------------------------------------- |
| A specified header is not signed in the signature | AccessDenied | Strict signature missing header that must be signed |
| A specified parameter is not signed in the signature  | AccessDenied | Strict signature missing param that must be signed  |

The process is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6a18edc7ea695751394b431933114a7c.png)

### Samples of using the strict signature mode

#### Sample 1

To specify that `Host` and request parameters must be signed for all requests, set the following strict signature mode rule:

```plaintext
<StrictSignatureConfiguration>
    <Rule>
        <ID>rule1</ID>
        <actionlist>
            <action>*</action>
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

#### Sample 2

To specify that `versionid` must be signed in the signature if it is in an object deletion request, set the following strict signature mode rule:

```plaintext
<StrictSignatureConfiguration>
    <Rule>
        <ID>rule2</ID>
        <actionlist>
            <action>DeleteObject</action>
        </actionlist>
        <paramlist>
            <param>versionid</param>
        </paramlist>
    </Rule>
</StrictSignatureConfiguration>

```

## How to Use



### Using the REST API


- [PUT Bucket StrictSignature](https://www.tencentcloud.com/document/product/436/53889)
- [GET Bucket StrictSignature](https://www.tencentcloud.com/document/product/436/53890)
- [DELETE Bucket StrictSignature](https://www.tencentcloud.com/document/product/436/53891)


