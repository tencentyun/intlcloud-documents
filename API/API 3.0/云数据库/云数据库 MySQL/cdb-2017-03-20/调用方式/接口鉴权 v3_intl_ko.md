Tencent Cloud API는 각 액세스 요청에 대해 자격 증명을 진행하고 각 요청은 공통 요청 매개변수 중에 서명 정보(Signature)를 포함시켜 요청자의 ID를 확인해야 합니다.
서명 정보는 보안 자격 증명에서 생성되며, 보안 자격 증명에는 SecretId 및 SecretKey가 포함됩니다. 사용자가 보안 자격 증명이 없을 경우, [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 신청하십시오. 그렇지 않으면 클라우드 API를 호출할 수 없습니다.

## 보안 자격 증명 신청
최초로 클라우드 API를 사용하기 전에 [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 보안 자격 증명을 신청하십시오.
보안 자격 증명은 SecretId 및 SecretKey로 구성됩니다.
* SecretId    API 호출자의 ID를 식별하는 데 사용됩니다.
* SecretKey는 서명 문자열 암호화 및 서버측 서명 문자열 인증에 사용되는 키입니다.
* <font color='red'>사용자는 보안 자격 증명을 철저히 관리하여 누출되지 않도록 해야 합니다.</font>

보안 자격 증명 신청의 구체적 단계:

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi)의 콘솔 페이지로 갑니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi) 페이지에서 [키 생성]을 클릭하면 SecretId/SecretKey 한 쌍을 생성할 수 있습니다.

주의: 개발사 계정은 최대 SecretId / SecretKey 두 쌍을 보유할 수 있습니다.

## TC3-HMAC-SHA256 서명 방법

주의: GET 방법에 대해서는 Content-Type: application/x-www-form-urlencoded 프로토콜 형식만 지원합니다. POST 방법은 현재 Content-Type: application/json 및 Content-Type: multipart/form-data의 두 가지 프로토콜 형식을 지원하며, json 형식은 기본적으로 모든 서비스 API에서 지원됩니다. multipart 형식은 특정 서비스 API에서만 지원되며 이때 해당 API가 json 형식으로 호출되지 못합니다. 서비스별 API 문서의 설명을 참조하십시오.

다음에서 CVM으로 광저우 지역 인스턴스 리스트를 조회하는 예를 들어 서명 컴퓨팅 프로세스를 단계별로 소개합니다. 인스턴스 리스트 조회의 Limit 및 Offset의 두 가지 매개변수를 사용했고, GET 방법으로 호출했습니다.

사용자의 SecretId와 SecretKey는 각각 다음과 같습니다. AKID**********************0123456789EXAMPLE 및 sk0123456789********************EXAMPLE.

### 1. 정규 요청 문자열 합치기

다음과 같이 정규 요청 문자열(CanonicalRequest)을 합치기 합니다.

```
CanonicalRequest =
    HTTPRequestMethod + '\n' +
    CanonicalURI + '\n' +
    CanonicalQueryString + '\n' +
    CanonicalHeaders + '\n' +
    SignedHeaders + '\n' +
    HashedRequestPayload
```

- HTTPRequestMethod: HTTP 요청 방법(GET, POST), 본 예시에서는 GET입니다.
- CanonicalURI: URI 매개변수, API 3.0는 슬래시(/)로 고정됩니다.
- CanonicalQueryString: HTTP 요청 URL 중 조회 문자열, POST 요청에 대해 빈 문자열로 고정되어 있고, GET 요청에 대해 URL의 물음표(?) 뒤의 문자열 내용입니다. 본 예시의 값은 Limit=10&Offset=0입니다. 주의: CanonicalQueryString은 URL로 인코딩해야 합니다.
- CanonicalHeaders: 서명에 참여하는 헤더 정보, 적어도 host 및 content-type 두 가지 헤더를 포함하며, 서명에 참여할 사용자 지정의 헤더를 추가하여 자체 요청의 유일성 및 보안성을 향상시킬 수 있습니다. 합치기 규칙: 1)헤더 key 및 value는 통일적으로 소문자로 변환되고, 앞뒤 공백을 제거하며, key:value\n 형식에 따라 합치기 합니다. 2)여러 헤더의 경우 헤더 key(소문자)의 사전순에 따라 합치기를 진행합니다. 이 예시의 경우: `content-type:application/x-www-form-urlencoded\nhost:cvm.tencentcloudapi.com\n`이 됩니다.
- SignedHeaders: 서명에 참여하는 헤더 정보, 이번 요청에 어느 헤더가 서명에 참여하는지 설명합니다. CanonicalHeaders에 포함되는 헤더의 내용과 일대일로 대응합니다. content-type 및 host는 필수 헤더입니다. 합치기 규칙: 1)헤더 key는 통일적으로 소문자로 변환됩니다. 2)여러 헤더의 경우 key(소문자)는 사전순에 따라 합치기를 진행하고 세미콜론(;)으로 구분됩니다. 이 예시의 경우: `content-type;host`가 됩니다.
- HashedRequestPayload: 요청 본문의 해시 값, 계산 방법은 Lowercase(HexEncode(Hash.SHA256(RequestPayload))), HTTP 요청 전체 본문 payload에 대해 SHA256 해시한 후, 16진수 인코딩되고 마지막으로 인코딩 문자열이 소문자로 변환됩니다. 주의: GET 요청의 경우, RequestPayload는 빈 문자열로 고정되며 POST 요청의 경우 RequestPayload는 HTTP 요청 본문 payload입니다.

위의 규칙에 따라 예시에서 얻은 정규 요청 문자열은 다음과 같습니다(명확하게 표시하기 위해 \n 줄 바꿈 부호는 직접 새 행 바꿈으로 대체함).
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

다음과 같이 서명 대기 문자열을 합치기 합니다.

```
StringToSign =
    Algorithm + \n +
    RequestTimestamp + \n +
    CredentialScope + \n +
    HashedCanonicalRequest
```

- Algorithm: 서명 알고리즘, 현재 TC3-HMAC-SHA256으로 고정됩니다.
- RequestTimestamp: 요청 타임스탬프, 즉 요청 헤더의 X-TC-Timestamp 값, 위의 예시 요청은 1539084154입니다.
- CredentialScope: 자격 증명 범위, 형식은 Date/service/tc3_request, 날짜, 요청한 서비스 및 정지 문자열(tc3_request)이 포함됩니다. Date는 UTC 기준 날짜이며, 값은 공통 매개변수 X-TC-Timestamp가 변환된 UTC 기준 날짜와 동일해야 합니다. service는 제품 이름이며 호출된 제품 도메인 이름과 일치해야 합니다(예: cvm). 위의 예시 요청 값은 2018-10-09/cvm/tc3_request입니다.
- HashedCanonicalRequest: 앞서 설명한 합치기 단계에서 얻은 정규 요청 문자열의 해시 값, 컴퓨팅 방법은 Lowercase(HexEncode(Hash.SHA256(CanonicalRequest)))입니다.

위의 규칙에 따라 예시에서 얻은 서명 대기 문자열은 다음과 같습니다(명확하게 표시하기 위해 \n 줄 바꿈 부호는 직접 새 행 바꿈으로 대체함).

```
TC3-HMAC-SHA256
1539084154
2018-10-09/cvm/tc3_request
91c9c192c14460df6c1ffc69e34e6c5e90708de2a6d282cccf957dbf1aa7f3a7
```

### 3. 서명 컴퓨팅
1)파생 서명 키 컴퓨팅. 의사 코드는 다음과 같습니다.

```
SecretKey = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"
SecretDate = HMAC_SHA256("TC3" + SecretKey, Date)
SecretService = HMAC_SHA256(SecretDate, Service)
SecretSigning = HMAC_SHA256(SecretService, "tc3_request")
```

- SecretKey: 원본 SecretKey.
- Date: Credential 내의 Date 필드 정보, 위 예시의 경우: 2018-10-09.
- Service: Credential 내의 Service 필드 정보, 위 예시의 경우: cvm.

2)서명 컴퓨팅. 의사 코드는 다음과 같습니다

```
Signature = HexEncode(HMAC_SHA256(SecretSigning, StringToSign))
```

- SecretSigning: 위에서 컴퓨팅으로 얻은 파생 서명 키.
- StringToSign: 2단계 컴퓨팅으로 얻은 서명 대기 문자열.

### 4. Authorization 합치기

다음과 같이 Authorization을 합치기 합니다.

```
Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', '
    'Signature=' + Signature
```

- Algorithm: 서명 방법, TC3-HMAC-SHA256으로 고정.
- SecretId: 키 쌍 내의 SecretId.
- CredentialScope: 위 참조, 자격 증명 범위.
- SignedHeaders: 위 참조, 서명에 포함된 헤더 정보.
- Signature: 서명 값.

위의 규칙에 따라 예시에서 얻은 값:

```
TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
```

마지막으로 완전 호출 정보:

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKID**********************0123456789EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

### 5. 서명 데모

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
    private final static String SECRET_ID = "AKID**********************0123456789EXAMPLE";
    private final static String SECRET_KEY = "sk0123456789********************EXAMPLE";
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
        // 시간대에 주의하십시오. 그렇지 않으면 오류가 발생할 수 있습니다.
        sdf.setTimeZone(TimeZone.getTimeZone("UTC"));
        String date = sdf.format(new Date(Long.valueOf(timestamp + "000")));

        // ************* 1단계: 정규 요청 문자열 합치기 *************
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
secret_id = "AKID**********************0123456789EXAMPLE"
secret_key = "sk0123456789********************EXAMPLE"

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

# ************* 1단계: 정규 요청 문자열 합치기 *************
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
# 서명 요약 함수
def sign(key, msg):
    return hmac.new(key, msg.encode("utf-8"), hashlib.sha256).digest()
secret_date = sign(("TC3" + secret_key).encode("utf-8"), date)
secret_service = sign(secret_date, service)
secret_signing = sign(secret_service, "tc3_request")
signature = hmac.new(secret_signing, string_to_sign.encode("utf-8"), hashlib.sha256).hexdigest()
print(signature)

# ************* 4단계:Authorization 합치기 *************
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

다음의 서명 실패 오류 코드가 존재할 수 있습니다. 실제 상황에 따라 처리하십시오.

| 오류 코드 | 오류 설명 |
|----------|---------|
| AuthFailure.SignatureExpire | 서명 만료됨 |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않음 |
| AuthFailure.SignatureFailure | 서명 오류 |
| AuthFailure.TokenFailure | token 오류 |
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님) |

