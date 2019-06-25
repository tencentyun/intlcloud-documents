>
> 1. This document is only for the COS XML edition.
> 2. It is not applicable for HTTP requests for posting objects.

An anonymous or signed HTTP request can be initiated to COS through RESTful APIs. For the signed request, the COS server will authenticate the request initiator.

- Anonymous request: The HTTP request does not carry any identity or authentication information and is manipulated through RESTful APIs.
- Signed request: The HTTP request is signed. After receiving the request, the COS server performs authentication. If authentication succeeds, the request can be accepted and executed; otherwise, an error message is returned and the request is discarded.

COS performs authentication based on a custom scheme of Hash-based Message Authentication Code (HMAC).

## Signature Use Cases

During the use of COS, objects for data that needs to be released externally can usually be set to public read and private write, i.e., they can be viewed by everyone and written only by accounts specified by an ACL policy. The ACL policy can be combined with the API request signature to authenticate access requests and control the permissions and validity periods of operations.

> The API request signature described in this document is already included in the SDK. **You need to follow the steps below only if you want to redevelop based on the original APIs**.

In this case, multiple layers of security protection can be applied to API requests:

1. **Requester authentication**. A requester's identity is verified using the unique ID and key.
2. **Data tampering prevention during transmission**. Data is signed and verified to ensure the integrity of the transmitted content.
3. **Signature theft prevention**. A signature can be protected from theft and reuse by setting its validity period.

## Preparations

1. APPID, SecretId, and SecretKey:
They can be obtained on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console.
2. Programming language:
Supported languages include without limitation Java, PHP, C#, C++, Node.js, and Python. You should determine the corresponding HMAC-SHA1, SHA1, and UrlEncode functions according to the actual language.
The HMAC-SHA1 and SHA1 functions take UTF-8 encoded strings as input and hexadecimal lowercase strings as output. UrlEncode is based on UTF-8 encoding. For printable characters in the ASCII range, the following special symbols should also be encoded:

| Character | Decimal | Hex | Character | Decimal | Hex |
| ------ | ------ | -------- | ---- | ------ | -------- |
| (space) | 32     | 20       | ;    | 59     | 3B       |
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

## Signing Process

### Generating KeyTime
1. Get the Unix timestamp "StartTimestamp" corresponding to the current time, which is the total number of seconds starting from January 1, 1970, 00:00:00 UTC (January 1, 1970, 08:00:00 Beijing time).
2. Calculate the Unix timestamp "EndTimestamp" corresponding to the signature expiry time based on the timestamp above and the expected validity period of the signature.
3. Splice the signature validity period in the format of `StartTimestamp;EndTimestamp`, which is the KeyTime.
**Example:** `1557902800;1557910000`

