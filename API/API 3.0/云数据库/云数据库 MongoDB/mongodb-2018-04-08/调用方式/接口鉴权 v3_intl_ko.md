Tencent Cloud API는 모든 액세스 요청에 대해 ID 인증을 진행합니다. 즉, 요청자의 ID를 인증하기 위해 모든 요청은 공통 요청 매개변수에 서명 정보(Signature)가 포함되어 있어야 합니다.
서명 정보는 보안 자격 증명에 의해 생성됩니다. 보안 자격 증명은 SecretId와 SecretKey를 포함합니다. 사용자가 아직 보안 자격 증명이 없을 경우, [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 신청하십시오. 그렇지 않으면 클라우드 API를 호출할 수 없습니다.

## 보안 자격 증명 신청
처음 클라우드 API를 사용하기 전에 [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 보안 자격 증명을 신청하십시오.
보안 자격 증명은 SecretID와 SecretKey를 포함합니다.
* SecretID    API 호출자 ID를 표시하는 데 사용됩니다.
* SecretKey 서명 문자열과 서버의 검증 서명 문자열의 키를 암호화하는 데 사용됩니다.
* <font color='red'>사용자는 반드시 보안 자격 증명을 철저히 보관하여 유출을 방지해야 합니다.</font>

보안 자격 증명의 구체적인 신청 절차는 다음과 같습니다.

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi)의 콘솔 페이지로 이동합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi) 페이지에서, [생성]을 클릭하면 한 쌍의 SecretId/SecretKey를 생성할 수 있습니다.

주의: 개발자 계정은 최대 두 쌍의 SecretId/SecretKey를 보유할 수 있습니다.

## TC3-HMAC-SHA256 서명 방식

주의: GET 방식은 Content-Type: application/x-www-form-urlencoded 프로토콜 형식만 지원합니다. POST 방식은 현재 Content-Type: application/json 및 Content-Type: multipart/form-data 두 가지 프로토콜 형식을 지원합니다. json 형식은 모든 비즈니스 API에서 기본적으로 지원합니다. multipart 형식은 특정 비즈니스의 API에서만 지원하며 해당 API는 json 형식으로 호출할 수 없습니다. 비즈니스별 API 문서의 설명을 참조하십시오.

다음은 CVM이 광저우 지역의 인스턴스 리스트 조회를 예제로 하여 단계별로 서명의 컴퓨팅 프로세스를 소개하고 있습니다. 인스턴스 리스트 조회의 두 개의 매개변수, Limit과 Offset만 사용하며 GET 방식으로 호출합니다.

사용자의 SecretId와 SecretKey가 각각 AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE과 Gu5t9xGARNpq86cd98joQYCN3EXAMPLE이라고 가정합니다.

### 1. 정규 요청열 합치기

다음과 같은 형식으로 정규 요청열(CanonicalRequest)을 합치십시오.

```
CanonicalRequest =
    HTTPRequestMethod + '\n' +
    CanonicalURI + '\n' +
    CanonicalQueryString + '\n' +
    CanonicalHeaders + '\n' +
    SignedHeaders + '\n' +
    HashedRequestPayload
```

