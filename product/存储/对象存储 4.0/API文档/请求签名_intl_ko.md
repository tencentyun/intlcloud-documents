> !
> 1. 이 문서는 COS XML 버전에 적용되며, 로그인 후 COS 콘솔 홈페이지에서 볼 수 있습니다.
> 2. 이 문서는 POST object의 HTTP 요청에 적용되지 않습니다.

COS를 사용할 때, RESTful API를 통해 COS에 대해 HTTP 익명 요청 또는 HTTP 서명 요청을 개시할 수 있으며 서명 요청에 대해 COS 서버는 요청 개시자에 대해 신분 인증을 진행하게 됩니다.

- 익명 요청: HTTP 요청은 어떠한 ID와 인증 정보도 지침하지 않으며, RESTful API를 통해 HTTP 요청 작업을 진행합니다.
- 서명 요청: HTTP 요청 시 서명을 추가합니다. COS 서버는 메시지 수신 후, 신분 인증을 진행합니다. 인증에 성공하면 요청을 수신 및 실행할 수 있습니다. 그렇지 않을 경우, 오류 정보를 반환하고 이 요청을 취소하게 됩니다.

Tencent Cloud COS는 키 HMAC(Hash Message Authentication Code)의 사용자 지정 HTTP 방안을 기반으로 하여 신분 인증을 수행합니다.
Tencent Cloud COS는 현재 사용자가 서명을 생성하도록 [COS 서명 도구](https://cos5.cloud.tencent.com/static/cos-sign/)를 제공하였습니다. 필요할 경우 사용하시면 됩니다.

## 서명 적용 시나리오

COS 서비스 적용 시나리오에서 대외 공개할 데이터에 대해 일반적으로 공개 읽기 및 비공개 읽기로 설정하는 것입니다. 즉, 모든 사람이 조회할 수 있으며, ACL 정책에 지정된 계정 또는 IP를 통해 쓰기 작업을 할 수 있습니다. 이때, ACL 정책과 API 요청 서명을 서로 결합하여 접속에 대해 신분 인증을 진행하고, 작업에 대해 권한과 유효 기간 관리를 할 수 있습니다.

>!SDK를 사용하여 개발하는 경우, 본문에서 설명한 API 요청 서명은 이미 그 안에 모두 포함되어 있습니다. **기존 API를 통해 2차 개발을 진행하려는 경우에만 본문 설명 절차에 따라 작업을 해야 합니다.**

이상의 시나리오에서 API 요청에 대해 여러 측면에서 보안 방어를 설정할 수 있습니다.

1. **요청자 신분 인증** 접근자의 고유 ID와 키를 통해 요청자의 신분을 확인합니다.
2. **전송 데이터 무결성 확보** 전송 내용의 무결성을 보장하기 위해 데이터를 암호화하고 검사합니다.
3. **서명 도난 방지** 서명 유효기간 설정 및 데이터 암호화를 통해 서명 도난 및 중복 사용을 방지합니다.

## 서명 프로세스

클라이언트는 HTTP 요청에 대해 서명한 후 해당 요청을 Tencent Cloud에 발송하여 서명 인증을 진행합니다. 구체적인 절차는 다음 그림과 같습니다.
![프로세스도](//mc.qcloudimg.com/static/img/4a1eb29033caa977c648cb84d9398fdd/image.png)

## 준비 작업

1. APPID, SecretId와 SecretKey.
   CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 획득합니다.
2. 개발 언어 확인.
   Java, PHP, C Sharp, C++, Node.js, Python를 지원하지만 한정되지는 않으며, 개발 언어에 따라 해당하는 HMAC-SHA1, SHA1 함수를 확인합니다.

## 서명 내용

RESTful API를 통해 COS에 개시한 HTTP 서명 요청. 표준 HTTP 인증 헤더를 사용하여 전송합니다. 아래 그림과 같습니다.

```shell
PUT ?versioning HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1480932292;1481012298&q-key-time=1480932292;1481012298&q-header-list=host&q-url-param-list=versioning&q-signature=438023e4a4207299d87bb75d1c739c06cc9406bb
```

여기서 서명 내용은 여러 개의 키-값 쌍으로 이루어지며, '&'를 통해 연결됩니다. 형식은 다음과 같습니다.

```shell
q-sign-algorithm=sha1&q-ak=[SecretID]&q-sign-time=[SignTime]&
q-key-time=[KeyTime]&q-header-list=[SignedHeaderList]&
q-url-param-list=[SignedParameterList]&q-signature=[Signature]
```

<span id="signaturesplit"></span>

### 키-값 설명

서명 내용을 구성하는 키-값(key=value) 설명은 다음과 같습니다.

<style>
table th:first-of-type {
    width: 150px;
}
</style><style  rel="stylesheet"> table th:nth-of-type(1) { width: 140px; }</style>

| 키(key)        | 값(value)                   | 설명                                                         | 필수 입력 여부 |
| ---------------- | --------------------------- | ------------------------------------------------------------ | -------- |
| q-sign-algorithm | sha1                        | 서명 알고리즘. 현재는 sha1만 지원합니다.                      | 예       |
| q-ak             | 매개변수 [*SecretID*]            | 계정 ID, 즉 SecretId. CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 획득할 수 있습니다.<br>**예:** AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q. | 예       |
| q-sign-time      | 매개변수 [*SignTime*]            | 이 서명의 유효 시작/종료 시간. [Unix 타임스탬프](#add)를 통해 시작과 종료 시간을 설명합니다. 단위는 초이고 형식은 [*start-seconds*];[*end-seconds*]입니다.<br>**예:** 1480932292;1481012298. | 예       |
| q-key-time       | 매개변수 [*KeyTime*]             | q-sign-time 값과 동일합니다.                                      | 예       |
| q-header-list    | 매개변수 [*SignedHeaderList*]    | HTTP 요청 헤더. key:value에서 일부 또는 전체 key를 추출하고 소문자로 전환해야 하며, 여러 개의 key를 사전순으로 정렬해야 합니다. 여러 그룹의 key가 있을 경우, ';'을 사용하여 연결할 수 있습니다.<br>**예:** HTTP 요청   ' Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com Content-Type: image/jpeg ', 이의 SignedHeaderList는 content-type;host입니다. | 예       |
| q-url-param-list | 매개변수 [*SignedParameterList*] | HTTP 요청 매개변수. key=value에서 일부 또는 전체 key를 추출하고 소문자로 전환해야 하며, 여러 개의 key를 사전순으로 정렬해야 합니다. 여러 그룹의 key가 있을 경우, ';'을 사용하여 연결할 수 있습니다.<br>**예:** HTTP 요청   ' GET /?prefix=abc&max-keys=20 ', SignedParameterList는 max-keys;prefix 또는 prefix입니다. | 예       |
| q-signature      | 매개변수 [Signature]             | HTTP 내용 서명. [Signature 계산](#signature)을 참조하십시오.         | 예       |

<a id="add">&nbsp;</a><!-- 앵커 포인트 정의 -->
>?q-sign-time과 q-key-time에 대하여:
>1. Unix 타임스탬프는 그리니치 표준시 1970년 01월 01일 00시 00분 00초(베이징 시간 1970년 01월 01일 08시 00분 00초)부터 현재까지 총 초 수입니다.
>2. 종료 타임스탬프는 시작 타임스탬프보다 커야 하며, 그렇지 않을 경우 서명이 바로 만료될 수 있습니다.
>**3. 서명 계산과 요청 발송 시, 로컬 시간이 국제 표준 시간과 보정되었는지 확인하십시오. 오차가 과도하게 클 경우, 서비스는 관련 요청을 거절하게 됩니다.**

<span id="signature"></span>
### Signature 계산

Signature 계산은 네 가지 절차로 나뉩니다.

1. 서명의 유효 시작/종료 시간에 대해 SignKey 값을 암호화하여 산출합니다.
2. 고정 형식에 따라 조합하여 HttpString을 생성합니다.
3. HttpString을 암호화하고 고정 형식에 따라 조합하여 StringToSign을 생성합니다.
4. StringToSign을 암호화하고 Signature를 생성합니다.

#### 코드 설명

의사 코드는 다음과 같습니다.

```shell
SignKey = HMAC-SHA1(SecretKey,"[q-key-time]")
HttpString = [HttpMethod]\n[HttpURI]\n[HttpParameters]\n[HttpHeaders]\n
StringToSign = [q-sign-algorithm]\n[q-sign-time]\nSHA1-HASH(HttpString)\n
Signature = HMAC-SHA1(SignKey,StringToSign)
```

각기 다른 개발 언어 환경에서 각기 다른 언어 규범을 사용하여 코드를 업데이트하십시오(다음 사항 포함).

1. 변수의 정의와 값은 사용하는 개발 언어의 규범에 따라 업데이트하십시오.
2. 가함수 SHA1-HASH, 16진법 소문자로 출력합니다.

#### 암호화 알고리즘 예시

언어별 HMAC-SHA1과 SHA1-HASH 호출 방법은 다음 예시를 참조하십시오.

#### PHP

```c
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

#### 매개변수 설명

| 매개변수               | 설명                                                         |
| ------------------ | ------------------------------------------------------------ |
| [q-key-time]       | 반드시 [키 값 설명](#signaturesplit)에 입력한 q-key-time과 일치해야 합니다. |
| [HttpMethod]       | HTTP 요청 방식. 소문자만 지원하므로 get, post, put, delete, head, options가 될 수 있습니다.<br>**예:** HTTP 요청   ' GET /testfile ', HttpMethod는 get입니다. |
| [HttpURI]          | HTTP 요청 URI 부분. 즉 '/'부터의 가상 루트 경로 부분입니다.<br>**예:** HTTP 요청 'GET /testfile의 HttpURI는 /testfile입니다.<br>**주의:** URI에 한글 또는 특수 문자가 포함되어 있으면 URLEncode를 진행하지 않습니다. |
| [HttpParameters]   | HTTP 요청 매개변수. 즉 URI 중 '?' 이후 '&'로 연결한 부분으로 전체 또는 부분 key=value를 선택해야 하며, key를 소문자로 전환하고 value는 URLEncode 전환을 해야 합니다. 여러 쌍의 key=value 사이는 '&'로 서로 연결하고 사전순으로 정렬해야 합니다.<br>**예:**  HTTP 요청   ' GET /?prefix=abc&max-keys=20 ', HttpParameters는 max-keys=20&prefix=abc 또는 prefix=abc입니다.<br>**주의:** 포함된 key=value 쌍의 key는 반드시 [키 값 설명](#signaturesplit)에 입력한 q-url-param-list의 key와 일치해야 합니다. |
| [HttpHeaders]      | HTTP 요청 헤더. 전체 또는 부분 key:value를 선택하고 key=value 형식으로 전환해야 하며, key는 소문자로 전환하고 value는 URLEncode 전환을 해야 합니다. 여러 쌍의 key=value 사이는 '&'로 서로 연결해야 하고 사전순으로 정렬해야 합니다.<br>**예:** HTTP 요청 ' Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com Content-Type: image/jpeg ', HttpHeaders는 content-type=image%2Fjpeg&host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com입니다.<br>**주의:** 포함된 key=value 쌍의 key는 반드시 [키 값 설명](#signaturesplit)에 입력한 q-header-list의 key와 일치해야 합니다. |
| [q-sign-algorithm] | sha1. 현재 sha1 암호화 알고리즘만 지원합니다.                             |
| [q-sign-time]      | 반드시 [키 값 설명](#signaturesplit)에 입력한 q-sign-time과 일치해야 합니다. |

#### 매개변수 인스턴스

| 매개변수               | 값                                                        |
| ------------------ | --------------------------------------------------------- |
| [q-key-time]       | 1417773892;1417853898                                     |
| [HttpMethod]       | get                                                       |
| [HttpURI]          | /testfile                                                 |
| [HttpParameters]   | max-keys=20&prefix=abc                                    |
| [HttpHeaders]      | host=examplebucket-1250000000.cos.ap-beijing.myqcloud.com |
| [q-sign-algorithm] | sha1                                                      |
| [q-sign-time]      | 1417773892;1417853898                                     |

## 사례 설명

어느 사용자가 API 호출 방식을 사용하여 객체를 다운로드 및 업로드하고 호출에 대해 서명하려 합니다.

### 준비 작업

CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에 로그인하여 APPID, SecretId와 SecretKey를 획득하고 개발 언어를 확인합니다. 다음과 같습니다.

| APPID      | SecretId                             | SecretKey                        | 개발 언어 |
| ---------- | ------------------------------------ | -------------------------------- | -------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz | PHP      |

### 업로드 객체

요구: 객체를 버킷 examplebucket에 업로드합니다.

초기 HTTP 요청은 다음과 같습니다.

```shell
PUT /example-file HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
x-cos-storage-class: standard

Hello world
```

서명 후 HTTP 요청은 다음과 같습니다.

```shell
PUT /example-file HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
x-cos-storage-class: standard
x-cos-content-sha1: 7b502c3a1f48c8609ae212cdfb639dee39673f5e
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1417773892;1417853898&q-key-time=1417773892;1417853898&q-header-list=host;x-cos-content-sha1;x-cos-storage-class&q-url-param-list=&q-signature=14e6ebd7955b0c6da532151bf97045e2c5a64e10

Hello world
```

매개변수별 해당하는 값과 설명은 다음과 같습니다.

| 키(key)          | 값(value)                                   | 비고                                     |
| ---------------- | ------------------------------------------- | ---------------------------------------- |
| q-sign-algorithm | sha1                                        | 현재 sha1 서명 알고리즘만 지원합니다.               |
| q-ak             | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q        | SecretId 필드                            |
| q-sign-time      | 1417773892;1417853898                       | 2014/12/5 18:04:52부터  2014/12/6 16:18:18까지
| q-key-time       | 1417773892;1417853898                       | 2014/12/5 18:04:52부터  2014/12/6 16:18:18까지
| q-header-list    | host;x-cos-content-sha1;x-cos-storage-class | HTTP 헤더 key의 리스트(사전순으로 정렬)         |
| q-url-param-list |                                             | HTTP 매개변수 리스트가 비어있음                        |
| q-signature      | 14e6ebd7955b0c6da532151bf97045e2c5a64e10    | 코드 계산을 통해 획득                         |

그 중, q-signature의 계산 코드는 다음과 같습니다.

```c
$signTime = '1417773892;1417853898';
$keyTime = $signTime;
$signKey = hash_hmac('sha1', $keyTime, 'BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz');
$httpString = "put\n/example-file\n\nhost=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&x-cos-content-sha1=7b502c3a1f48c8609ae212cdfb639dee39673f5e&x-cos-storage-class=standard\n";
$sha1edHttpString = sha1($httpString);
$stringToSign = "sha1\n$signTime\n$sha1edHttpString\n";
$signature = hash_hmac('sha1', $stringToSign, $signKey);
```

### 객체 다운로드

요구: 버킷 examplebucket 중 객체의 앞 4개 바이트를 다운로드합니다.

초기 HTTP 요청은 다음과 같습니다.

```shell
GET /example-file HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Range: bytes=0-3
```

서명 후 HTTP 요청은 다음과 같습니다.

```shell
GET /example-file HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Range: bytes=0-3
Authorization: q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1417773892;1417853898&q-key-time=1417773892;1417853898&q-header-list=host;range&q-url-param-list=&q-signature=4b6cbab14ce01381c29032423481ebffd514e8be
```

매개변수별 해당하는 값과 설명은 다음과 같습니다.

| 키(key)        | 값(value)                              | 비고                                     |
| ---------------- | ---------------------------------------- | ---------------------------------------- |
| q-sign-algorithm | sha1                                     | 현재 sha1 서명 알고리즘만 지원합니다.               |
| q-ak             | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q     | SecretId 필드                            |
| q-sign-time      | 1417773892;1417853898                    | 2014/12/5 18:04:52부터 2014/12/6 16:18:18까지 |
| q-key-time       | 1417773892;1417853898                    | 2014/12/5 18:04:52부터 2014/12/6 16:18:18까지 |
| q-header-list    | host;range                               | HTTP 헤더 key의 리스트                     |
| q-url-param-list |                                          | HTTP 매개변수 리스트가 비어있음                        |
| q-signature      | 4b6cbab14ce01381c29032423481ebffd514e8be | 코드 계산을 통해 획득                         |

그 중, q-signature의 계산 코드는 다음과 같습니다.

```c
$signTime = '1417773892;1417853898';
$keyTime = $signTime;
$signKey = hash_hmac('sha1', $keyTime, 'BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz');
$httpString = "get\n/testfile\n\nhost=examplebucket-1250000000.cos.ap-beijing.myqcloud.com&range=bytes%3D0-3\n";
$sha1edHttpString = sha1($httpString);
$stringToSign = "sha1\n$signTime\n$sha1edHttpString\n";
$signature = hash_hmac('sha1', $stringToSign, $signKey);
```
