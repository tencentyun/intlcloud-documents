> !
> - This document is only for the COS XML version.
> - It does not apply to POST Object requests over HTTP.
> 


## Overview

You can use COS with RESTful APIs, which support anonymous and signed HTTP requests. The COS server will authenticate the requester of signed requests.

- Anonymous request: an HTTP request that does not contain any authentication information, and is sent using RESTful API.
- Signed request: an HTTP request that carries a signature. The COS server will authenticate requesters and only execute requests initiated by authenticated ones. If the authentication fails, COS will return an error message and deny the request.

COS authenticates requesters using a custom solution based on Hash Message Authentication Code (HMAC).


## Implementing Signature in SDK

Signatures are already implemented in COS SDKs, which means when you initiate requests or obtain signatures using an SDK, you can ignore the signature issue. To implement a signature by yourself or learn about the implementation of signatures in different programming languages, see the programming language−specific signature implementation file from the table below:

| SDK | Signature Implementation File |
| --- | --- |
| Android SDK | [COSXmlSigner.java](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudFoundation/foundation/src/main/java/com/tencent/qcloud/core/auth/COSXmlSigner.java) |
| C SDK | [cos_auth.c](https://github.com/tencentyun/cos-c-sdk-v5/blob/master/cos_c_sdk/cos_auth.c) |
| C++ SDK | [auth_tool.cpp](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/src/util/auth_tool.cpp) |
| .NET(C#) SDK | [IQCloudSigner.cs](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Auth/IQCloudSigner.cs) (class CosXmlSigner) |
| Go SDK | [auth.go](https://github.com/tencentyun/cos-go-sdk-v5/blob/master/auth.go) |
| iOS SDK | [QCloudAuthentationV5Creator.m](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/QCloudCore/Classes/Base/QCloudClientBase/Authentation/QCloudAuthentationV5Creator.m) |
| Java SDK | [COSSigner.java](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/auth/COSSigner.java) |
| JavaScript SDK | [util.js](https://github.com/tencentyun/cos-js-sdk-v5/blob/master/src/util.js) (getAuth) |
| Node.js SDK | [util.js](https://github.com/tencentyun/cos-nodejs-sdk-v5/blob/master/sdk/util.js) (getAuth) |
| PHP SDK | [Signature.php](https://github.com/tencentyun/cos-php-sdk-v5/blob/master/src/Signature.php) |
| Python SDK | [cos_auth.py](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/cos_auth.py) |
| Mini Program SDK | [util.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/src/util.js) (getAuth) |



## Generating a Signed URL



Currently, all COS [SDKs](https://intl.cloud.tencent.com/document/product/436/6474) can generate URLs that carry a signature valid for a period of time. The signature supports PUT and GET requests. Therefore, you can use the generated signed URL to upload/download objects directly without having to generate a signature separately.

- When generating a signed URL for uploads, you can also specify headers such as `Content-Type` and `Content-MD5` to limit the media type/content to upload. For the configurations of request headers related to uploads, please see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).
- When generating a signed URL for downloads, you can also specify `response-xxx` so that you can temporarily modify response headers upon download. For the configurations of request parameters related to downloads, please see [GET Object](https://intl.cloud.tencent.com/document/product/436/7753).

Find the pre-signed URL document corresponding to your SDK language from the table below:

>?
>- You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.

| SDK | Pre-Signed URL Document  |
| -------------- | ------------------------------------------------------------ |
| Android SDK    | [Generating a Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/37680) |
| C SDK          | [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31520) |
| C++ SDK        | [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31524) |
| .NET(C#) SDK   | [Generating a Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/38068) |
| Go SDK         | [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31528) |
| iOS SDK       | [Generating a Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/37690) |
| Java SDK       | [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31536) |
| JavaScript SDK | [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31540) |
| Node.js SDK    | [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/32455) |
| PHP SDK        | Pre-Signed URL|
| Python SDK     | [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31548) |
| Mini Program SDK     | [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31711) |



## Use Cases

If a COS object needs to be published to the public, you will usually need to set this object to public-read/private-write (everyone can read the object but only the ACL-specified account can write to it). After this, you can use the ACL policy together with the API request signature to authenticate requesters and control the permissions and validity period of operations.

>! The API request signature described in this document is already included in the SDK. **Perform the steps below only if you want to redevelop based on the native APIs**.
>

You can secure your API request as follows for the use case above.

1. **Authenticate requester**: verifies the identity of the requester by their unique ID and key.
2. **Prevent data tempering during transfer**: signs and verifies data to ensure its integrity during transfer.
3. **Prevent signature from being stolen**: sets validity period for the signature to prevent it from being stolen or used repeatedly.

## Preparations

1. Obtain APPID, SecretId, and SecretKey. 
They can be obtained on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page in the CAM console.
2. Determine the programming language.
Supported languages include but are not limited to Java, PHP, .NET, C++, Node.js, and Python. You can determine the HMAC-SHA1, SHA1, and UrlEncode functions according to the programming language selected.
The HMAC-SHA1 and SHA1 functions take UTF-8 encoded strings as input, and output lowercase hexadecimal strings, and UrlEncode is also based on UTF-8 encoding. Besides, the following printable special characters in the ASCII range should also be encoded:

| Character | Decimal | Hex | Character | Decimal | Hex |
| ------ | ------ | -------- | ---- | ------ | -------- |
| (Space) | 32     | 20       | ;    | 59     | 3B       |
| !      | 33     | 21       | <    | 60     | 3C       |
| "      | 34     | 22       | =    | 61     | 3D       |
| #      | 35     | 23       | >    | 62     | 3E       |
| $      | 36     | 24       | ?    | 63     | 3F       |
| %      | 37     | 25       | @    | 64     | 40       |
| &      | 38     | 26       | [    | 91     | 5B       |
| '      | 39     | 27       | \    | 92     | 5C       |
| (      | 40     | 28       | ]    | 93     | 5D       |
| )      | 41     | 29       | ^    | 94     | 5E       |
| *      | 42     | 2A       | \`    | 96     | 60       |
| +      | 43     | 2B       | {    | 123    | 7B       |
| ,      | 44     | 2C       |  \|    | 124    | 7C       |
| /      | 47     | 2F       | }    | 125    | 7D       |
| :      | 58     | 3A       |   None  |    None    |      None  |

## Generating a Signature

### Step 1. Generate KeyTime
1. Get the Unix `StartTimestamp` of the current time. It is the total number of seconds from January 1, 1970, 00:00:00 UTC (January 1, 1970, 08:00:00 Beijing time) till the current time.
2. Calculate the Unix `EndTimestamp` for the signature to expire according to `StartTimestamp` and the expected validity period of the signature.
3. Generate `KeyTime` by splicing the two timestamps above in `StartTimestamp;EndTimestamp` format (e.g., `1557902800;1557910000`).

### Step 2. Generate SignKey
Use [HMAC-SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) with [SecretKey](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) as the key and [KeyTime](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.9F.E6.88.90-keytime) as the message to calculate the message digest (i.e., `SignKey`), which is a hash value in lowercase hexadecimal format, such as `eb2519b498b02ac213cb1f3d1a3d27a3b3c9bc5f`.


### Step 3. Generate UrlParamList and HttpParameters
1. Traverse the HTTP request parameters to generate a key-to-value `Map` and a `KeyList`:
 - Encode keys using [UrlEncode](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C), and convert them to lowercase.
 - Encode values using [UrlEncode](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C). If a parameter does not take any value, its value is considered to be an empty string. For example, a request path `/?acl` is considered as `/?acl=`.
>? The parameters in an HTTP request are what comes after `?` in the request path. For example, in the request path `/?versions&prefix=example-folder%2F&delimiter=%2F&max-keys=10`, the request parameters are `versions&prefix=example-folder%2F&delimiter=%2F&max-keys=10`.
>
2. Sort the `KeyList` in lexicographical order.
3. Splice all key-value pairs in the `Map` according to the order in `KeyList` in the format of `key1=value1&key2=value2&key3=value3`, which is the `HttpParameters`.
4. Splice all keys in the order of the `KeyList`· in the format of `key1;key2;key3`, which is the `UrlParamList`.

#### Examples
- Example 1:
Request path: `/?prefix=example-folder%2F&delimiter=%2F&max-keys=10`
UrlParamList: `delimiter;max-keys;prefix`
HttpParameters: `delimiter=%2F&max-keys=10&prefix=example-folder%2F`
>! When the request is sent, the request parameters in the request path will also be URL-encoded. Therefore, do not repeat the URL encoding operation.
>
- Example 2:
Request path: `/exampleobject?acl`
UrlParamList: `acl`
HttpParameters: `acl=`

### Step 4. Generate HeaderList and HttpHeaders
1. Traverse the HTTP request parameters, and generate the key-to-value mapping `Map` and the key list `KeyList`, where keys are [URL-encoded](#.E5.87.86.E5.A4.87.E5.B7.A5 .E4.BD.9C) and converted to lowercase, and values are [URL-encoded](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C).
2. Sort the `KeyList` in lexicographical order.
3. Splice all key-value pairs in the `Map` according to the order in `KeyList` in the format of `key1=value1&key2=value2&key3=value3`, which is the `HttpHeaders`.
4. Splice all keys according to the order in `KeyList` in the format of `key1;key2;key3`, which is the `HeaderList`.

#### Examples
Request headers:
```plaintext
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Date: Thu, 16 May 2019 03:15:06 GMT
x-cos-acl: private
x-cos-grant-read: uin="100000000011"
```
Calculations:
- HeaderList = `date;host;x-cos-acl;x-cos-grant-read`
- HttpHeaders = `date=Thu%2C%2016%20May%202019%2003%3A15%3A06%20GMT&host=examplebucket-1250000000.cos.ap-shanghai.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22`

### Step 5. Generate HttpString
Generate `HttpString` based on `HttpMethod`, `UriPathname`, [HttpParameters](#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.94.9F.E6.88.90-urlparamlist-.E5.92.8C-httpparameters), and [HttpHeaders](#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E7.94.9F.E6.88.90-headerlist-.E5.92.8C-httpheaders) in the format of `HttpMethod\nUriPathname\nHttpParameters\nHttpHeaders\n`.

Where:
- `HttpMethod` is converted to lowercase, such as `get` or `put`.
- `UriPathname` is the request path, such as `/` or `/exampleobject`.
- `\n` is a line break. If there is an empty string, the line breaks before and after it should be retained, for example, `get\n/exampleobject\n\n\n`.


### Step 6. Generate StringToSign
Generate `StringToSign` based on [KeyTime](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.9F.E6.88.90-keytime) and [HttpString](#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E7.94.9F.E6.88.90-httpstring) in the format of `sha1\nKeyTime\nSHA1(HttpString)\n`.
Where:
- `sha1` is a fixed string.
- `\n` is a line break.
- SHA1(HttpString) is the message digest (in lowercase hexadecimal format, such as `54ecfe22f59d3514fdc764b87a32d8133ea611e6`) calculated with [SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) and [HttpString](#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E7.94.9F.E6.88.90-httpstring).

### Step 7. Generate Signature
Use [HMAC-SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) with [SignKey](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E7.94.9F.E6.88.90-signkey) (a string rather than the original binary) as the key and [StringToSign](#.E6.AD.A5.E9.AA.A46.EF.BC.9A.E7.94.9F.E6.88.90-stringtosign) as the message to calculate the message digest, which is `Signature`, for example, `01681b8c9d798a678e43b685a9f1bba0f6c01234`.

### Step 8. Generate an actual signature
Generate the actual signature based on [SecretId](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C), [KeyTime](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.9F.E6.88.90-keytime), [HeaderList](#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E7.94.9F.E6.88.90-headerlist-.E5.92.8C-httpheaders), [UrlParamList](#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.94.9F.E6.88.90-urlparamlist-.E5.92.8C-httpparameters), and [Signature](#.E6.AD.A5.E9.AA.A47.EF.BC.9A.E7.94.9F.E6.88.90-signature) in the following format:
```plaintext
q-sign-algorithm=sha1
&q-ak=SecretId
&q-sign-time=KeyTime
&q-key-time=KeyTime
&q-header-list=HeaderList
&q-url-param-list=UrlParamList
&q-signature=Signature
```

>! Line breaks in the sample above are for readability only and are not included in the actual signature.
>

## Using a Signature
Signed HTTP requests sent to COS via RESTful APIs can pass the signature in the following ways:
1. Pass through a standard HTTP `Authorization` header, such as `Authorization: q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753;1557996953&...&q-signature=...`
2. Pass as an HTTP request parameter (be sure to URL-encode), such as `/exampleobject?q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753%3B1557996953&...&q-signature=...`

>? In the example above, `...` are the signatures.
>

## Using a Temporary Credential (Key)
If a temporary credential is used for signature calculation, the `x-cos-security-token` field should be specified when you send the request. The way to specify this field varies depending on how the signature is passed in.
1. If the signature is passed in using the standard HTTP `Authorization` header, specify `x-cos-security-token` as a request header as follows:
```plaintext
Authorization: q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753;1557996953&...&q-signature=...
x-cos-security-token: ...
```
2. If the signature is passed in as an HTTP request parameter, specify `x-cos-security-token` as a request parameter as follows:
```plaintext
/exampleobject?q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753%3B1557996953&...&q-signature=...&x-cos-security-token=...
```

>? In the samples above, `...` is the signature and access token.
>

## Sample Code

### Pseudocode
```plaintext
KeyTime = [Now];[Expires]
SignKey = HMAC-SHA1([SecretKey], KeyTime)
HttpString = [HttpMethod]\n[HttpURI]\n[HttpParameters]\n[HttpHeaders]\n
StringToSign = sha1\nKeyTime\nSHA1(HttpString)\n
Signature = HMAC-SHA1(SignKey, StringToSign)
```

### Sample of the message digest algorithm

The samples below illustrate how to call HMAC-SHA1 in different languages:

#### PHP

```php
$sha1HttpString = sha1('ExampleHttpString');

$signKey = hash_hmac('sha1', 'ExampleKeyTime', 'YourSecretKey');
```

#### Java

```java
import org.apache.commons.codec.digest.DigestUtils;
import org.apache.commons.codec.digest.HmacUtils;

String sha1HttpString = DigestUtils.sha1Hex("ExampleHttpString");

String signKey = HmacUtils.hmacSha1Hex("YourSecretKey", "ExampleKeyTime");
```

#### Python

```python
import hmac
import hashlib

sha1_http_string = hashlib.sha1('ExampleHttpString'.encode('utf-8')).hexdigest()

sign_key = hmac.new('YourSecretKey'.encode('utf-8'), 'ExampleKeyTime'.encode('utf-8'), hashlib.sha1).hexdigest()
```

#### Node.js

```node
var crypto = require('crypto');

var sha1HttpString = crypto.createHash('sha1').update('ExampleHttpString').digest('hex');
var signKey = crypto.createHmac('sha1', 'YourSecretKey').update('ExampleKeyTime').digest('hex');
```

#### Go

```go
import (
	"crypto/hmac"
	"crypto/sha1"
)

h := sha1.New()
h.Write([]byte("ExampleHttpString"))
sha1HttpString := h.Sum(nil)

var hashFunc = sha1.New
h = hmac.New(hashFunc, []byte("YourSecretKey"))
h.Write([]byte("ExampleKeyTime"))
signKey := h.Sum(nil)
```

## Examples

### Preparations

Log in to the CAM console and go to the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page to obtain your `APPID`, `SecretId`, and `SecretKey`. Below is an example:

| APPID      | SecretId                             | SecretKey                        |
| ---------- | ------------------------------------ | -------------------------------- |
| 1250000000 | AKXXXXXXXXXXXXXXXXXXX | BQXXXXXXXXXXXXXXXXXXXX |

### Uploading an object

#### Original request

```plaintext
PUT /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91) HTTP/1.1
Date: Thu, 16 May 2019 06:45:51 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Content-Type: text/plain
Content-Length: 13
Content-MD5: mQ/fVh815F3k6TAUm8m0eg==
x-cos-acl: private
x-cos-grant-read: uin="100000000011"

ObjectContent
```

#### Intermediate variables

- **KeyTime** = `1557989151;1557996351`
- **SignKey** = `eb2519b498b02ac213cb1f3d1a3d27a3b3c9bc5f`
- **UrlParamList** = `(empty string)`
- **HttpParameters** = `(empty string)`
- **HeaderList** = `content-length;content-md5;content-type;date;host;x-cos-acl;x-cos-grant-read`
- **HttpHeaders** = `content-length=13&content-md5=mQ%2FfVh815F3k6TAUm8m0eg%3D%3D&content-type=text%2Fplain&date=Thu%2C%2016%20May%202019%2006%3A45%3A51%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22`
- **HttpString** = `put\n/exampleobject(tencentcloud)\n\ncontent-length=13&content-md5=mQ%2FfVh815F3k6TAUm8m0eg%3D%3D&content-type=text%2Fplain&date=Thu%2C%2016%20May%202019%2006%3A45%3A51%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22\n`
- **StringToSign** = `sha1\n1557989151;1557996351\n8b2751e77f43a0995d6e9eb9477f4b685cca4172\n`
- **Signature** = `3b8851a11a569213c17ba8fa7dcf2abec6931234`

Here, (empty string) is a zero-byte string and `\n` is a line break.

#### Signed request

```plaintext
PUT /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91) HTTP/1.1
Date: Thu, 16 May 2019 06:45:51 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Content-Type: text/plain
Content-Length: 13
Content-MD5: mQ/fVh815F3k6TAUm8m0eg==
x-cos-acl: private
x-cos-grant-read: uin="100000000011"
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn****&q-sign-time=1557989151;1557996351&q-key-time=1557989151;1557996351&q-header-list=content-length;content-md5;content-type;date;host;x-cos-acl;x-cos-grant-read&q-url-param-list=&q-signature=3b8851a11a569213c17ba8fa7dcf2abec693****

ObjectContent
```


### Download an object

#### Original request

```plaintext
GET /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91)?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D600 HTTP/1.1
Date: Thu, 16 May 2019 06:55:53 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### Intermediate variables

- **KeyTime** = `1557989753;1557996953`
- **SignKey** = `937914bf490e9e8c189836aad2052e4feeb35eaf`
- **UrlParamList** = `response-cache-control;response-content-type`
- **HttpParameters** = `response-cache-control=max-age%3D600&response-content-type=application%2Foctet-stream`
- **HeaderList** = `date;host`
- **HttpHeaders** = `date=Thu%2C%2016%20May%202019%2006%3A55%3A53%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com`
- **HttpString** = `get\n/exampleobject(tencentcloud)\nresponse-cache-control=max-age%3D600&response-content-type=application%2Foctet-stream\ndate=Thu%2C%2016%20May%202019%2006%3A55%3A53%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com\n`
- **StringToSign** = `sha1\n1557989753;1557996953\n54ecfe22f59d3514fdc764b87a32d8133ea611e6\n`
- **Signature** = `01681b8c9d798a678e43b685a9f1bba0f6c01234`

Here, `\n` is a line break.

#### Signed request

```plaintext
GET /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91)?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D600 HTTP/1.1
Date: Thu, 16 May 2019 06:55:53 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn****&q-sign-time=1557989753;1557996953&q-key-time=1557989753;1557996953&q-header-list=date;host&q-url-param-list=response-cache-control;response-content-type&q-signature=01681b8c9d798a678e43b685a9f1bba0f6c0****
```