- HTTPRequestMethod: HTTP 요청 방식(GET, POST), 본 예제에서는 GET 방식을 사용하였습니다.
- CanonicalURI: URI 매개변수, API 3.0은 슬래시(/)를 고정적으로 사용합니다.
- CanonicalQueryString: HTTP 요청 발송 시 URL 중의 조회 문자열. POST 요청은 고정적으로 빈 문자열이고 GET 요청은 URL 중 물음표(?) 뒤의 문자열입니다. 본 예제의 값은 Limit=10&Offset=0입니다. 주의: CanonicalQueryString은 URL 인코딩을 해야 합니다.
- CanonicalHeaders: 서명의 헤더 정보. 적어도 host와 content-type 두 가지의 헤더를 포함합니다. 또한, 사용자 정의한 헤더를 서명에 추가하여 자체 요청의 유일성과 보안성을 향상시킬 수 있습니다. 합치기 규칙: 1)헤더 key와 value는 모두 소문자로 전환하고 앞뒤 빈칸을 지웁니다. 그리고 key:value\n 형식에 따라 합칩니다. 2)다중 헤더의 경우, 헤더 key(소문자)의 사전순에 따라 합칩니다. 이 예제는 `content-type:application/x-www-form-urlencoded\nhost:cvm.tencentcloudapi.com\n`이 됩니다.
- SignedHeaders: 서명의 헤더 정보. 이번 요청에 포함된 헤더 정보를 설명합니다. CanonicalHeaders에 포함된 헤더의 내용과 일일이 대응합니다. content-type과 host는 필수 선택 사항입니다. 합치기 규칙: 1)헤더 key는 모두 소문자로 전환합니다. 2)다중 헤더 key(소문자)는 사전순에 따라 합치고 세미콜론(;)으로 구분됩니다. 이 예제는 `content-type;host`가 됩니다.
- HashedRequestPayload: 요청 본문의 해시값. 컴퓨팅 방식은 Lowercase(HexEncode(Hash.SHA256(RequestPayload)))입니다. 전체 HTTP 요청 본문 payload에 대해 SHA256 해시를 실행한 뒤, 16진수 인코딩하여 마지막으로 인코딩 문자열을 소문자로 전환합니다. 주의: GET 요청의 경우 RequestPayload가 항상 빈 문자열이고 POST 요청의 경우 RequestPayload가 HTTP 요청 본문의 payload가 됩니다.

위의 규칙에 따라 예제에서 얻은 정규 요청열은 다음과 같습니다(명확하게 보여드리기 위해 \n 새줄 문자를 직접 줄 바꿈으로 대체하였습니다).
```
GET
/
Limit=10&Offset=0
content-type:application/x-www-form-urlencoded
host:cvm.api.tencentyun.com

content-type;host
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

### 2. 서명 대기 문자열 합치기

다음과 같은 형식으로 서명 대기 문자열을 합칩니다.

```
StringToSign =
    Algorithm + \n +
    RequestTimestamp + \n +
    CredentialScope + \n +
    HashedCanonicalRequest
```

- Algorithm: 서명 알고리즘. 현재 TC3-HMAC-SHA256으로 고정되어 있습니다.
- RequestTimestamp: 요청 타임스탬프. 즉, 요청 헤더의 X-TC-Timestamp 값. 위 요청 예제에서는 1539084154에 해당합니다.
- CredentialScope: 자격 증명 범위. 형식은 Date/service/tc3_request입니다. 날짜, 요청한 서비스와 종료 문자열(tc3_request)을 포함합니다. Date는 UTC 표준 시간의 날짜이며 값은 공통 매개변수 X-TC-Timestamp로 환산한 UTC 표준 시간의 날짜와 일치해야 합니다. service는 제품명이며 반드시 호출한 제품의 도메인 이름과 일치해야 합니다(예: CVM). 위 요청 예제에서 값은 2018-10-09/cvm/tc3_request가 됩니다.
- HashedCanonicalRequest: 전술한 단계를 합쳐 얻은 정규 요청열의 해시값. 컴퓨팅 방법은 Lowercase(HexEncode(Hash.SHA256(CanonicalRequest)))입니다.

위 규칙에 따라 예제 중 얻은 서명 대기 문자열은 다음과 같습니다(명확하게 보여드리기 위해 \n 새줄 문자를 직접 줄 바꿈으로 대체하였습니다).

```
TC3-HMAC-SHA256
1539084154
2018-10-09/cvm/tc3_request
91c9c192c14460df6c1ffc69e34e6c5e90708de2a6d282cccf957dbf1aa7f3a7
```

### 3. 서명 컴퓨팅
1)파생 서명 키 컴퓨팅. 의사코드는 다음과 같습니다.

```
SecretKey = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"
SecretDate = HMAC_SHA256("TC3" + SecretKey, Date)
SecretService = HMAC_SHA256(SecretDate, Service)
SecretSigning = HMAC_SHA256(SecretService, "tc3_request")
```

- SecretKey: 초기의 SecretKey.
- Date: Credential 중의 Date 필드 정보. 위 예제에서는 2018-10-09입니다.
- Service: Credential 중의 Service 필드 정보. 위 예제에서는 cvm입니다.

2)서명 컴퓨팅. 의사코드는 다음과 같습니다.

```
Signature = HexEncode(HMAC_SHA256(SecretSigning, StringToSign))
```

- SecretSigning: 위 컴퓨팅으로 얻은 파생 서명 키.
- StringToSign: 2단계에서 컴퓨팅으로 얻은 서명 대기 문자열.

### 4. Authorization 합치기

다음의 형식으로 Authorization를 합칩니다.

```
Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', '
    'Signature=' + Signature
