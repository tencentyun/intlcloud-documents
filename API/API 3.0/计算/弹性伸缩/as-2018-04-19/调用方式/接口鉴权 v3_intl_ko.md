Tencent Cloud API 는 각 액세스 요청에 대해서 ID 검증을 합니다. 즉, 각 요청은 모두 공통 요청 매개변수 중 서명 정보(Signature)를 포함해 요청자 ID를 검증해야 합니다.
서명 정보는 보안 자격 증명의 의해 생성되고 보안 자격 증명은 SecretId와 SecretKey를 포함합니다. 사용자가 보안 자격 증명이 없으면 [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)로 가서 신청하고 그렇지 않으면 클라우드 API를 호출할 수 없습니다.

## 보안 자격 증명 신청
처음 클라우드 API를 사용하기 전에 [클라우드 API 키 페이지](https://console.cloud.tencent.com/capi)에서 보안 자격 증명을 신청하십시오.
보안 자격 증명은 SecretID와 SecretKey를 포함합니다.
* SecretID    API 호출자 ID를 식별하는 데 사용됩니다.
* SecretKey는 서명 문자열 암호화와 서버에서 서명 문자열 검증에 사용됩니다.
* <font color='red'>사용자는 보안 자격 증명을 잘 보관해 유출되지 않도록 해야 합니다.</font>

보안 자격 증명 신청 절차는 다음과 같습니다.

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi)의 콘솔 페이지로 이동합니다.
1. [클라우드 API 키](https://console.cloud.tencent.com/capi) 페이지로 가서 [생성]을 클릭하면 SecretId/SecretKey 한 쌍을 생성할 수 있습니다.

주의: 개발자 계정은 최대 SecretId/SecretKey 두 쌍을 보유할 수 있습니다.

## TC3-HMAC-SHA256 서명 방법

주의: GET 방법은 Content-Type: application/x-www-form-urlencoded 프로토콜 형식만 지원합니다. POST 방법은 현재 Content-Type: application/json 및 Content-Type: multipart/form-data 두 가지 프로토콜 형식을 지원합니다. json 형식은 기본 모든 비즈니스 API에서 지원합니다. multipart 형식은 특정 비즈니스 API에서만 지원하며, 이때 해당 API는 json 형식으로 호출할 수 없습니다. 비즈니스별 API 문서를 참조하십시오.

다음의 CVM에서 광저우 지역 인스턴스 리스트 조회를 예로 단계별로 서명의 컴퓨팅 과정을 설명합니다. 인스턴스 리스트 조회의 두 개의 매개변수, Limit와 Offset만 사용했으며 호출 방식은 GET입니다.

사용자의 SecretId와 SecretKey는 각각 AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE과 Gu5t9xGARNpq86cd98joQYCN3EXAMPLE인 것을 예로 합니다.

### 1. 정규 요청 문자열 압치기

다음 형식에 따라 정규 요청 문자열(CanonicalRequest)을 합칩니다.

```
CanonicalRequest =
    HTTPRequestMethod + '\n' +
    CanonicalURI + '\n' +
    CanonicalQueryString + '\n' +
    CanonicalHeaders + '\n' +
    SignedHeaders + '\n' +
    HashedRequestPayload
```

- HTTPRequestMethod: HTTP 요청 방식(GET, POST), 여기에서 GET입니다.
- CanonicalURI: URI 매개변수, API 3.0에는 고정으로 슬래시(/)입니다.
- CanonicalQueryString: HTTP 요청 URL에서의 조회 문자열입니다. POST 요청의 경우, 고정으로 빈 문자열이고 GET 요청의 경우, URL 중의 물음표(?) 뒤의 문자열 내용입니다. 본 예시 값은 Limit=10&Offset=0입니다. 주의: CanonicalQueryString은 URL 인코딩돼야 합니다.
- CanonicalHeaders: 서명에 포함한 헤더 정보. 적어도 Host와 Content-type 두 개 헤더를 포함하고 사용자 지정의 헤더를 추가해 요청의 유일성과 보안성을 높일 수 있습니다. 합치기 규칙: 1)헤더 key와 value는 일괄적으로 소문자로 전환하고 앞뒤 빈칸을 제거하고 key:value\n의 형식에 따라 연결합니다. 2)여러 헤더를 헤더 key(소문자)의 사전 순서에 따라 연결합니다. 여기는 `content-type:application/x-www-form-urlencoded\nhost:cvm.tencentcloudapi.com\n`이 됩니다.
- SignedHeaders: 서명에 포함한 헤더 정보. 해당 요청에 어느 헤드가 서명에 포함되는지 표시합니다. CanonicalHeaders에 포함한 헤더 내용과 일일이 대응합니다. content-type과 host는 필수 선택 헤더입니다. 합치기 규칙: 1)헤더 key는 일괄적으로 소문자로 전환합니다. 2)여러 헤더 key(소문자)를 사전 순서에 따라 연결하고 쌍반점(;)으로 구분합니다. 여기는 `Content-type;host`가 됩니다.
- HashedRequestPayload: 요청 본문의 해시값. 컴퓨팅 방법은 Lowercase(HexEncode(Hash.SHA256(RequestPayload)))로, HTTP 요청 전체 본문 payload에 대해서 SHA256 해시를 하고 그 다음 16진 인코딩 후 마지막으로 인코딩 문자열을 소문자 알파벳으로 전환합니다. 주의: GET 요청의 경우 RequestPayload는 고정으로 빈 문자열이고 POST 요청의 경우 RequestPayload는 HTTP 요청 본문 Payload입니다.

