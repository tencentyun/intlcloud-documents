Tencent Cloud API authenticates each access request, so each request is required to include the Signature in the common request parameters for user identity authentication.
The signature is generated with user's security credentials, which consist of a SecretId and a SecretKey. If you don't have security credentials, apply for the credentials on the [Cloud API Key](https://console.cloud.tencent.com/capi) page. Otherwise, you will not be able to call the cloud APIs.

## Applying for Security Credentials
Before using cloud APIs for the first time, you need to apply for security credentials on the [Cloud API Key](https://console.cloud.tencent.com/capi) page.
Security credentials consist of a SecretId and a SecretKey, where:
* The SecretId is used to identify the API caller.
* SecretKey is a key used for signature string encryption, and signature string verification by the server.
* <font color='red'>The security credentials must be kept confidential to avoid leakage.</font>

Apply for security credentials by following the steps below:

1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/).
1. Go to the [Cloud API Key](https://console.cloud.tencent.com/capi) console page.
1. On the [Cloud API Key](https://console.cloud.tencent.com/capi) page, click **New** to create a pair of SecretId/SecretKey.

Note: A developer account can have two pairs of SecretId/SecretKey at most.

## TC3-HMAC-SHA256 Signature Method

Note: For the GET method, only the Content-Type: application/x-www-form-urlencoded protocol format is supported. For the POST method, two protocol formats, Content-Type: application/json and Content-Type: multipart/form-data, are supported. The JSON format is supported by default for all business APIs, and the multipart format is supported only for specific business APIs. In this case, the API cannot be called in JSON format. See the specific business API documentation for more information.

The following shows how to compute signature by using CVM to query the instance list in Guangzhou zone. Only two parameters of "Query Instance List": Limit and Offset are used via the GET method.

For example, your SecretId and SecretKey are AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE and Gu5t9xGARNpq86cd98joQYCN3EXAMPLE.

### 1. Splice specification request string

Splice specification request string (CanonicalRequest) in the following format:

```
CanonicalRequest =
    HTTPRequestMethod + '\n' +
    CanonicalURI + '\n' +
    CanonicalQueryString + '\n' +
    CanonicalHeaders + '\n' +
    SignedHeaders + '\n' +
    HashedRequestPayload
```

- HTTPRequestMethod: HTTP request method (GET and POST). GET is used in this example.
- CanonicalURI: URI parameter. Slash ("/") is used for API 3.0;
- CanonicalQueryString: query string for HTTP request URL, which is always an empty string for the POST request and a string after the question mark ("?") in URL for the GET request. Limit=10&Offset=0 is used in this example. Note: CanonicalQueryString must be URL encoded.
- CanonicalHeaders: header information for signature, including at least the host and content-type headers. Custom header for signature can also be added to improve the uniqueness and security of the request. Splicing rules: 1) The key and value headers are converted to lowercase, and the spaces at the start and end are removed. Splice​in the format of key:value\n. 2) Multiple headers are spliced in the lexicographic order of the header key (lowercase). `content-type:application/x-www-form-urlencoded\nhost:cvm.tencentcloudapi.com\n` is used in this example.
- SignedHeaders: header information for signature. It specifies the headers for signature in the request, which correspond to the header content contained in CanonicalHeaders. The content-type and host headers are required. Splicing rules: 1) The header key is converted to lowercase. 2) Multiple header keys are spliced in the lexicographic order of the header key (lowercase) and separated by semicolons (";"). `content-type;host` is used in this example.
- HashedRequestPayload: hash value of the request body, which is computed by Lowercase(HexEncode(Hash.SHA256(RequestPayload))). After computing the SHA256 hash on the entire body payload of the HTTP request, it is encoded in hexadecimal format, and then the encoded string is converted into lowercase. Note: For GET requests, RequestPayload must be an empty string. For POST requests, RequestPayload is the body payload of the HTTP request.

Based on the above rules, the specification request string obtained in the example is as follows (For clarity, "\n" is removed by starting a new line.):
```
GET
/
Limit=10&Offset=0
content-type:application/x-www-form-urlencoded
host:cvm.api.tencentyun.com

content-type;host
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

### 2. Splice string to be signed

Splice string to be signed in the following formats:

```
StringToSign =
    Algorithm + \n +
    RequestTimestamp + \n +
    CredentialScope + \n +
    HashedCanonicalRequest
