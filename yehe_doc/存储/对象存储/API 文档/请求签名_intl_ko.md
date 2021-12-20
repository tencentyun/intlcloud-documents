> !
> - 본 문서는 COS XML 버전 전용입니다.
> - HTTP를 통한 POST Object 요청에는 적용되지 않습니다.
> 


## 소개

익명 및 서명된 HTTP 요청을 지원하는 RESTful API를 통해 Cloud Object Storage(COS)를 사용할 수 있습니다. COS 서버는 서명된 요청의 요청자를 인증합니다.

- 익명 요청: 인증 정보를 전달하지 않고 RESTful API를 사용하여 전송되는 HTTP 요청입니다.
- 서명된 요청: 서명을 전달하는 HTTP 요청. COS 서버는 요청자를 인증하고 인증된 요청자가 발송한 요청만 실행합니다. 인증에 실패하면 COS는 오류 메시지를 반환하고 요청을 거부합니다.

COS는 HMAC(Hash Message Authentication Code)를 기반으로 하는 맞춤형 솔루션을 사용하여 요청자를 인증합니다.


## SDK에서 서명 구현

서명은 이미 COS SDK에 구현되어 있습니다. 즉, SDK를 사용하여 요청을 시작하거나 서명을 얻을 때 서명 문제를 무시할 수 있습니다. 서명 자체 구현 또는 다른 프로그래밍 언어를 통한 서명 구현은 하기 프로그래밍 언어별 서명 구현 파일을 참고하십시오.

| SDK | 서명 구현 파일 |
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
| 미니프로그램 SDK | [util.js](https://github.com/tencentyun/cos-wx-sdk-v5/blob/master/src/util.js) (getAuth) |



## 서명된 URL 생성



현재 모든 COS [SDK](https://intl.cloud.tencent.com/document/product/436/6474)는 일정 기간 동안 유효한 서명을 포함하는 URL을 생성할 수 있습니다. 서명은 PUT 및 GET 요청을 지원합니다. 따라서 생성된 서명된 URL을 사용하여 별도의 서명을 생성할 필요 없이 객체를 직접 업로드/다운로드할 수 있습니다.

- 업로드를 위해 서명된 URL을 생성할 때 Content-Type 및 Content-MD5와 같은 헤더를 지정하여 업로드할 미디어 유형/콘텐츠를 제한할 수도 있습니다. 업로드와 관련된 요청 헤더의 구성은 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)를 참고하십시오.
- 다운로드를 위해 서명된 URL을 생성할 때 다운로드 시 응답 헤더를 일시적으로 수정할 수 있도록 response-xxx를 지정할 수도 있습니다. 다운로드와 관련된 요청 매개변수의 구성은 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)를 참고하십시오.

아래 표에서 SDK 언어에 해당하는 사전 서명된 URL 문서를 찾으십시오.

>?
>- 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
>- 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.