상기 규칙에 따라 예시 중에서 얻은 정규 요청 문자열은 다음과 같습니다(잘 보이기 위해 \n 줄바꿈 부호는 직접 새 새줄로 바꿈으로 대체됩니다).
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

다음의 형식에 따라 서명 대기 문자열을 연결합니다.

```
StringToSign =
    Algorithm + \n +
    RequestTimestamp + \n +
    CredentialScope + \n +
    HashedCanonicalRequest
```

- Algorithm: 서명 알고리즘, 현재 TC3-HMAC-SHA256으로 고정합니다.
- RequestTimestamp: 요청 타임스탬프, 즉 요청 헤더의 X-TC-Timestamp 값입니다. 위 요청에는 1539084154입니다.
- CredentialScope: 자격 증명 범위, 형식은 Date/service/tc3_request입니다. 일자, 요청한 서비스와 종료 문자열(tc3_request)을 포함합니다. Date는 UTC 기준 일자, 값은 공통 매개변수 X-TC-Timestamp를 환산한 UTC 기준 일자와 일치해야 합니다. Service는 제품명, 호출한 제품 도메인 이름과 일치해야 합니다. 예를 들어 CVM입니다. 위 예시 요청의 값은 2018-10-09/cvm/tc3_request입니다.
- HashedCanonicalRequest: 이전 절차에 따라 합치기를 통해 얻은 요청 문자열 해시값. 컴퓨팅 방법은 Lowercase(HexEncode(Hash.SHA256(CanonicalRequest)))입니다.

상기 규칙에 따라 예시 중에서 얻은 서명 대기 문자열은 다음과 같습니다(잘 보이기 위해 \n 줄바꿈 부호는 직접 새 새줄로 바꿈으로 대체됩니다).

```
TC3-HMAC-SHA256
1539084154
2018-10-09/cvm/tc3_request
91c9c192c14460df6c1ffc69e34e6c5e90708de2a6d282cccf957dbf1aa7f3a7
```

### 3. 서명 컴퓨팅
1)파생 서명 키 컴퓨팅, 의사 코드는 다음과 같습니다.

```
SecretKey = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"
SecretDate = HMAC_SHA256("TC3" + SecretKey, Date)
SecretService = HMAC_SHA256(SecretDate, Service)
SecretSigning = HMAC_SHA256(SecretService, "tc3_request")
```

- SecretKey: 기존의 SecretKey입니다.
- Date: Credential의 Date 필드 정보입니다. 위 예시에서 2018-10-09입니다.
- Service: Credential의 Service 필드 정보입니다. 위 예시에서 CVM입니다.

2)서명 컴퓨팅, 의사 코드는 다음과 같습니다.

```
Signature = HexEncode(HMAC_SHA256(SecretSigning, StringToSign))
```

- SecretSigning: 이전 컴퓨팅으로 얻은 파생 서명 키입니다.
- StringToSign: 절차 2에서 컴퓨팅으로 얻은 서명 대기 문자열입니다.