```

- Algorithm: 서명 방식. TC3-HMAC-SHA256으로 고정되어 있습니다.
- SecretId: 키 페어 중의 SecretId.
- CredentialScope: 자격 증명 범위, 윗글 참조.
- SignedHeaders: 서명에 포함한 헤더 정보, 윗글 참조.
- Signature: 서명값

위 규칙에 따라 예제 중 얻은 값은 다음과 같습니다.

```
TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
```

최종적으로 완전한 호출 정보는 다음과 같습니다.

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

### 5. 서명 예제

#### Java

```
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URL;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Map;
import java.util.TimeZone;
import java.util.TreeMap;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import javax.net.ssl.HttpsURLConnection;
import javax.xml.bind.DatatypeConverter;

import org.apache.commons.codec.digest.DigestUtils;

public class TencentCloudAPITC3Demo {
    private final static String CHARSET = "UTF-8";
    private final static String ENDPOINT = "cvm.tencentcloudapi.com";
    private final static String PATH = "/";
    private final static String SECRET_ID = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE";
    private final static String SECRET_KEY = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE";
    private final static String CT_X_WWW_FORM_URLENCODED = "application/x-www-form-urlencoded";
    private final static String CT_JSON = "application/json";
    private final static String CT_FORM_DATA = "multipart/form-data";

    public static byte[] sign256(byte[] key, String msg) throws Exception {
        Mac mac = Mac.getInstance("HmacSHA256");
        SecretKeySpec secretKeySpec = new SecretKeySpec(key, mac.getAlgorithm());
        mac.init(secretKeySpec);
        return mac.doFinal(msg.getBytes(CHARSET));
    }

    public static void main(String[] args) throws Exception {
        String service = "cvm";
        String host = "cvm.tencentcloudapi.com";
        String region = "ap-guangzhou";
        String action = "DescribeInstances";
        String version = "2017-03-12";
        String algorithm = "TC3-HMAC-SHA256";
        String timestamp = "1539084154";
        //String timestamp = String.valueOf(System.currentTimeMillis() / 1000);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        // 오류가 발생하지 않도록 시간대를 주의하십시오.
        sdf.setTimeZone(TimeZone.getTimeZone("UTC"));
        String date = sdf.format(new Date(Long.valueOf(timestamp + "000")));

        // ************* 1단계: 정규 요청열 합치기 *************
        String httpRequestMethod = "GET";
        String canonicalUri = "/";
        String canonicalQueryString = "Limit=10&Offset=0";
        String canonicalHeaders = "content-type:application/x-www-form-urlencoded\n" + "host:" + host + "\n";
        String signedHeaders = "content-type;host";
        String hashedRequestPayload = DigestUtils.sha256Hex("");
        String canonicalRequest = httpRequestMethod + "\n" + canonicalUri + "\n" + canonicalQueryString + "\n"
                + canonicalHeaders + "\n" + signedHeaders + "\n" + hashedRequestPayload;
        System.out.println(canonicalRequest);

        // ************* 2단계: 서명 대기 문자열 합치기 *************
        String credentialScope = date + "/" + service + "/" + "tc3_request";
        String hashedCanonicalRequest = DigestUtils.sha256Hex(canonicalRequest.getBytes(CHARSET));
        String stringToSign = algorithm + "\n" + timestamp + "\n" + credentialScope + "\n" + hashedCanonicalRequest;
        System.out.println(stringToSign);

        // ************* 3단계: 서명 컴퓨팅 *************
        byte[] secretDate = sign256(("TC3" + SECRET_KEY).getBytes(CHARSET), date);
        byte[] secretService = sign256(secretDate, service);
        byte[] secretSigning = sign256(secretService, "tc3_request");
        String signature = DatatypeConverter.printHexBinary(sign256(secretSigning, stringToSign)).toLowerCase();
        System.out.println(signature);

        // ************* 4단계: Authorization 합치기 *************
        String authorization = algorithm + " " + "Credential=" + SECRET_ID + "/" + credentialScope + ", "
                + "SignedHeaders=" + signedHeaders + ", " + "Signature=" + signature;
        System.out.println(authorization);

        TreeMap<String, String> headers = new TreeMap<String, String>();
        headers.put("Authorization", authorization);
        headers.put("Host", host);
        headers.put("Content-Type", CT_X_WWW_FORM_URLENCODED);
        headers.put("X-TC-Action", action);
        headers.put("X-TC-Timestamp", timestamp);
        headers.put("X-TC-Version", version);
        headers.put("X-TC-Region", region);
    }
}
```

#### Python

```
# -*- coding: utf-8 -*-
import hashlib, hmac, json, os, sys, time
from datetime import datetime