| SDK            | 사전 서명된 URL 문서                                              |
| -------------- | ------------------------------------------------------------ |
| Android SDK    | [사전 서명된 URL 생성](https://intl.cloud.tencent.com/document/product/436/37680) |
| C SDK          | 사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31520) |
| C++ SDK        | [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31524) |
| .NET(C#) SDK   | [사전 서명된 URL 생성](https://intl.cloud.tencent.com/document/product/436/38068) |
| Go SDK         | [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31528) |
| iOS SDK       | [사전 서명된 URL 생성](https://intl.cloud.tencent.com/document/product/436/37690) |
| Java SDK       | [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31536) |
| JavaScript SDK | [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31540) |
| Node.js SDK    | [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/32455) |
| PHP SDK        | [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/43312) |
| Python SDK     | [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31548) |
| 미니프로그램 SDK     | [사전 서명된 URL](https://intl.cloud.tencent.com/document/product/436/31711) |



## 사용 사례

COS 객체를 공개해야 하는 경우 일반적으로 이 객체를 public-read/private-write로 설정해야 합니다(모든 사람이 객체를 읽을 수 있지만 ACL 지정 계정만 쓸 수 있음). 그런 다음 ACL 정책을 API 요청 서명과 함께 사용하여 요청자를 인증하고 작업의 권한 및 유효 기간을 제어할 수 있습니다.

>! 본문에서 설명하는 API 요청 서명은 이미 SDK에 포함되어 있습니다. **네이티브 API를 기반으로 재개발하려는 경우에만 아래 단계를 수행하십시오**.
>

위의 사용 사례에 대해 다음과 같이 API 요청을 보호할 수 있습니다.

1. **요청자 인증**. 요청자의 고유 ID와 키로 요청자의 신원을 확인합니다.
2. **전송 중 데이터 변조 방지**. 전송 중 무결성을 보장하기 위해 데이터에 서명하고 확인합니다.
3. **서명 도용 방지**. 서명이 도용되거나 반복적으로 사용되는 것을 방지하기 위해 서명의 유효 기간을 설정합니다.

## 준비 작업

1. APPID, SecretId 및 SecretKey를 가져옵니다. 
CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 얻을 수 있습니다.
2. 프로그래밍 언어를 결정합니다.
지원되는 언어에는 Java, PHP, .NET, C++, Node.js 및 Python이 포함되지만 이에 국한되지 않습니다. 선택한 프로그래밍 언어에 따라 HMAC-SHA1, SHA1 및 UrlEncode 기능을 결정할 수 있습니다.
HMAC-SHA1 및 SHA1 함수는 UTF-8 인코딩 문자열을 입력하고 소문자 16진수 문자열을 출력하며, UrlEncode도 UTF-8 인코딩을 기반으로 합니다. 또한 ASCII 범위에서 다음과 같은 출력 가능한 특수 문자도 인코딩해야 합니다.

| 캐릭터 | 10진법 | 16진법 | 캐릭터 | 10진법 | 16진법 |
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

## 서명 생성

### 1단계: KeyTime 생성
1. 현재 시간의 Unix StartTimestamp를 가져옵니다. 1970년 1월 1일 00:00:00 UTC(1970년 1월 1일 베이징 시간 08:00:00)부터 현재 시간까지의 총 시간(초)입니다.
2. StartTimestamp 및 서명의 예상 유효 기간에 따라 만료될 서명에 대한 Unix EndTimestamp를 계산합니다.
3. 위의 두 타임스탬프를 `StartTimestamp;EndTimestamp` 형식(예: `1557902800;1557910000`)으로 연결하여 KeyTime을 생성합니다.

### 2단계: SignKey 생성
[HMAC-SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C)을 사용하여 [SecretKey](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C)를 키로, [KeyTime](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.9F.E6.88.90-keytime)을 메시지로 `eb2519b498b02ac213cb1f3d1a3d27a3b3c9bc5f`와 같은 소문자 16진수 형식의 해시 값인 메시지 다이제스트(즉, SignKey)를 계산합니다.


### 3단계: UrlParamList 및 HttpParameters 생성
1. HTTP 요청 매개변수를 탐색하여 key value Map 및 KeyList 생성
 - [UrlEncode](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C)를 사용하여 key를 인코딩하고 소문자로 변환합니다.
 - [UrlEncode](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C)를 사용하여 value를 인코딩합니다. 매개변수에 value가 없으면 해당 value는 빈 문자열로 간주됩니다. 예를 들어 요청 경로 `/?acl`은 `/?acl=`으로 간주됩니다.
>? HTTP 요청의 매개변수는 `?` 다음에 옵니다. 예를 들어 `/?versions&prefix=example-folder%2F&delimiter=%2F&max-keys=10` 요청 경로에서 요청 매개변수는 `versions&prefix=example-folder%2F&delimiter=%2F&max-keys=10`입니다.
>
2. 사전순으로 KeyList를 정렬합니다.
3. KeyList의 순서에 따라 `key1=value1&key2=value2&key3=value3` 형식으로 Map의 모든 키 값 쌍을 연결합니다. 즉, HttpParameters입니다.
4. `key1;key2;key3` 형식으로 KeyList의 순서로 모든 키를 연결합니다. 즉, UrlParamList입니다.

#### 예시:
- 예시1:
요청 경로: `/?prefix=example-folder%2F&delimiter=%2F&max-keys=10`
UrlParamList: `delimiter;max-keys;prefix`
HttpParameters: `delimiter=%2F&max-keys=10&prefix=example-folder%2F`
>! 요청이 전송되면 요청 경로의 요청 매개변수도 UrlEncode됩니다. 따라서 UrlEncode 작업을 반복하지 마십시오.
>
- 예시2:
요청 경로: `/exampleobject?acl`
UrlParamList: `acl`
HttpParameters: `acl=`

### 4단계: HeaderList 및 HttpHeaders 생성
1. HTTP 요청 매개변수를 트래버스하고 key value 매핑 맵 및 key 목록 KeyList를 생성합니다. 여기서 key는 [UrlEncode](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) 및 소문자로 변환되며 value는 URL 인코딩됩니다.
2. 사전순으로 KeyList를 정렬합니다.
3. `key1=value1&key2=value2&key3=value3` 형식으로 KeyList의 순서에 따라 Map의 모든 키 값 쌍을 연결합니다. 즉, HttpHeaders입니다.
4. `key1;key2;key3` 형식으로 KeyList의 순서에 따라 모든 키를 연결합니다. 즉, HeaderList입니다.

#### 예시:
요청 헤더:
```plaintext
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Date: Thu, 16 May 2019 03:15:06 GMT
x-cos-acl: private
x-cos-grant-read: uin="100000000011"
```
계산:
- HeaderList = `date;host;x-cos-acl;x-cos-grant-read`
- HttpHeaders = `date=Thu%2C%2016%20May%202019%2003%3A15%3A06%20GMT&host=examplebucket-1250000000.cos.ap-shanghai.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22`

### 5단계: HttpString 생성
HttpMethod, UriPathname, [HttpParameters](#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.94.9F.E6.88.90-urlparamlist-.E5.92.8C-httpparameters) 및 [HttpHeaders](#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E7.94.9F.E6.88.90-headerlist-.E5.92.8C-httpheaders)를 기반으로, `HttpMethod\nUriPathname\nHttpParameters\nHttpHeaders\n` 형식의 HttpString을 생성합니다.

그중에서,
- HttpMethod는 get 또는 put과 같이 소문자로 변환됩니다.
- UriPathname은 `/` 또는 `/exampleobject`와 같은 요청 경로입니다.
- `\n`은 줄 바꿈입니다. 빈 문자열이 있는 경우 해당 문자열 앞과 뒤에 줄 바꿈이 유지되어야 합니다(예: `get\n/exampleobject\n\n\n`).


### 6단계: StringToSign 생성
[KeyTime](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.9F.E6.88.90-keytime) 및 [HttpString](#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E7.94.9F.E6.88.90-httpstring)을 기반으로 `sha1\nKeyTime\nSHA1(HttpString)\n` 형식의 StringToSign을 생성합니다.
그중에서,
- sha1은 고정 문자열입니다.
- `\n`은 줄 바꿈입니다.
- SHA1(HttpString)은 [SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) 및 [HttpString](#.E6.AD.A5.E9.AA.A45.EF.BC.9A.E7.94.9F.E6.88.90-httpstring)으로 계산된 소문자 16진수 형식의 메시지 다이제스트입니다. 예: `54ecfe22f59d3514fdc764b87a32d8133ea611e6`.

### 7단계: Signature 생성
[HMAC-SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C)과 함께 [SignKey](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E7.94.9F.E6.88.90-signkey)(원래 바이너리가 아닌 문자열)를 키로 사용하고 [StringToSign](#.E6.AD.A5.E9.AA.A46.EF.BC.9A.E7.94.9F.E6.88.90-stringtosign)을 메시지로 사용하여 메시지 다이제스트, 즉 Signature를 계산합니다. 예: `01681b8c9d798a678e43b685a9f1bba0f6c0e012`.

### 8단계: 서명 생성
[SecretId](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C), [KeyTime](#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.9F.E6.88.90-keytime), [HeaderList](#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E7.94.9F.E6.88.90-headerlist-.E5.92.8C-httpheaders), [UrlParamList](#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.94.9F.E6.88.90-urlparamlist-.E5.92.8C-httpparameters) 및 [Signature](#.E6.AD.A5.E9.AA.A47.EF.BC.9A.E7.94.9F.E6.88.90-signature)를 기반으로 다음 형식의 서명을 생성합니다.
```plaintext
q-sign-algorithm=sha1
&q-ak=SecretId
&q-sign-time=KeyTime
&q-key-time=KeyTime
&q-header-list=HeaderList
&q-url-param-list=UrlParamList
&q-signature=Signature
```

>! 상기 형식의 줄 바꿈은 가독성만을 위한 것이며 실제 서명에는 포함되지 않습니다.
>

## 서명 사용
RESTful API를 통해 COS로 전송된 서명된 HTTP 요청은 다음과 같은 방식으로 서명을 전달할 수 있습니다.
1. `Authorization: q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753;1557996953&...&q-signature=...`와 같은 표준 HTTP Authorization 헤더를 통과합니다.
2. `/exampleobject?q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753%3B1557996953&...&q-signature=...`와 같은 HTTP 요청 매개변수로 전달합니다(URL 인코딩해야 함).

>? 상기 예시의 `...`는 서명입니다.
>

## 임시 자격 증명(키) 사용
서명 계산에 임시 자격 증명을 사용하는 경우 요청을 보낼 때 x-cos-security-token 필드를 지정해야 합니다. 이 필드를 지정하는 방법은 서명이 전달되는 방식에 따라 다릅니다.
1. 표준 HTTP Authorization 헤더를 사용하여 서명이 전달되는 경우 다음과 같이 x-cos-security-token을 요청 헤더로 지정합니다.
```plaintext
Authorization: q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753;1557996953&...&q-signature=...
x-cos-security-token: ...
```
2. 서명이 HTTP 요청 매개변수로 전달되는 경우 다음과 같이 x-cos-security-token을 요청 매개변수로 지정합니다.
```plaintext
/exampleobject?q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753%3B1557996953&...&q-signature=...&x-cos-security-token=...
```

>? 상기 예시에서 `...`는 서명 및 액세스 토큰입니다.
>

## 코드 예시

### 의사 코드
```plaintext
KeyTime = [Now];[Expires]
SignKey = HMAC-SHA1([SecretKey], KeyTime)
HttpString = [HttpMethod]\n[HttpURI]\n[HttpParameters]\n[HttpHeaders]\n
StringToSign = sha1\nKeyTime\nSHA1(HttpString)\n
Signature = HMAC-SHA1(SignKey, StringToSign)
```

### 메시지 다이제스트 알고리즘 예시

하기 예시는 다른 언어로 HMAC-SHA1을 호출하는 방법을 보여줍니다.

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

## 실제 사례

### 준비 과정

CAM 콘솔에 로그인하고 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지로 이동하여 APPID, SecretId 및 SecretKey를 얻습니다. 다음은 예시입니다.

| APPID      | SecretId                             | SecretKey                        |
| ---------- | ------------------------------------ | -------------------------------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz |

### 객체 업로드

#### 원본 요청

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

#### 중간 변수

- **KeyTime** = `1557989151;1557996351`
- **SignKey** = `eb2519b498b02ac213cb1f3d1a3d27a3b3c9bc5f`
- **UrlParamList** = `(empty string)`
- **HttpParameters** = `(empty string)`
- **HeaderList** = `content-length;content-md5;content-type;date;host;x-cos-acl;x-cos-grant-read`
- **HttpHeaders** = `content-length=13&content-md5=mQ%2FfVh815F3k6TAUm8m0eg%3D%3D&content-type=text%2Fplain&date=Thu%2C%2016%20May%202019%2006%3A45%3A51%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22`
- **HttpString** = `put\n/exampleobject(Tencent Cloud)\n\ncontent-length=13&content-md5=mQ%2FfVh815F3k6TAUm8m0eg%3D%3D&content-type=text%2Fplain&date=Thu%2C%2016%20May%202019%2006%3A45%3A51%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&x-cos-acl=private&x-cos-grant-read=uin%3D%22100000000011%22\n`
- **StringToSign** = `sha1\n1557989151;1557996351\n8b2751e77f43a0995d6e9eb9477f4b685cca4172\n`
- **Signature** = `3b8851a11a569213c17ba8fa7dcf2abec6935172`

여기서 (empty string)은 0바이트 문자열이고 `\n`은 줄 바꿈입니다.

#### 서명된 요청

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

### 객체 다운로드

#### 원본 요청

```plaintext
GET /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91)?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D600 HTTP/1.1
Date: Thu, 16 May 2019 06:55:53 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### 중간 변수

- **KeyTime** = `1557989753;1557996953`
- **SignKey** = `937914bf490e9e8c189836aad2052e4feeb35eaf`
- **UrlParamList** = `response-cache-control;response-content-type`
- **HttpParameters** = `response-cache-control=max-age%3D600&response-content-type=application%2Foctet-stream`
- **HeaderList** = `date;host`
- **HttpHeaders** = `date=Thu%2C%2016%20May%202019%2006%3A55%3A53%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com`
- **HttpString** = `get\n/exampleobject(Tencent Cloud)\nresponse-cache-control=max-age%3D600&response-content-type=application%2Foctet-stream\ndate=Thu%2C%2016%20May%202019%2006%3A55%3A53%20GMT&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com\n`
- **StringToSign** = `sha1\n1557989753;1557996953\n54ecfe22f59d3514fdc764b87a32d8133ea611e6\n`
- **Signature** = `01681b8c9d798a678e43b685a9f1bba0f6c0e012`

여기서 `\n`은 줄 바꿈입니다.

#### 서명된 요청

```plaintext
GET /exampleobject(%E8%85%BE%E8%AE%AF%E4%BA%91)?response-content-type=application%2Foctet-stream&response-cache-control=max-age%3D600 HTTP/1.1
Date: Thu, 16 May 2019 06:55:53 GMT
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1557989753;1557996953&q-key-time=1557989753;1557996953&q-header-list=date;host&q-url-param-list=response-cache-control;response-content-type&q-signature=01681b8c9d798a678e43b685a9f1bba0f6c0e012
```