### 4. Authorization 합치기

다음 형식에 따라 Authorization 합치기:

```
Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', '
    'Signature=' + Signature
```

- Algorithm: 서명 방법, TC3-HMAC-SHA256입니다.
- SecretId: 키 쌍의 SecretId입니다.
- CredentialScope: 자격 증명 범위입니다. 위의 내용 참조.
- SignedHeaders: 서명에 포함한 헤더 정보입니다. 위의 내용 참조.
- Signature: 서명 값

상기 규칙에 따라 예시에서 얻은 값은 다음과 같습니다.

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

### 5.서명 예제

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
        // 시간대에 유의하십시오. 그렇지 않으면 오류가 발생할 수 있습니다.
        sdf.setTimeZone(TimeZone.getTimeZone("UTC"));
        String date = sdf.format(new Date(Long.valueOf(timestamp + "000")));

        // ************* 절차 1: 정규 요청 문자열 합치기 *************
        String httpRequestMethod = "GET";
        String canonicalUri = "/";
        String canonicalQueryString = "Limit=10&Offset=0";
        String canonicalHeaders = "content-type:application/x-www-form-urlencoded\n" + "host:" + host + "\n";
        String signedHeaders = "content-type;host";
        String hashedRequestPayload = DigestUtils.sha256Hex("");
        String canonicalRequest = httpRequestMethod + "\n" + canonicalUri + "\n" + canonicalQueryString + "\n"
                + canonicalHeaders + "\n" + signedHeaders + "\n" + hashedRequestPayload;
        System.out.println(canonicalRequest);

        // ************* 절차 2: 서명 대기 문자열 합치기 *************
        String credentialScope = date + "/" + service + "/" + "tc3_request";
        String hashedCanonicalRequest = DigestUtils.sha256Hex(canonicalRequest.getBytes(CHARSET));
        String stringToSign = algorithm + "\n" + timestamp + "\n" + credentialScope + "\n" + hashedCanonicalRequest;
        System.out.println(stringToSign);

        // ************* 절차 3: 서명 컴퓨팅 *************
        byte[] secretDate = sign256(("TC3" + SECRET_KEY).getBytes(CHARSET), date);
        byte[] secretService = sign256(secretDate, service);
        byte[] secretSigning = sign256(secretService, "tc3_request");
        String signature = DatatypeConverter.printHexBinary(sign256(secretSigning, stringToSign)).toLowerCase();
        System.out.println(signature);

        // ************* 절차 4: Authorization 합치기 *************
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

# ************* 절차 1: 정규 요청 문자열 합치기 *************
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

# ************* 절차 2: 서명 대기 문자열 합치기 *************
credential_scope = date + "/" + service + "/" + "tc3_request"
hashed_canonical_request = hashlib.sha256(canonical_request.encode("utf-8")).hexdigest()
string_to_sign = (algorithm + "\n" +
                  str(timestamp) + "\n" +
                  credential_scope + "\n" +
                  hashed_canonical_request)
print(string_to_sign)


# ************* 절차 3: 서명 컴퓨팅 *************
# 컴퓨팅 서명 개요 함수 
def sign(key, msg):
    return hmac.new(key, msg.encode("utf-8"), hashlib.sha256).digest()
secret_date = sign(("TC3" + secret_key).encode("utf-8"), date)
secret_service = sign(secret_date, service)
secret_signing = sign(secret_service, "tc3_request")
signature = hmac.new(secret_signing, string_to_sign.encode("utf-8"), hashlib.sha256).hexdigest()
print(signature)

# ************* 절차 4: Authorization 합치기 *************
authorization = (algorithm + " " +
                 "Credential=" + secret_id + "/" + credential_scope + ", " +
                 "SignedHeaders=" + signed_headers + ", " +
                 "Signature=" + signature)
print(authorization)

# 공통 매개변수를 요청 헤더에 추가합니다.
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

실제 상황에 따라 다음의 서명 실패 오류 코드가 반환될 수 있습니다. 실제 상황에 따라 해결하십시오.

| 오류 코드 | 오류 설명 |
|----------|---------|
| AuthFailure.SignatureExpire | 서명 만료됨 |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않음 |
| AuthFailure.SignatureFailure | 서명 오류 |
| AuthFailure.TokenFailure | token 오류 |
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님) |