### Generating SignKey
Calculate the message digest (hash value) using [HMAC-SHA1](#Preparations) with [SecretKey](#Preparations) as the key and [KeyTime](#Generating KeyTime) as the message, which is SignKey.

**Example:** `36bcd76dbb8c9f066472fec403df8a34cab34c77`

### Generating UrlParamList and HttpParameters
1. Traverse the HTTP request parameters, generate the key-to-value mapping "Map" and the key list "KeyList", where key is converted to lowercase and value is [UrlEncoded](#Preparations).
In parameters without value, the value is considered to be an empty string. For example, if the request path is `/?acl`, it is considered to be `/?acl=`.
2. Sort the KeyList in lexicographical order.
3. [UrlEncode](#Preparations) the keys in the Map and KeyList and convert them to lowercase too.
4. Splice all key-value pairs in the Map in the order of the KeyList in the format of `key1=value1&key2=value2&key3=value3`, which is the HttpParameters.
5. Splice all items in the KeyList in the order of the KeyList in the format of `key1;key2;key3`, which is the UrlParamList.

**Example:**
- Example 1:
Request path: `/?prefix=example-folder%2F&delimiter=%2F&max-keys=10`
UrlParamList: `delimiter;max-keys;prefix`
HttpParameters: `delimiter=%2F&max-keys=10&prefix=example-folder%2F`
> The request parameters in the request path are UrlEncoded too when the request is actually sent; therefore, be careful not to repeat the UrlEncoding.
- Example 2:
Request path: `/exampleobject?acl`
UrlParamList: `acl`
HttpParameters: `acl=`

### Generating HeaderList and HttpHeaders
Generate the HeaderList and HttpHeaders in the same way as described in [Generating UrlParamList and HttpParameters](#Generating UrlParamList and HttpParameters), where the HTTP request parameters used for generation need to be replaced with HTTP request headers. The generated HttpParameters is the HttpHeaders, while the generated UrlParamList is the HeaderList.

**Example:**
Request header:
```shell
Date: Thu, 16 May 2019 03:15:06 GMT
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
x-cos-acl: private
x-cos-grant-read: uin="100000000011"
```
Calculate the HeaderList as `date;host;x-cos-acl;x-cos-grant-read` and HttpHeaders as `date=Thu%2C%2016%20May%202019%2003%3A15%3A06%20GMT&host=examplebucket-1250000000.cos.ap-shanghai.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22`.

### Generating HttpString
Generate the HttpString based on the HTTP method, HTTP request path, [HttpParameters](#Generating UrlParamList and HttpParameters), and [HttpHeaders](#Generating HeaderList and HttpHeaders) in the format of `HttpMethod\nUriPathname\nHttpParameters\nHttpHeaders\n`.
Here, HttpMethod is converted to lowercase, such as `get` or `put`; UriPathname is the request path, such as `/` or `/exampleobject`; and \n is a line break (if a string is empty, the line breaks before and after it need to be retained, such as `get\n/exampleobject\n\n\n`).

### Generating StringToSign
Generate the StringToSign based on the [KeyTime](#Generating KeyTime) and [HttpString](#Generating HttpString) in the format of `sha1\nKeyTime\nSHA1(HttpString)\n`.
Here, SHA1(HttpString) is the message digest generated by calculating the [HttpString](#Generating HttpString) using [SHA1](#Preparations).

### Generating Signature
Calculate the message digest using [HMAC-SHA1](#Preparations) with [SignKey](#Generating SignKey) as the key and [StringToSign](#Generating StringToSign) as the message, which is the Signature.

### Generating the Actual Signature
Generate the actual signature based on [SecretId](#Preparations), [KeyTime](#Generating KeyTime), [HeaderList](#Generating HeaderList and HttpHeaders), [UrlParamList](#Generating UrlParamList and HttpParameters), and [Signature](#Generating Signature) in the following format:
```shell
q-sign-algorithm=sha1
&q-ak=SecretId
&q-sign-time=KeyTime
&q-key-time=KeyTime
&q-header-list=HeaderList
&q-url-param-list=UrlParamList
&q-signature=Signature
```

> Line breaks in the example above are for easy understanding only and are not included in a real signature.

## Signature Use
Signed HTTP requests initiated to COS via RESTful APIs can pass the signature in the following ways:
1. Pass through a standard HTTP Authorization header, such as `Authorization: q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753;1557996953&...&q-signature=...`
2. Pass as an HTTP request parameter (be sure to UrlEncode), such as `/exampleobject?q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753%3B1557996953&...&q-signature=...`

> In the example above, `...` is used to substitute the specific signature content.

## Sample Code

### Pseudocode
```shell
KeyTime = [Now];[Expires]
SignKey = HMAC-SHA1([SecretKey], KeyTime)
HttpString = [HttpMethod]\n[HttpURI]\n[HttpParameters]\n[HttpHeaders]\n
StringToSign = sha1\nKeyTime\nSHA1(HttpString)\n
Signature = HMAC-SHA1(SignKey, StringToSign)
```

### Sample Message Digest Calculation

The samples below illustrate how to call HMAC-SHA1 in different languages:

#### PHP

```shell
$sha1HttpString = sha1('ExampleHttpString');

$signKey = hash_hmac('sha1', 'ExampleKeyTime', 'YourSecretKey');
```

#### Java

```shell
import org.apache.commons.codec.digest.DigestUtils;
import org.apache.commons.codec.digest.HmacUtils;

String sha1HttpString = DigestUtils.sha1Hex("ExampleHttpString");

String signKey = HmacUtils.hmacSha1Hex("YourSecretKey", "ExampleKeyTime");
```

#### Python

```shell
import hmac
import hashlib

sha1 = hashlib.sha1()
sha1_http_string = sha1.update('ExampleHttpString'.encode('utf-8')).hexdigest()

sign_key = hmac.new('YourSecretKey'.encode('utf-8'), 'ExampleKeyTime'.encode('utf-8'), hashlib.sha1).hexdigest()
```

#### Node.js

```shell
var crypto = require('crypto');

var sha1HttpString = crypto.createHash('sha1').update('ExampleHttpString').digest('hex');
var signKey = crypto.createHmac('sha1', 'YourSecretKey').update('ExampleKeyTime').digest('hex');
```

#### Go

```shell
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

## Use Case

### Preparations

Obtain your APPID, SecretId, and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console. Below is an example:

| APPID      | SecretId                             | SecretKey                        |
| ---------- | ------------------------------------ | -------------------------------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz |

### Uploading an Object

#### Original Request

```shell
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

#### Intermediate Variables

- KeyTime = `1557989151;1557996351`
- SignKey = `eb2519b498b02ac213cb1f3d1a3d27a3b3c9bc5f`
- UrlParamList = `(empty string)`
- HttpParameters = `(empty string)`
- HeaderList = `content-length;content-md5;content-type;date;host;x-cos-acl;x-cos-grant-read`
- HttpHeaders = `content-length=13&content-md5=mQ%2FfVh815F3k6TAUm8m0eg%3D%3D&content-type=text%2Fplain&date=Thu%2C%2016%20May%202019%2006%3A45%3A51%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22`
- HttpString = `put\n/exampleobject(tencentcloud)\n\ncontent-length=13&content-md5=mQ%2FfVh815F3k6TAUm8m0eg%3D%3D&content-type=text%2Fplain&date=Thu%2C%2016%20May%202019%2006%3A45%3A51%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22\n`
- StringToSign = `sha1\n1557989151;1557996351\n8b2751e77f43a0995d6e9eb9477f4b685cca4172\n`
- Signature = `3b8851a11a569213c17ba8fa7dcf2abec6935172`

Here, (empty string) represents an empty string with a length of 0 and `\n` a line break.

#### Signed Request

```shell
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

### Downloading an Object

#### Original Request

```shell
GET /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91)?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D600 HTTP/1.1
Date: Thu, 16 May 2019 06:55:53 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### Intermediate Variables

- KeyTime = `1557989753;1557996953`
- SignKey = `937914bf490e9e8c189836aad2052e4feeb35eaf`
- UrlParamList = `response-cache-control;response-content-type`
- HttpParameters = `response-cache-control=max-age%3D600&response-content-type=application%2Foctet-stream`
- HeaderList = `date;host`
- HttpHeaders = `date=Thu%2C%2016%20May%202019%2006%3A55%3A53%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com`
- HttpString = `get\n/exampleobject(tencentcloud)\nresponse-cache-control=max-age%3D600&response-content-type=application%2Foctet-stream\ndate=Thu%2C%2016%20May%202019%2006%3A55%3A53%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com\n`
- StringToSign = `sha1\n1557989753;1557996953\n54ecfe22f59d3514fdc764b87a32d8133ea611e6\n`
- Signature = `01681b8c9d798a678e43b685a9f1bba0f6c0e012`

Here, `\n` represents a line break.

#### Signed Request

```shell
GET /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91)?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D600 HTTP/1.1
Date: Thu, 16 May 2019 06:55:53 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1557989753;1557996953&q-key-time=1557989753;1557996953&q-header-list=date;host&q-url-param-list=response-cache-control;response-content-type&q-signature=01681b8c9d798a678e43b685a9f1bba0f6c0e012
```