# 키 매개변수
secret_id = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"
secret_key = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"

service = "cvm"
host = "cvm.tencentcloudapi.com"
endpoint = "https://" + host
region = "ap-guangzhou"
action = "DescribeInstances"
version = "2017-03-12"
algorithm = "TC3-HMAC-SHA256"
timestamp = 1539084154
date = datetime.utcfromtimestamp(timestamp).strftime("%Y-%m-%d")
params = {"Limit": 10, "Offset": 0}

# ************* 1단계: 정규 요청열 합치기 *************
http_request_method = "GET"
canonical_uri = "/"
canonical_querystring = "Limit=10&Offset=0"
ct = "x-www-form-urlencoded"
payload = ""
if http_request_method == "POST":
    canonical_querystring = ""
    ct = "json"
    payload = json.dumps(params)
canonical_headers = "content-type:application/%s\nhost:%s\n" % (ct, host)
signed_headers = "content-type;host"
hashed_request_payload = hashlib.sha256(payload.encode("utf-8")).hexdigest()
canonical_request = (http_request_method + "\n" +
                     canonical_uri + "\n" +
                     canonical_querystring + "\n" +
                     canonical_headers + "\n" +
                     signed_headers + "\n" +
                     hashed_request_payload)
print(canonical_request)

# ************* 2단계: 서명 대기 문자열 합치기 *************
credential_scope = date + "/" + service + "/" + "tc3_request"
hashed_canonical_request = hashlib.sha256(canonical_request.encode("utf-8")).hexdigest()
string_to_sign = (algorithm + "\n" +
                  str(timestamp) + "\n" +
                  credential_scope + "\n" +
                  hashed_canonical_request)
print(string_to_sign)


# ************* 3단계: 서명 컴퓨팅 *************
# 서명 컴퓨팅 해시 함수
def sign(key, msg):
    return hmac.new(key, msg.encode("utf-8"), hashlib.sha256).digest()
secret_date = sign(("TC3" + secret_key).encode("utf-8"), date)
secret_service = sign(secret_date, service)
secret_signing = sign(secret_service, "tc3_request")
signature = hmac.new(secret_signing, string_to_sign.encode("utf-8"), hashlib.sha256).hexdigest()
print(signature)

# ************* 4단계：Authorization 합치기 *************
authorization = (algorithm + " " +
                 "Credential=" + secret_id + "/" + credential_scope + ", " +
                 "SignedHeaders=" + signed_headers + ", " +
                 "Signature=" + signature)
print(authorization)

# 공통 매개변수를 요청 헤더에 추가
headers = {
    "Authorization": authorization,
    "Host": host,
    "Content-Type": "application/%s" % ct,
    "X-TC-Action": action,
    "X-TC-Timestamp": str(timestamp),
    "X-TC-Version": version,
    "X-TC-Region": region,
}
```


## 서명 실패

서명 실패 시 다음과 같은 오류 코드가 발생할 수 있습니다. 실제 상황에 따라 처리해 주십시오.

| 오류 코드 | 오류 설명 |
|----------|---------|
| AuthFailure.SignatureExpire | 서명 유효기간 만료 |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않음 |
| AuthFailure.SignatureFailure | 서명 오류 |
| AuthFailure.TokenFailure | token 오류 |
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님) |