```

- Algorithm: signature algorithm, which is always TC3-HMAC-SHA256;
- RequestTimestamp: request timestamp, which is the X-TC-Timestamp value of the request header, such as 1539084154 in the above example;
- CredentialScope: credential scope in the format of Date/service/tc3_request, including date, requested service and terminated string (tc3_request). Date is UTC date, which must be consistent with the UTC date converted by the X-TC-Timestamp common parameter; service is the product name, which must be consistent with the called product domain name, such as CVM. 2018-10-09/cvm/tc3_request is used in the above example.
- HashedCanonicalRequest: hash value of the specification request string spliced in the above step. The computing method is Lowercase(HexEncode(Hash.SHA256(CanonicalRequest))).

Based on the above rules, the string to be signed in the example is as follows (For clarity, "\n" is removed by starting a new line.):

```
TC3-HMAC-SHA256
1539084154
2018-10-09/cvm/tc3_request
91c9c192c14460df6c1ffc69e34e6c5e90708de2a6d282cccf957dbf1aa7f3a7
```

### 3. Compute signature
1) Compute the derived signature key. Its pseudo code is as follows:

```
SecretKey = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"
SecretDate = HMAC_SHA256("TC3" + SecretKey, Date)
SecretService = HMAC_SHA256(SecretDate, Service)
SecretSigning = HMAC_SHA256(SecretService, "tc3_request")
```

- SecretKey: Original SecretKey;
- Date: Value in the Date field in Credential, such as 2018-10-09 in the above example;
- Service: Value in the Service field in Credential, such as CVM in the above example;

2) Compute the signature. Its pseudo code is as follows:

```
Signature = HexEncode(HMAC_SHA256(SecretSigning, StringToSign))
```

- SecretSigning: Derived signature key obtained by computing;
- StringToSign: String to be signed in Step 2;

### 4. Splice Authorization

Splice Authorization in the following formats:

```
Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', '
    'Signature=' + Signature
```

- Algorithm: signature method, which is always TC3-HMAC-SHA256;
- SecretId: SecretId in the key pair;
- CredentialScope: credential scope. See above for more information;
- SignedHeaders: header information for signature. See above for more information;
- Signature: signature value

Based on the above rules, the value in the example is:

```
TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
```

The complete calling is as follows:

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

### 5. Signature demonstration

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
        //Mind the time zone. Otherwise an error may occur.
        sdf.setTimeZone(TimeZone.getTimeZone("UTC"));
        String date = sdf.format(new Date(Long.valueOf(timestamp + "000")));

        // ************* Step 1: Splice the specification request string*************
        String httpRequestMethod = "GET";
        String canonicalUri = "/";
        String canonicalQueryString = "Limit=10&Offset=0";
        String canonicalHeaders = "content-type:application/x-www-form-urlencoded\n" + "host:" + host + "\n";
        String signedHeaders = "content-type;host";
        String hashedRequestPayload = DigestUtils.sha256Hex("");
        String canonicalRequest = httpRequestMethod + "\n" + canonicalUri + "\n" + canonicalQueryString + "\n"
                + canonicalHeaders + "\n" + signedHeaders + "\n" + hashedRequestPayload;
        System.out.println(canonicalRequest);

        // ************* Step 2: Splice the string to be signed*************
        String credentialScope = date + "/" + service + "/" + "tc3_request";
        String hashedCanonicalRequest = DigestUtils.sha256Hex(canonicalRequest.getBytes(CHARSET));
        String stringToSign = algorithm + "\n" + timestamp + "\n" + credentialScope + "\n" + hashedCanonicalRequest;
        System.out.println(stringToSign);

        // ************* Step 3: Compute signature*************
        byte[] secretDate = sign256(("TC3" + SECRET_KEY).getBytes(CHARSET), date);
        byte[] secretService = sign256(secretDate, service);
        byte[] secretSigning = sign256(secretService, "tc3_request");
        String signature = DatatypeConverter.printHexBinary(sign256(secretSigning, stringToSign)).toLowerCase();
        System.out.println(signature);

        // ************* Step 4: Splice Authorization *************
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

# Key parameter
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

# ************* Step 1: Splice the specification request string*************
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

# ************* Step 2: Splice the string to be signed*************
credential_scope = date + "/" + service + "/" + "tc3_request"
hashed_canonical_request = hashlib.sha256(canonical_request.encode("utf-8")).hexdigest()
string_to_sign = (algorithm + "\n" +
                  str(timestamp) + "\n" +
                  credential_scope + "\n" +
                  hashed_canonical_request)
print(string_to_sign)


# ************* Step 3: Compute signature*************
# Function for computing signature digest
def sign(key, msg):
    return hmac.new(key, msg.encode("utf-8"), hashlib.sha256).digest()
secret_date = sign(("TC3" + secret_key).encode("utf-8"), date)
secret_service = sign(secret_date, service)
secret_signing = sign(secret_service, "tc3_request")
signature = hmac.new(secret_signing, string_to_sign.encode("utf-8"), hashlib.sha256).hexdigest()
print(signature)

# ************* Step 4: Splice Authorization *************
authorization = (algorithm + " " +
                 "Credential=" + secret_id + "/" + credential_scope + ", " +
                 "SignedHeaders=" + signed_headers + ", " +
                 "Signature=" + signature)
print(authorization)

# Common parameters are added to the request string.
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


## Signature Failure

The following signature error codes may be returned depending on the actual situation.

| Error Code | Description |
|----------|---------|
| AuthFailure.SignatureExpire | Signature expired |
| AuthFailure.SecretIdNotFound | Key does not exist |
| AuthFailure.SignatureFailure | Invalid signature |
| AuthFailure.TokenFailure | Invalid token |
| AuthFailure.InvalidSecretId | Invalid key (it is not a cloud API key) |

