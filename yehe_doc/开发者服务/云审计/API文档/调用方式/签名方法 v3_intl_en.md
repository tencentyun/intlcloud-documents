The signature algorithm v3 (TC3-HMAC-SHA256) is compatible with the previous signature algorithm v1 and more secure, supports larger request packets and POST JSON format, and has a higher performance. You are recommended to use it to calculate signatures.

If you are using the signature algorithm for the first time, you are recommended to use the "signature string generation" feature in [API Explorer](https://console.cloud.tencent.com/api/explorer) and select "API 3.0 signature v3" as the signature version, which can generate a signature for demonstration and verification. Plus, it can also generate SDK code directly. Seven common open-source programming language SDKs are available for TencentCloud API, including [Python](https://github.com/TencentCloud/tencentcloud-sdk-python), [Java](https://github.com/TencentCloud/tencentcloud-sdk-java), [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php), [Go](https://github.com/TencentCloud/tencentcloud-sdk-go), [Node.js](https://github.com/TencentCloud/tencentcloud-sdk-nodejs), [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet), and [C++](https://github.com/TencentCloud/tencentcloud-sdk-cpp).

TencentCloud API authenticates every request, that is, the request must be signed with the security credentials in the designated steps. Each request must contain the signature information in the common request parameters and be sent in the specified way and format.

## Applying for Security Credentials

In this document, the security credential used is a key pair, which consists of a `SecretId` and a `SecretKey`. Each user can have up to two key pairs.

* SecretId: identifies the user that calls an API, which is similar to a username.
* SecretKey: authenticates the user that calls the API, which is similar to a password.
* **You must keep your security credentials private and avoid disclosure; otherwise, your assets may be compromised. If they are disclosed, please disable them as soon as possible.**

You can apply for security credentials as follows:

1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/).
2. Go to the [TencentCloud API Key](https://console.cloud.tencent.com/capi) page.
3. On the [TencentCloud API Key](https://console.cloud.tencent.com/capi) page, click **Create** to create a key pair.

## Signing Process

TencentCloud API supports both GET and POST requests. For the GET method, only the `Content-Type: application/x-www-form-urlencoded` protocol format is supported. For the POST method, `Content-Type: application/json` and `Content-Type: multipart/form-data` are supported. The JSON format is supported by all business APIs, while the multipart format is supported only by specific APIs (in this case, an API cannot be called in JSON format). For more information, please see the specific business API document. You are recommended to use the POST method because the two methods generate the same results, but the GET method only supports request packets below 32 KB in size.

The following describes how to calculate a signature by calling the CVM API to query instances in Guangzhou. This API is chosen because:

1. The CVM API is enabled by default, and this API is often used.
2. It is read-only and does not change the status of existing resources.
3. It covers many types of parameters so that it is easy to show how to use an array that contains data structures.

In the example, common parameters and API parameters that are prone to mistakes are chosen. When you call an API, use parameters based on the actual conditions. The parameters and values in this example are only for reference because the parameters vary by API.

Suppose your `SecretId` and `SecretKey` are `AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE` and `Gu5t9xGARNpq86cd98joQYCN3EXAMPLE`, respectively. If you want to view the status of an unnamed instance in the Guangzhou region and have only one data entry returned, the request may be:

```
curl -X POST https://cvm.tencentcloudapi.com \
-H "Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea809ad7a8c8f7a4507b9bddcbaa8e581f516e8da2f66e2c5a96525168" \
-H "Content-Type: application/json; charset=utf-8" \
-H "Host: cvm.tencentcloudapi.com" \
-H "X-TC-Action: DescribeInstances" \
-H "X-TC-Timestamp: 1551113065" \
-H "X-TC-Version: 2017-03-12" \
-H "X-TC-Region: ap-guangzhou" \
-d '{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}'
```

The following describes the signature calculation process in detail.

### 1. Concatenate the canonical request string

Concatenate the canonical request string (`CanonicalRequest`) in the following pseudo-code format:

```
CanonicalRequest =
    HTTPRequestMethod + '\n' +
    CanonicalURI + '\n' +
    CanonicalQueryString + '\n' +
    CanonicalHeaders + '\n' +
    SignedHeaders + '\n' +
    HashedRequestPayload
```

| Field | Description |
|-|-|
| HTTPRequestMethod | HTTP request method (GET or POST). This example uses `POST`. |
| CanonicalURI | URI parameter. Slash ("/") is used for API 3.0. |
| CanonicalQueryString | Query string in the URL of the originating HTTP request. This is always an empty string "" for POST requests and is the string after the question mark (?) for GET requests such as `Limit=10&Offset=0`. <br/>Note: `CanonicalQueryString` must be URL-encoded as instructed in [RFC 3986](https://tools.ietf.org/html/rfc3986) with the UTF-8 character set. The applicable standard programming language library is recommended. All special characters must be encoded and capitalized. |
| CanonicalHeaders | Header information for signature calculation, including at least `host` and `content-type`. Custom headers can also be added to the signature process to improve the uniqueness and security of the request. <br/>Concatenation rules: <ol><li>Both the key and value of a header should be converted to lowercase with the leading and trailing spaces removed so that they are concatenated in the `key:value\n` format. </li><li>If there are multiple headers, they should be sorted in ASCII ascending order by header key (lowercase). </li></ol>The calculation result in this example is `content-type:application/json; charset=utf-8\nhost:cvm.tencentcloudapi.com\n`. <br/>Note: `content-type` must match the content that is actually sent. In some programming languages, a `charset` value is automatically added even if it is not specified. In this case, the request sent will be different from the one signed, and the sever will return a signature verification failure. |
| SignedHeaders | Header information for signature calculation, indicating the request headers that are involved in the signature process. The request headers must correspond to the headers in `CanonicalHeaders`. `Content-type` and `host` are required headers. <br/>Concatenation rules: <ol><li>Both the key and value of a header should be converted to lowercase. </li><li>If there are multiple headers, they should be sorted in ASCII ascending order by header key (lowercase) and separated by semicolons (;). </li></ol>The value in this example is `content-type;host`. |
| HashedRequestPayload | Hash value of the request payload (i.e., the request body, such as `{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}` in this example). The pseudo-code for calculation is `Lowercase(HexEncode(Hash.SHA256(RequestPayload)))`, which means that SHA256 hashing is performed on the payload of the HTTP request, then hexadecimal encoding is performed, and finally the encoded string is converted to lowercase letters. For GET requests, `RequestPayload` is always an empty string. The calculation result in this example is `35e9c5b0e3ae67532d3c9f17ead6c90222632e5b1ff7f6e89887f1398934f064`. |

According to the rules above, the canonical request string obtained in the example is as follows:

```
POST
/

content-type:application/json; charset=utf-8
host:cvm.tencentcloudapi.com

content-type;host
35e9c5b0e3ae67532d3c9f17ead6c90222632e5b1ff7f6e89887f1398934f064
```

### 2. Concatenate the string to sign

Concatenate the string to sign in the following format:

```
StringToSign =
    Algorithm + \n +
    RequestTimestamp + \n +
    CredentialScope + \n +
    HashedCanonicalRequest
```

| Field | Description |
|-|-|
| Algorithm | Signature algorithm, which is always `TC3-HMAC-SHA256` currently. |
| RequestTimestamp | Request timestamp, i.e., the value of the common parameter `X-TC-Timestamp` in the request header. It is the UNIX timestamp of the current time in seconds, such as `1551113065` in this example. |
| CredentialScope | Scope of the credential in the format of `Date/service/tc3_request`, including the date, requested service, and termination string (tc3_request). **`Date` indicates a UTC date, which should match the UTC date converted by the common parameter `X-TC-Timestamp`.** `service` is the product name, which should match the domain name of the product called. The calculation result in this example is `2019-02-25/cvm/tc3_request`. |
| HashedCanonicalRequest | Hash value of the canonical request string concatenated in the steps above. The pseudo-code for calculation is `Lowercase(HexEncode(Hash.SHA256(CanonicalRequest)))`. The calculation result in this example is `5ffe6a04c0664d6b969fab9a13bdab201d63ee709638e2749d62a09ca18d7031`. |

Note:

> 1. Date must be calculated from the timestamp `X-TC-Timestamp` and the time zone is UTC+0. If you add the local time zone information (such as UTC+8) in the system, calls can succeed both day and night but will definitely fail at 00:00. For example, if the timestamp is 1551113065 and the time in UTC+8 is 2019-02-26 00:44:25, the UTC+0 date in the calculated Date value should be 2019-02-25 instead of 2019-02-26.
> 2. Timestamp must be the same as your current system time, and your system time must be in sync with the UTC time. If the difference between the timestamp and your current system time is greater than five minutes, the request will fail. If your system time is out of sync with the UTC time for some time, the request will fail and a signature expiration error will be returned.

According to the rules above, the string to sign obtained in the example is as follows:

```
TC3-HMAC-SHA256
1551113065
2019-02-25/cvm/tc3_request
5ffe6a04c0664d6b969fab9a13bdab201d63ee709638e2749d62a09ca18d7031
```

### 3. Calculate the signature
1) Calculate the derived signature key with the following pseudo-code:

```
SecretKey = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"
SecretDate = HMAC_SHA256("TC3" + SecretKey, Date)
SecretService = HMAC_SHA256(SecretDate, Service)
SecretSigning = HMAC_SHA256(SecretService, "tc3_request")
```

The derived key `SecretDate`,` SecretService`, and `SecretSigning` are binary data and may contain non-printable characters. Intermediate results are not displayed here.

Please note that the order of the parameters in the HMAC library functions may vary by programming language. In the pseudo code here, key parameters are at the second half, and the actual requirement of the used programming language shall prevail. Generally, standard library functions will provide calculated values in binary format, which is also used here. They will also provide print-friendly calculated values in hexadecimal format, which will be used in calculating the signature result below.

| Field | Description |
|-|-|
| SecretKey | Original `SecretKey`, i.e., `Gu5t9xGARNpq86cd98joQYCN3EXAMPLE`. |
| Date | Value of the `Date` field in `Credential`, such as `2019-02-25` in this example. |
| Service | Value of the `Service` field in `Credential`, such as `cvm` in this example. |

2) Calculate the signature with the following pseudo-code:

```
Signature = HexEncode(HMAC_SHA256(SecretSigning, StringToSign))
```

The calculation result in this example is `72e494ea809ad7a8c8f7a4507b9bddcbaa8e581f516e8da2f66e2c5a96525168`.

### 4. Concatenate the Authorization string

Concatenate the `Authorization` string in the following format:

```
Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', ' +
    'Signature=' + Signature
```

| Field | Description |
|-|-|
| Algorithm | Signature algorithm, which is always `TC3-HMAC-SHA256`. |
| SecretId | `SecretId` in the key pair, i.e., `AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE`. |
| CredentialScope | Credential scope (see above). The calculation result in this example is `2019-02-25/cvm/tc3_request`. |
| SignedHeaders | Header information for signature calculation (see above), such as `content-type;host` in this example. |
| Signature | Signature value. The calculation result in this example is `72e494ea809ad7a8c8f7a4507b9bddcbaa8e581f516e8da2f66e2c5a96525168`. |

According to the rules above, the values obtained in this example are:

```
TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea809ad7a8c8f7a4507b9bddcbaa8e581f516e8da2f66e2c5a96525168
```

The complete call information is as follows:

```
POST https://cvm.tencentcloudapi.com/
Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea809ad7a8c8f7a4507b9bddcbaa8e581f516e8da2f66e2c5a96525168
Content-Type: application/json; charset=utf-8
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1551113065
X-TC-Region: ap-guangzhou

{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}
```

### 5. Signature demo

#### Java

```
import java.nio.charset.Charset;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.TimeZone;
import java.util.TreeMap;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import javax.xml.bind.DatatypeConverter;

public class TencentCloudAPITC3Demo {
    private final static Charset UTF8 = StandardCharsets.UTF_8;
    private final static String SECRET_ID = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE";
    private final static String SECRET_KEY = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE";
    private final static String CT_JSON = "application/json; charset=utf-8";

    public static byte[] hmac256(byte[] key, String msg) throws Exception {
        Mac mac = Mac.getInstance("HmacSHA256");
        SecretKeySpec secretKeySpec = new SecretKeySpec(key, mac.getAlgorithm());
        mac.init(secretKeySpec);
        return mac.doFinal(msg.getBytes(UTF8));
    }

    public static String sha256Hex(String s) throws Exception {
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        byte[] d = md.digest(s.getBytes(UTF8));
        return DatatypeConverter.printHexBinary(d).toLowerCase();
    }

    public static void main(String[] args) throws Exception {
        String service = "cvm";
        String host = "cvm.tencentcloudapi.com";
        String region = "ap-guangzhou";
        String action = "DescribeInstances";
        String version = "2017-03-12";
        String algorithm = "TC3-HMAC-SHA256";
        String timestamp = "1551113065";
        //String timestamp = String.valueOf(System.currentTimeMillis() / 1000);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        // Make sure that the time zone is correct
        sdf.setTimeZone(TimeZone.getTimeZone("UTC"));
        String date = sdf.format(new Date(Long.valueOf(timestamp + "000")));

        // ************* Step 1. Concatenate the canonical request string *************
        String httpRequestMethod = "POST";
        String canonicalUri = "/";
        String canonicalQueryString = "";
        String canonicalHeaders = "content-type:application/json; charset=utf-8\n" + "host:" + host + "\n";
        String signedHeaders = "content-type;host";

        String payload = "{\"Limit\": 1, \"Filters\": [{\"Values\": [\"\\u672a\\u547d\\u540d\"], \"Name\": \"instance-name\"}]}";
        String hashedRequestPayload = sha256Hex(payload);
        String canonicalRequest = httpRequestMethod + "\n" + canonicalUri + "\n" + canonicalQueryString + "\n"
                + canonicalHeaders + "\n" + signedHeaders + "\n" + hashedRequestPayload;
        System.out.println(canonicalRequest);

        // ************* Step 2. Concatenate the string to sign *************
        String credentialScope = date + "/" + service + "/" + "tc3_request";
        String hashedCanonicalRequest = sha256Hex(canonicalRequest);
        String stringToSign = algorithm + "\n" + timestamp + "\n" + credentialScope + "\n" + hashedCanonicalRequest;
        System.out.println(stringToSign);

        // ************* Step 3. Calculate the signature *************
        byte[] secretDate = hmac256(("TC3" + SECRET_KEY).getBytes(UTF8), date);
        byte[] secretService = hmac256(secretDate, service);
        byte[] secretSigning = hmac256(secretService, "tc3_request");
        String signature = DatatypeConverter.printHexBinary(hmac256(secretSigning, stringToSign)).toLowerCase();
        System.out.println(signature);

        // ************* Step 4. Concatenate the `Authorization` string *************
        String authorization = algorithm + " " + "Credential=" + SECRET_ID + "/" + credentialScope + ", "
                + "SignedHeaders=" + signedHeaders + ", " + "Signature=" + signature;
        System.out.println(authorization);

        TreeMap<String, String> headers = new TreeMap<String, String>();
        headers.put("Authorization", authorization);
        headers.put("Content-Type", CT_JSON);
        headers.put("Host", host);
        headers.put("X-TC-Action", action);
        headers.put("X-TC-Timestamp", timestamp);
        headers.put("X-TC-Version", version);
        headers.put("X-TC-Region", region);

        StringBuilder sb = new StringBuilder();
        sb.append("curl -X POST https://").append(host)
        .append(" -H \"Authorization: ").append(authorization).append("\"")
        .append(" -H \"Content-Type: application/json; charset=utf-8\"")
        .append(" -H \"Host: ").append(host).append("\"")
        .append(" -H \"X-TC-Action: ").append(action).append("\"")
        .append(" -H \"X-TC-Timestamp: ").append(timestamp).append("\"")
        .append(" -H \"X-TC-Version: ").append(version).append("\"")
        .append(" -H \"X-TC-Region: ").append(region).append("\"")
        .append(" -d '").append(payload).append("'");
        System.out.println(sb.toString());
    }
}
```

#### Python

```
# -*- coding: utf-8 -*-
import hashlib, hmac, json, os, sys, time
from datetime import datetime

# Key parameters
secret_id = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"
secret_key = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"

service = "cvm"
host = "cvm.tencentcloudapi.com"
endpoint = "https://" + host
region = "ap-guangzhou"
action = "DescribeInstances"
version = "2017-03-12"
algorithm = "TC3-HMAC-SHA256"
#timestamp = int(time.time())
timestamp = 1551113065
date = datetime.utcfromtimestamp(timestamp).strftime("%Y-%m-%d")
params = {"Limit": 1, "Filters": [{"Name": "instance-name", "Values": [u"unnamed"]}]}

# ************* Step 1. Concatenate the canonical request string *************
http_request_method = "POST"
canonical_uri = "/"
canonical_querystring = ""
ct = "application/json; charset=utf-8"
payload = json.dumps(params)
canonical_headers = "content-type:%s\nhost:%s\n" % (ct, host)
signed_headers = "content-type;host"
hashed_request_payload = hashlib.sha256(payload.encode("utf-8")).hexdigest()
canonical_request = (http_request_method + "\n" +
                     canonical_uri + "\n" +
                     canonical_querystring + "\n" +
                     canonical_headers + "\n" +
                     signed_headers + "\n" +
                     hashed_request_payload)
print(canonical_request)

# ************* Step 2. Concatenate the string to sign *************
credential_scope = date + "/" + service + "/" + "tc3_request"
hashed_canonical_request = hashlib.sha256(canonical_request.encode("utf-8")).hexdigest()
string_to_sign = (algorithm + "\n" +
                  str(timestamp) + "\n" +
                  credential_scope + "\n" +
                  hashed_canonical_request)
print(string_to_sign)


# ************* Step 3. Calculate the signature *************
# Function for calculating signature digest
def sign(key, msg):
    return hmac.new(key, msg.encode("utf-8"), hashlib.sha256).digest()
secret_date = sign(("TC3" + secret_key).encode("utf-8"), date)
secret_service = sign(secret_date, service)
secret_signing = sign(secret_service, "tc3_request")
signature = hmac.new(secret_signing, string_to_sign.encode("utf-8"), hashlib.sha256).hexdigest()
print(signature)

# ************* Step 4. Concatenate the `Authorization` string *************
authorization = (algorithm + " " +
                 "Credential=" + secret_id + "/" + credential_scope + ", " +
                 "SignedHeaders=" + signed_headers + ", " +
                 "Signature=" + signature)
print(authorization)

print('curl -X POST ' + endpoint
      + ' -H "Authorization: ' + authorization + '"'
      + ' -H "Content-Type: application/json; charset=utf-8"'
      + ' -H "Host: ' + host + '"'
      + ' -H "X-TC-Action: ' + action + '"'
      + ' -H "X-TC-Timestamp: ' + str(timestamp) + '"'
      + ' -H "X-TC-Version: ' + version + '"'
      + ' -H "X-TC-Region: ' + region + '"'
      + " -d '" + payload + "'")
```

#### Go

```
package main

import (
    "crypto/hmac"
    "crypto/sha256"
    "encoding/hex"
    "fmt"
    "time"
)

func sha256hex(s string) string {
    b := sha256.Sum256([]byte(s))
    return hex.EncodeToString(b[:])
}

func hmacsha256(s, key string) string {
    hashed := hmac.New(sha256.New, []byte(key))
    hashed.Write([]byte(s))
    return string(hashed.Sum(nil))
}

func main() {
    secretId := "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"
    secretKey := "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"
    host := "cvm.tencentcloudapi.com"
    algorithm := "TC3-HMAC-SHA256"
    service := "cvm"
    version := "2017-03-12"
    action := "DescribeInstances"
    region := "ap-guangzhou"
    //var timestamp int64 = time.Now().Unix()
    var timestamp int64 = 1551113065

    // step 1: build canonical request string
    httpRequestMethod := "POST"
    canonicalURI := "/"
    canonicalQueryString := ""
    canonicalHeaders := "content-type:application/json; charset=utf-8\n" + "host:" + host + "\n"
    signedHeaders := "content-type;host"
    payload := `{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}`
    hashedRequestPayload := sha256hex(payload)
    canonicalRequest := fmt.Sprintf("%s\n%s\n%s\n%s\n%s\n%s",
        httpRequestMethod,
        canonicalURI,
        canonicalQueryString,
        canonicalHeaders,
        signedHeaders,
        hashedRequestPayload)
    fmt.Println(canonicalRequest)

    // step 2: build string to sign
    date := time.Unix(timestamp, 0).UTC().Format("2006-01-02")
    credentialScope := fmt.Sprintf("%s/%s/tc3_request", date, service)
    hashedCanonicalRequest := sha256hex(canonicalRequest)
    string2sign := fmt.Sprintf("%s\n%d\n%s\n%s",
        algorithm,
        timestamp,
        credentialScope,
        hashedCanonicalRequest)
    fmt.Println(string2sign)

    // step 3: sign string
    secretDate := hmacsha256(date, "TC3"+secretKey)
    secretService := hmacsha256(service, secretDate)
    secretSigning := hmacsha256("tc3_request", secretService)
    signature := hex.EncodeToString([]byte(hmacsha256(string2sign, secretSigning)))
    fmt.Println(signature)

    // step 4: build authorization
    authorization := fmt.Sprintf("%s Credential=%s/%s, SignedHeaders=%s, Signature=%s",
        algorithm,
        secretId,
        credentialScope,
        signedHeaders,
        signature)
    fmt.Println(authorization)

    curl := fmt.Sprintf(`curl -X POST https://%s\
 -H "Authorization: %s"\
 -H "Content-Type: application/json; charset=utf-8"\
 -H "Host: %s" -H "X-TC-Action: %s"\
 -H "X-TC-Timestamp: %d"\
 -H "X-TC-Version: %s"\
 -H "X-TC-Region: %s"\
 -d '%s'`, host, authorization, host, action, timestamp, version, region, payload)
    fmt.Println(curl)
}
```

#### PHP

```
<?php
$secretId = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE";
$secretKey = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE";
$host = "cvm.tencentcloudapi.com";
$service = "cvm";
$version = "2017-03-12";
$action = "DescribeInstances";
$region = "ap-guangzhou";
// $timestamp = time();
$timestamp = 1551113065;
$algorithm = "TC3-HMAC-SHA256";

// step 1: build canonical request string
$httpRequestMethod = "POST";
$canonicalUri = "/";
$canonicalQueryString = "";
$canonicalHeaders = "content-type:application/json; charset=utf-8\n"."host:".$host."\n";
$signedHeaders = "content-type;host";
$payload = '{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}';
$hashedRequestPayload = hash("SHA256", $payload);
$canonicalRequest = $httpRequestMethod."\n"
    .$canonicalUri."\n"
    .$canonicalQueryString."\n"
    .$canonicalHeaders."\n"
    .$signedHeaders."\n"
    .$hashedRequestPayload;
echo $canonicalRequest.PHP_EOL;

// step 2: build string to sign
$date = gmdate("Y-m-d", $timestamp);
$credentialScope = $date."/".$service."/tc3_request";
$hashedCanonicalRequest = hash("SHA256", $canonicalRequest);
$stringToSign = $algorithm."\n"
    .$timestamp."\n"
    .$credentialScope."\n"
    .$hashedCanonicalRequest;
echo $stringToSign.PHP_EOL;

// step 3: sign string
$secretDate = hash_hmac("SHA256", $date, "TC3".$secretKey, true);
$secretService = hash_hmac("SHA256", $service, $secretDate, true);
$secretSigning = hash_hmac("SHA256", "tc3_request", $secretService, true);
$signature = hash_hmac("SHA256", $stringToSign, $secretSigning);
echo $signature.PHP_EOL;

// step 4: build authorization
$authorization = $algorithm
    ." Credential=".$secretId."/".$credentialScope
    .", SignedHeaders=content-type;host, Signature=".$signature;
echo $authorization.PHP_EOL;

$curl = "curl -X POST https://".$host
    .' -H "Authorization: '.$authorization.'"'
    .' -H "Content-Type: application/json; charset=utf-8"'
    .' -H "Host: '.$host.'"'
    .' -H "X-TC-Action: '.$action.'"'
    .' -H "X-TC-Timestamp: '.$timestamp.'"'
    .' -H "X-TC-Version: '.$version.'"'
    .' -H "X-TC-Region: '.$region.'"'
    ." -d '".$payload."'";
echo $curl.PHP_EOL;
```


## Signature Failure

The following error codes may be returned for signature failure. Please sesolve the errors accordingly.

| Error Code | Error Description |
|----------|---------|
| AuthFailure.SignatureExpire | The signature expired. The difference between the `Timestamp` and the server time cannot be greater than five minutes. |
| AuthFailure.SecretIdNotFound | The key does not exist. Log in to the console and check whether it is disabled or you copied fewer or more characters. |
| AuthFailure.SignatureFailure | Signature error. It is possible that the signature is calculated incorrectly, the signature does not match the content that is actually sent, or the `SecretKey` is incorrect. |
| AuthFailure.TokenFailure | Temporary credential token error. |
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |

