>
> 1. This document is only for the COS XML version.
> 2. It does not apply to POST Object requests over HTTP.

## Overview

RESTful APIs support anonymous and signed HTTP requests, which help you use COS resources. For a signed request, the COS server will authenticate its initiator.

- Anonymous request: a HTTP request that does not contain any authentication information, and is sent using RESTful API.
- Signed request: a request that is signed with authentication information. The COS server authenticates the requester of the signed request and only executes the authenticated ones. Otherwise, it returns an error message and denies the request.

The COS server performs HMAC (Hash Message Authentication Code) authentication schema.

Besides, **pre-signed URLs** are provided in all language-specific [SDKs](https://intl.cloud.tencent.com/document/product/436/6474) so that you can easily access signed URLs and process requests. For more information, see **Pre-signed URL** in any language-specific SDK documentation.

## Use Cases

In use cases where COS objects need be published to the public, public read and private write is usually configured. It means that every one can read, but only accounts you specify with ACL policies can write to your objects. In this case, you can use ACL policies together with API request signature to authenticate access and control operation permission and period.

> The API request signature described in this document is already included in the SDK. **You need to follow the steps below only if you want to redevelop based on the initial APIs**.

In the above use cases, a variety of safety protections can be included for the API request:

1. **Requester authentication**: verifies the identity of the requester  by their unique ID and key.
2. **Transferred data anti-tampering**: signs and verifies the data to ensure its integrity during transfer.
3. **Signature anti-theft**: expires signatures to prevent them from being stolen for repeated use.

## Preparations

1. APPID, SecretId, and SecretKey: 
They can be obtained on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console.
2. Programming language:
Supported languages include without limitation Java, PHP, C#, C++, Node.js, and Python. You should determine the corresponding HMAC-SHA1, SHA1, and UrlEncode functions according to the actual language.
The HMAC-SHA1 and SHA1 functions input UTF-8 encoded string, and output lowercase hexadecimal string. The UrlEncode functions work based on UTF-8 encoding. The following printable special characters in the ASCII range should also be encoded:

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
| :      | 58     | 3A       |      |        |          |

## To Generate a Signature

### Step 1. Generate KeyTime
1. Get the Unix timestamp "StartTimestamp" for the current time, which is the total number of seconds starting from January 1, 1970, 00:00:00 UTC (January 1, 1970, 08:00:00 Beijing time).
2. Calculate the Unix timestamp "EndTimestamp" for the moment the signature expires based on the timestamp above and the expected valid duration of the signature.
3. Get KeyTime by combining the two timestamps above in the format `StartTimestamp;EndTimestamp`, such as `1557902800;1557910000`.

### Step 2. Generate SignKey
Calculate the message digest, which is a hexadecimal lowercase hash value, by using [HMAC-SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C), with [SecretKey](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) as the key and [KeyTime](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.9F.E6.88.90-keytime) as the message. The resulting message digest is SignKey, such as `eb2519b498b02ac213cb1f3d1a3d27a3b3c9bc5f`.

### Step 3. Generate UrlParamList and HttpParameters
1. Traverse the HTTP request parameters to generate a key-to-value Map and a KeyList:
 - Encode keys using [UrlEncode](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C), and convert them to lowercase.
 - Encode values using [UrlEncode](#. E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C). In parameters without value, the value is considered to be an empty string. For example, a request path `/?acl` is considered as `/?acl=`.
> The parameters in a HTTP request are what comes after `?` in the request path. For example, in the request path `/?versions&prefix=example-folder%2F&delimiter=%2F&max-keys=10`, the request parameters are `versions&prefix=example-folder%2F&delimiter=%2F&max-keys=10`.
2. Sort the KeyList in lexicographical order.
3. Splice all key-value pairs in the Map in the order of the KeyList in the format of `key1=value1&key2=value2&key3=value3`, which is the HttpParameters.
4. Splice all keys in the order of the KeyList in the format of `key1;key2;key3`, which is the UrlParamList.

#### Examples:
- Example 1:
Request path: `/?prefix=example-folder%2F&delimiter=%2F&max-keys=10`
UrlParamList：`delimiter;max-keys;prefix`
HttpParameters：`delimiter=%2F&max-keys=10&prefix=example-folder%2F`
>The request parameters in the request path are UrlEncoded too when the request is actually sent; therefore, be careful not to repeat the UrlEncoding.
- Example 2:
Request path: `/exampleobject?acl`
UrlParamList: `acl`
HttpParameters: `acl=`

### Step 4. Generate HeaderList and HttpHeaders
1. Traverse the HTTP request parameters, and generate the key-to-value mapping "Map" and the key list "KeyList", where keys are [UrlEncoded](#.E5.87.86.E5.A4.87.E5.B7.A5 .E4.BD.9C), and converted to lowercase.
2. Sort the KeyList in lexicographical order.
3. Splice all key-value pairs in the Map in the order of the KeyList in the format of `key1=value1&key2=value2&key3=value3`, which is the HttpHeaders.
4. Splice all keys in the order of the KeyList in the format of `key1;key2;key3`, which is the HeaderList.

#### Examples:
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
Generate the HttpString based on the HTTP method, HTTP request path, [HttpParameters](#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.94.9F.E6.88.90-urlparamlist-.E5.92.8C-httpparameters), and [HttpHeaders](#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E7.94.9F.E6.88.90-headerlist-.E5.92.8C-httpheaders) in the format of `HttpMethod\nUriPathname\nHttpParameters\nHttpHeaders\n`.

Notes:
- HttpMethod is converted to lower case, such as `get` or `put`.
- UriPathname is the request path, such as `/` or `/exampleobject`.
- `\n` is a line break. The two line breaks (if any) bookending an empty string should be retained, such as in `get\n/exampleobject\n\n\n`.


### Step 6. Generate StringToSign
Generate the StringToSign based on the [KeyTime](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.9F.E6.88.90-keytime), and [HttpString](#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E7.94.9F.E6.88.90-httpstring) in the format of `sha1\nKeyTime\nSHA1(HttpString)\n`.
Notes:
- `sha1` is a fixed string.
- `\n` is a line break.
-SHA1(HttpString) represents the message digest in hexadecimal lowercase of the [HttpString](#.E6.AD.A5.E9. AA.A45.EF.BC.9A.E7.94.9F.E6.88.90-httpstring) calculated using [SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C), such as `54ecfe22f59d3514fdc764b87a32d8133ea611e6`.

### Step 7. Generate Signature
Calculate the message digest by using [HMAC-SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) with [SignKey](#.E6.AD.A5.E9.AA.A42. EF.BC.9A.E7.94.9F.E6.88.90-signkey) as the key (a non-raw binary string) and [StringToSign](#.E6.AD.A5.E9.AA.A46.EF .BC.9A.E7.94.9F.E6.88.90-stringtosign) as the message. The resulting message digest is Signature, such as `01681b8c9d798a678e43b685a9f1bba0f6c0e012`.


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

>Line breaks in the example above are for easy understanding only and are not included in a real signature.

## Using a Signature
Signed HTTP requests initiated to COS via RESTful APIs can pass the signature in the following ways:
1. Pass through a standard HTTP Authorization header, such as `Authorization: q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753;1557996953&...&q-signature=...`
2. Pass as an HTTP request parameter (be sure to UrlEncode), such as `/exampleobject?q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753%3B1557996953&...&q-signature=...`

>In the example above, `...` is used to substitute the specific signature content.

## Sample Code

### Pseudocode
```plaintext
KeyTime = [Now];[Expires]
SignKey = HMAC-SHA1([SecretKey], KeyTime)
HttpString = [HttpMethod]\n[HttpURI]\n[HttpParameters]\n[HttpHeaders]\n
StringToSign = sha1\nKeyTime\nSHA1(HttpString)\n
Signature = HMAC-SHA1(SignKey, StringToSign)
```

### Sample message digest calculation

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

## Use Cases

### Preparations

Log in to the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in CAM Console to get your APPID, SecretId, and SecretKey. Below is an example:

| APPID      | SecretId                             | SecretKey                        |
| ---------- | ------------------------------------ | -------------------------------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz |

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
- **Signature** = `3b8851a11a569213c17ba8fa7dcf2abec6935172`

Here, (empty string) represents an empty string with a length of 0 and `\n` a line break.

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
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1557989151;1557996351&q-key-time=1557989151;1557996351&q-header-list=content-length;content-md5;content-type;date;host;x-cos-acl;x-cos-grant-read&q-url-param-list=&q-signature=3b8851a11a569213c17ba8fa7dcf2abec6935172

ObjectContent
```

### Downloading an object

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
- **Signature** = `01681b8c9d798a678e43b685a9f1bba0f6c0e012`

Here, `\n` represents a line break.

#### Signed request

```plaintext
GET /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91)?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D600 HTTP/1.1
Date: Thu, 16 May 2019 06:55:53 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1557989753;1557996953&q-key-time=1557989753;1557996953&q-header-list=date;host&q-url-param-list=response-cache-control;response-content-type&q-signature=01681b8c9d798a678e43b685a9f1bba0f6c0e012
```
