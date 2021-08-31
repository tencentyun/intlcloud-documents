TencentCloud API has been upgraded to v3.0. This version is optimized for performance and deployed in all regions. It supports nearby access and access by region for significantly reduced access latency. In addition, it features more detailed API descriptions and error codes and API-level comments for SDKs, enabling you to use Tencent Cloud services more conveniently and quickly. This document describes how to call APIs for Java.
This version currently supports various [Tencent Cloud services](https://intl.cloud.tencent.com/product) such as CVM, CBS, VPC, and TencentDB and will support more services in the future. 





## Request Structure

#### 1. Service address (endpoint)

TencentCloud API supports access from either a nearby region (such as `cvm.tencentcloudapi.com` for CVM) or a specified region (such as `cvm.ap-guangzhou.tencentcloudapi.com` for CVM in the Guangzhou region). For values of the region parameter, please see the region list in the "Common Parameters" section below. To check whether a region is supported by a specific Tencent Cloud service, please see its "Request Structure" document.

>!For latency-sensitive businesses, we recommend you specify a domain name with a region.

#### 2. Communications protocol

 All TencentCloud APIs communicate over HTTPS, providing highly secure communications tunnels. 

#### 3. Request method

Supported HTTP request methods:

- POST (recommended)
- GET

`Content-Type` types supported by POST request:

- application/json (recommended). The signature algorithm v3 (TC3-HMAC-SHA256) must be used.
- application/x-www-form-urlencoded. The signature algorithm v1 (HmacSHA1 or HmacSHA256) must be used.
- multipart/form-data (only supported by certain APIs). The signature algorithm v3 (TC3-HMAC-SHA256) must be used.

The size of a GET request packet cannot exceed 32 KB. The size of a POST request cannot exceed 1 MB for the signature algorithm v1 (HmacSHA1 or HmacSHA256) or 10 MB for the signature algorithm v3 (TC3-HMAC-SHA256).

#### 4. Character encoding

<kbd>UTF-8</kbd> encoding is always used.



## Common Parameters

The common parameters are used to identity the user and API signature. They should be carried by each request to initiate properly. 

### Signature algorithm v3

The signature algorithm v3 (sometimes referred to as "TC3-HMAC-SHA256") is more secure than the signature algorithm v1 (referred to as signature algorithm in certain documents), supports larger request packets and POST JSON format, and has a higher performance. We recommend you use it to calculate signatures. For more information on how to use it, please see below. 

| Parameter Name | Type | Required | Description |
| :------------- | :------ | :--- | :----------------------------------------------------------- |
| X-TC-Action | String | Yes | Name of the API for the desired operation. For the specific value, please see the description of common parameter `Action` in the input parameters in the related API document. For example, the API for querying CVM instance list is `DescribeInstances`. |
| X-TC-Region | String | - | Region parameter, which is used to identify the region where the data you want to manipulate resides. For values supported for an API, please see the description of common parameter `Region` in the input parameters in related API documentation. **Note: this parameter is not required for some APIs (which will be indicated in related API documentation) and will not take effect even if it is passed.** |
| X-TC-Timestamp | Integer | Yes | The current UNIX timestamp that records the time when the API request was initiated, such as 1529223702. **Note: if the difference between the UNIX timestamp and the server time is greater than 5 minutes, a signature expiration error may occur.** |
| X-TC-Version | String | Yes | Version of the API for the desired operation, such as 2017-03-12 for CVM. For the specific value, please see the description of common parameter `Version` in the input parameters in related API documentation. |
| Authorization | String | Yes | HTTP authentication request header, such as TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea8******************************************a96525168 <br>Here, <li>TC3-HMAC-SHA256: signature algorithm, currently fixed as this value. </li><li>Credential: signature credential. `AKIDEXAMPLE` indicates the `SecretId`. </li><li>`Date` indicates a UTC date which must match the value of `X-TC-Timestamp` (a common parameter) in UTC format. </li><li>`service` indicates the name of the service and is generally a domain name prefix; for example, the domain name `cvm.tencentcloudapi.com` means the CVM service, and the value for this service is `cvm`. </li><li>SignedHeaders: the headers that contain the authentication information. `content-type` and `host` are required. </li><li>Signature: signature digest. For the calculation process, please see below. </li> |
| X-TC-Token | String | No | Token used for temporary credentials. It must be used with a temporary key. You can get the temporary key and token by calling a CAM API. No token is required for a long-term key. |

### Signature algorithm v1

When the signature algorithm v1 (sometimes referred to as "HmacSHA256" or "HmacSHA1") is used, the common parameters should be uniformly placed in the request string.

| Parameter Name | Type | Required | Description |
| :-------------- | :------ | :--- | :----------------------------------------------------------- |
| Action | String | Yes | Name of the API for the desired operation. For the specific value, please see the description of common parameter `Action` in the input parameters in the related API document. For example, the API for querying CVM instance list is `DescribeInstances`. |
| Region| String | - | Region parameter, which is used to identify the region where the data you want to manipulate resides. For values supported for an API, please see the description of common parameter `Region` in the input parameters in related API documentation. **Note: this parameter is not required for some APIs (which will be indicated in related API documentation) and will not take effect even if it is passed.** |
| Timestamp | Integer | Yes | The current UNIX timestamp that records the time when the API request was initiated, such as 1529223702. If the difference between the UNIX timestamp and the current time is too large, a signature expiration error may occur. |
| Nonce | Integer | Yes | A random positive integer used in conjunction with `Timestamp` to prevent replay attacks. |
| SecretId | String | Yes | The identifying `SecretId` obtained on the [TencentCloud API Key](https://console.cloud.tencent.com/capi) page. A `SecretId` corresponds to a unique `SecretKey` which is used to generate the request signature (`Signature`). |
| Signature | String | Yes | Request signature, which is used to verify the validity of the request. It is generated based on input parameters. For more information on how to calculate the signature, please see below. |
| Version | String | Yes | Version of the API for the desired operation, such as 2017-03-12 for CVM. For the specific value, please see the description of common parameter `Version` in the input parameters in related API documentation. |
| SignatureMethod | String | No | Signature algorithm. Currently, only HmacSHA256 and HmacSHA1 are supported. The HmacSHA256 algorithm is used to verify the signature only when this parameter is specified as HmacSHA256. In other cases, the signature is verified with HmacSHA1. |
| Token | String | No | Token used for temporary credentials. It must be used with a temporary key. You can get the temporary key and token by calling a CAM API. No token is required for a long-term key. |

### Region list


As the supported regions vary by service, please refer to the region list in each service's product documentation for specific details.
For example, you can see the [region list](https://intl.cloud.tencent.com/document/product/213/31574) of CVM.




## API Call Method for Java

TencentCloud API authenticates every request, that is, the request must be signed with the security credentials in the designated steps. Each request must contain the signature information in the common request parameters and be sent in the specified way and format.

Suppose your `SecretId` and `SecretKey` are `AKIDz8krbsJ5**********mLPx3EXAMPL` and `Gu5t9xGAR***********EXAMPLE`, respectively. If you want to view the status of an unnamed instance in the Guangzhou region and have only one data entry returned, the request may be: 

```
curl -X POST https://cvm.tencentcloudapi.com \
-H "Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5**********mLPx3EXAMPL/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea8******************************************a96525168" \
-H "Content-Type: application/json; charset=utf-8" \
-H "Host: cvm.tencentcloudapi.com" \
-H "X-TC-Action: DescribeInstances" \
-H "X-TC-Timestamp: 1551113065" \
-H "X-TC-Version: 2017-03-12" \
-H "X-TC-Region: ap-guangzhou" \
-d '{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}'
```

### Step 1. Apply for security credentials

In this document, the security credential used is a key pair, which consists of a `SecretId` and a `SecretKey`. Each user can have up to two key pairs.

* SecretId: identifies the user that calls an API, which is similar to a username.
* SecretKey: authenticates the user that calls the API, which is similar to a password.
>! You must keep your security credentials private and avoid disclosure; otherwise, your assets may be compromised. If they are disclosed, please disable them as soon as possible.

Go to the [API key management](https://console.cloud.tencent.com/cam/capi) page to get API keys as shown below:
![](https://main.qcloudimg.com/raw/12b5b846c057addb6ea5eab9010bc42f.png)

### Step 2
### 1. Get an API 3.0 signature v3



The signature algorithm v3 (TC3-HMAC-SHA256) is compatible with the previous signature algorithm v1 and more secure, supports larger request packets and POST JSON format, and has a higher performance. We recommend you use it to calculate signatures.
![](https://main.qcloudimg.com/raw/2bd7aa3a0f840da675a8eb768aa3dc72.png)

>! If you are using the signature algorithm for the first time, we recommend you use the "signature string generation" feature in [API Explorer](https://console.cloud.tencent.com/api/explorer) and select "API 3.0 signature v3" as the signature version, which can generate a signature for demonstration and verification. Plus, it can also generate SDK code directly. Seven common open-source programming language SDKs are available for TencentCloud API, including [Python](https://github.com/TencentCloud/tencentcloud-sdk-python), [Java](https://github.com/TencentCloud/tencentcloud-sdk-java), [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php), [Go](https://github.com/TencentCloud/tencentcloud-sdk-go), [Node.js](https://github.com/TencentCloud/tencentcloud-sdk-nodejs), [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet), and [C++](https://github.com/TencentCloud/tencentcloud-sdk-cpp).



TencentCloud API supports both GET and POST requests. For the GET method, only the `Content-Type: application/x-www-form-urlencoded` protocol format is supported. For the POST method, `Content-Type: application/json` and `Content-Type: multipart/form-data` are supported. The JSON format is supported by all business APIs, while the multipart format is supported only by specific APIs (in this case, an API cannot be called in JSON format). For more information, please see the specific business API document. We recommend you use the POST method because the two methods generate the same results, but the GET method only supports request packets below 32 KB in size.

The following describes how to calculate a signature by calling the [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258) API. This API is chosen because:

1. The CVM API is enabled by default, and this API is often used.
2. It is read-only and does not change the status of existing resources.
3. It covers many types of parameters so that it is easy to show how to use an array that contains data structures.

#### 1. Concatenate the canonical request string

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
| :------------------- | :----------------------------------------------------------- |
| HTTPRequestMethod | HTTP request method (GET or POST). This example uses `POST`. |
| CanonicalURI | URI parameter. Slash ("/") is used for API 3.0. |
| CanonicalQueryString | Query string in the URL of the originating HTTP request. This is always an empty string "" for POST requests and is the string after the question mark (?) for GET requests such as `Limit=10&Offset=0`. Note: `CanonicalQueryString` must be URL-encoded as instructed in [RFC 3986](https://tools.ietf.org/html/rfc3986) with the UTF-8 character set. The applicable standard programming language library is recommended. All special characters must be encoded and capitalized. |
| CanonicalHeaders | Header information for signature calculation, including at least `host` and `content-type`. Custom headers can also be added to the signature process to improve the uniqueness and security of the request. Concatenation rules: both the key and value of a header should be converted to lowercase with the leading and trailing spaces removed so that they are concatenated in the `key:value\n` format. If there are multiple headers, they should be sorted in ASCII ascending order by header key (lowercase). The calculation result in this example is `content-type:application/json; charset=utf-8\nhost:cvm.tencentcloudapi.com\n`. **Note: `content-type` must match the content that is actually sent. In some programming languages, a `charset` value is automatically added even if it is not specified. In this case, the request sent will be different from the one signed, and the sever will return a signature verification failure.** |
| SignedHeaders | Header information for signature calculation, indicating the request headers that are involved in the signature process. The request headers must correspond to the headers in `CanonicalHeaders`. `Content-type` and `host` are required headers. Concatenation rules: both the key and value of a header should be converted to lowercase. If there are multiple headers, they should be sorted in ASCII ascending order by header key (lowercase) and separated by semicolons (;). The value in this example is `content-type;host`. |
| HashedRequestPayload | Hash value of `Requestpayload` (i.e., the request body, such as `{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}` in this example). The pseudo-code for calculation is `Lowercase(HexEncode(Hash.SHA256(RequestPayload)))`, which means that SHA256 hashing is performed on the payload of the HTTP request, then hexadecimal encoding is performed, and finally the encoded string is converted to lowercase letters. For GET requests, `RequestPayload` is always an empty string. The calculation result in this example is `35e9c5b0e3ae67532d3c9f17ead6c90222632e5b1ff7f6e89887f1398934f064`. |

 According to the rules above, the canonical request string obtained in the example is as follows: 

```
POST
/

content-type:application/json; charset=utf-8
host:cvm.tencentcloudapi.com

content-type;host
35e9c5b0e3ae67532d3c9f17ead6c90222632e5b1ff7f6e89887f1398934f064
```

#### 2. Concatenate the string to sign

Concatenate the string to sign in the following format:

```
StringToSign =
    Algorithm + \n +
    RequestTimestamp + \n +
    CredentialScope + \n +
    HashedCanonicalRequest
```

| Field | Description |
| :--------------------- | :----------------------------------------------------------- |
| Algorithm | Signature algorithm, which is always `TC3-HMAC-SHA256` currently. |
| RequestTimestamp | Request timestamp, i.e., the value of the common parameter `X-TC-Timestamp` in the request header. It is the UNIX timestamp of the current time in seconds, such as `1551113065` in this example. |
| CredentialScope | Scope of the credential in the format of `Date/service/tc3_request`, including the date, requested service, and termination string (tc3_request). **`Date` indicates a UTC date, which should match the UTC date converted by the common parameter `X-TC-Timestamp`.** `service` is the service name, which should match the domain name of the service called. The calculation result in this example is `2019-02-25/cvm/tc3_request`. |
| HashedCanonicalRequest | Hash value of the canonical request string concatenated in the steps above. The pseudo-code for calculation is `Lowercase(HexEncode(Hash.SHA256(CanonicalRequest)))`. The calculation result in this example is `5ffe6a04c0664d6b969fab9a13bdab201d63ee709638e2749d62a09ca18d7031`. |

>! 1. `Date` must be calculated from the timestamp `X-TC-Timestamp` and the time zone is UTC+0. If you add the local time zone information (such as UTC+8) in the system, calls can succeed both day and night but will definitely fail at 00:00. For example, if the timestamp is 1551113065 and the time in UTC+8 is 2019-02-26 00:44:25, the UTC+0 date in the calculated `Date` value should be 2019-02-25 instead of 2019-02-26. <br>2. `Timestamp` must be the same as your current system time, and your system time must be in sync with the UTC time. If the difference between the timestamp and your current system time is greater than five minutes, the request will fail. If your system time is out of sync with the UTC time for a prolonged period, the request will fail, and a signature expiration error will be returned.

 According to the rules above, the string to sign obtained in the example is as follows: 

```
TC3-HMAC-SHA256
1551113065
2019-02-25/cvm/tc3_request
5ffe6a04c0664d6b969fab9a13bdab201d63ee709638e2749d62a09ca18d7031
```

#### 3. Calculate the signature (pseudocode)

```java
SecretKey = "Gu5t9xGAR***********EXAMPLE"
byte[] secretDate = hmac256(("TC3" + SecretKey).getBytes(UTF8), date);
byte[] secretService = hmac256(secretDate, service);
byte[] secretSigning = hmac256(secretService, "tc3_request");
String signature = DatatypeConverter.printHexBinary(hmac256(secretSigning, stringToSign)).toLowerCase();
System.out.println(signature);
```

The derived key `SecretDate`,` SecretService`, and `SecretSigning` are binary data and may contain non-printable characters. Intermediate results are not displayed here.

| Field | Description |
| :-------- | :----------------------------------------------------------- |
| SecretKey | Original `SecretKey`, i.e., `Gu5t9xGAR***********EXAMPLE`. |
| date | Value of the `Date` field in `Credential`, such as `2019-02-25` in this example. |
| service | Value of the `Service` field in `Credential`, such as `cvm` in this example. |

The calculation result in this example is `72e494ea8******************************************a96525168`.

#### 4. Concatenate the Authorization string

Concatenate the `Authorization` string in the following format:

```java
String Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', ' +
    'Signature=' + Signature
```

| Field | Description |
| :-------------- | :----------------------------------------------------------- |
| Algorithm | Signature algorithm, which is always `TC3-HMAC-SHA256`. |
| SecretId | `SecretId` in the key pair, i.e., `AKIDz8krbsJ5**********mLPx3EXAMPL`. |
| CredentialScope | Credential scope (see above). The calculation result in this example is `2019-02-25/cvm/tc3_request`. |
| SignedHeaders | Header information for signature calculation (see above), such as `content-type;host` in this example. |
| Signature       | Signature value. The calculation result in this example is `72e494ea8******************************************a96525168`. |

According to the rules above, the values obtained in this example are:

```
TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5**********mLPx3EXAMPL/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea8******************************************a96525168
```

The complete call information is as follows:

```
POST https://cvm.tencentcloudapi.com/
Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5**********mLPx3EXAMPL/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea8******************************************a96525168
Content-Type: application/json; charset=utf-8
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1551113065
X-TC-Region: ap-guangzhou

{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}
```

#### 5. Sample API 3.0 signature v3

```java
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
    private final static String SECRET_ID = "AKIDz8krbsJ5**********mLPx3EXAMPL";
    private final static String SECRET_KEY = "Gu5t9xGAR***********EXAMPLE";
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

###  
### 2. Get an API 3.0 signature v1

The signature algorithm v1 is simple and easy to use, but its functionality and security are not as good as the signature algorithm v3 which is therefore recommended.

>! If you are using the signature algorithm for the first time, we recommend you use the "signature string generation" feature in [API Explorer](https://console.cloud.tencent.com/api/explorer) and select "API 3.0 signature v1" as the signature version, which can generate a signature for demonstration and verification and provides signing examples for certain programming languages. Plus, it can also generate SDK code directly. Seven common open-source programming language SDKs are available for TencentCloud API, including [Python](https://github.com/TencentCloud/tencentcloud-sdk-python), [Java](https://github.com/TencentCloud/tencentcloud-sdk-java), [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php), [Go](https://github.com/TencentCloud/tencentcloud-sdk-go), [Node.js](https://github.com/TencentCloud/tencentcloud-sdk-nodejs), [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet), and [C++](https://github.com/TencentCloud/tencentcloud-sdk-cpp).

For example, if you call the `DescribeInstances` API to query CVM instances, the request parameters may be as follows:

| Parameter Name | Description | Value |
| :------------ | :-------------- | :---------------------------------- |
| Action | Method | DescribeInstances |
| SecretId | Key ID | `AKIDz8krbsJ5**********mLPx3EXAMPL` |
| Timestamp | Current timestamp | 1465185768 |
| Nonce | Random positive integer | 11886 |
| Region | Instance region | ap-guangzhou |
| InstanceIds.0 | ID of the instance to be queried | ins-09dx96dg |
| Offset | Offset | 0 |
| Limit | Allowed maximum number of output entries | 20 |
| Version | API version number | 2017-03-12 |

#### 1. Sort parameters

Sort all the request parameters in an ascending lexicographical order (ASCII code) by their names.
>!
>- The parameters are sorted only by name but not by value.
>- The parameters are sorted based on ASCII code but not in an alphabetical order or by value. For example, `InstanceIds.2` should be arranged behind `InstanceIds.12`. You can complete sorting by using a sorting function in a programming language, such as the `ksort` function in PHP.
>
The parameters in the example are sorted as follows:

```
{
    'Action' : 'DescribeInstances',
    'InstanceIds.0' : 'ins-09dx96dg',
    'Limit' : 20,
    'Nonce' : 11886,  
    'Offset' : 0,
    'Region' : 'ap-guangzhou',
    'SecretId' : 'AKIDz8krbsJ5**********mLPx3EXAMPL',
    'Timestamp' : 1465185768,
    'Version': '2017-03-12',
}
```

 Any other programming languages can be used to sort these parameters as long as the same result is produced. 

#### 2. Concatenate the canonical request string

This step generates a request string. Format the request parameters sorted in the previous step into the form of `parameter=value`. For example, for the `Action` parameter, its parameter is `Action` and its value is `DescribeInstances`; therefore, the parameter will be formatted into `Action=DescribeInstances`.
>!The `value` is the original value instead of the URL-encoded value.

Then, concatenate the formatted parameters with `&`. The generated request string will be as follows:

```
Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5**********mLPx3EXAMPL&Timestamp=1465185768&Version=2017-03-12
```

#### 3. Concatenate the string to sign

This step generates the original signature string. The original signature string consists of the following parameters:

1. Request method: POST and GET methods are supported. GET is used here for the request. Please note that the method name should be in all capital letters.
2. Request server: the domain name of the request for querying instances (DescribeInstances) is `cvm.tencentcloudapi.com`. The actual request domain name varies by the module to which the API belongs. For more information, please see the specific API document.
3. Request path: the request path in the current version of TencentCloud API is fixed to `/`.
4. Request string: the request string generated in the previous step.

The rule for concatenating the original string of the signature is `request method + request server + request path + ? + request string`.

The concatenation result in the example is as follows:

```
GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5**********mLPx3EXAMPL&Timestamp=1465185768&Version=2017-03-12
```

#### 4. Calculate the signature (pseudocode)

This step generates a signature string. Use the HMAC-SHA1 algorithm to sign the **original signature string** obtained in the previous step, and then Base64-encode the generated signature to get the final signature. 

```java
import javax.crypto.Mac;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Base64;
 
/**
 *
 * [Hmac-SHA1 signature algorithm]
 * @String  encryptText [encrypted original string]
 * @String  encryptKey  [encryption key]
 * @return [signature value]
 */
public class HmacSHA1 {
	private static final String MAC_NAME = "HmacSHA1";
	public static final String ENCODING = "UTF-8";
	// Signature algorithm
	public static String HmacSHA1Encrypt(String s,String secret_key ) throws Exception{
        byte[] data = encryptKey.getBytes( ENCODING );
        SecretKey secretKey = new SecretKeySpec( data, MAC_NAME );
        Mac mac = Mac.getInstance( MAC_NAME );
        mac.init( secretKey );
        byte[] text = encryptText.getBytes( ENCODING );
        byte[] digest = mac.doFinal( text );
        return new String(Base64.encodeBase64(digest));
	}
}
String secret_key = "Gu5t9xGAR***********EXAMPLE";
String s = "GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5**********mLPx3EXAMPL&Timestamp=1465185768&Version=2017-03-12";
// Final signature string
String Signature = new HmacSHA1();
System.out.println(Signature)
```

 #### 5. Get the call information and send a request

  ```python
# The API will be called actually, and fees will be incurred if it is a consumption API and the request succeeds (the example here is to send a GET request in Python)
resp = requests.get("https://" + endpoint, params=data)
print(resp.url)
  ```

```
The obtained request string is as follows:
https://cvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5**********mLPx3EXAMPL&Signature=EliP9YW3pW28FpsEdkXt%2F%2BWcGeI%3D&Timestamp=1465185768&Version=2017-03-12
```

| Field | Description |
| :------- | ------------------------------------------------------------ |
| endpoint | Service address, such as `cvm.tencentcloudapi.com`.                   |
| data     | API parameter of the sample API 3.0 signature v1. **Note:** you should add the calculated signature in the format of key-value pair to `data`. |

>! The key in the example is not real, and the timestamp is not the current system time. If you open this URL in the browser or call it by using commands such as `curl`, an authentication error `The signature expired` will be returned. To obtain a URL that works, you need to replace the `SecretId` and `SecretKey` in this example with your own credentials and use the current system time as the `Timestamp`. 

To further explain the signing process, Java is used as examples below to implement the process as described above. The request domain name, API, and parameter values in the above example are used here. The code below is for demonstration only. Please use the SDK for actual development.

#### 6. Encode a signature string

The generated signature string cannot be directly used as a request parameter and needs to be URL-encoded.

For example, if the signature string generated in the previous step is `Eli*****************cGeI=`, the final value of the `Signature` request parameter will be `EliP***********************eI%3d`, which will be used to generate the final request URL.
>!
>- If you use the GET request method or use the POST request method with `Content-Type` of `application/x-www-form-urlencoded`, all the request parameter values must be URL-encoded (except the parameter key and the equal symbol (=)) before the request is sent. Non-ASCII characters must be encoded with **UTF-8** before URL-encoding.
>- The network libraries of some programming languages automatically URL-encode all parameters. In this case, the signature string does not need to be URL-encoded again; otherwise, two rounds of URL-encoding will cause the signature to fail.
>- Other parameter values also need to be encoded with [RFC 3986](http://tools.ietf.org/html/rfc3986). Use `%XY` in percent-encoding for special characters such as Chinese characters, where "X" and "Y" are hexadecimal characters (0–9 and uppercase A–F). Using lowercase characters will cause an error.

#### 7. Sample API 3.0 signature v1

```java
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
import java.util.Random;
import java.util.TreeMap;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import javax.xml.bind.DatatypeConverter;

public class TencentCloudAPIDemo {
    private final static String CHARSET = "UTF-8";

    public static String sign(String s, String key, String method) throws Exception {
        Mac mac = Mac.getInstance(method);
        SecretKeySpec secretKeySpec = new SecretKeySpec(key.getBytes(CHARSET), mac.getAlgorithm());
        mac.init(secretKeySpec);
        byte[] hash = mac.doFinal(s.getBytes(CHARSET));
        return DatatypeConverter.printBase64Binary(hash);
    }

    public static String getStringToSign(TreeMap<String, Object> params) {
        StringBuilder s2s = new StringBuilder("GETcvm.tencentcloudapi.com/?");
        // In the signing process, the parameters need to be sorted in lexicographical order. `TreeMap` is used here to guarantee the correct order
        for (String k : params.keySet()) {
            s2s.append(k).append("=").append(params.get(k).toString()).append("&");
        }
        return s2s.toString().substring(0, s2s.length() - 1);
    }

    public static String getUrl(TreeMap<String, Object> params) throws UnsupportedEncodingException {
        StringBuilder url = new StringBuilder("https://cvm.tencentcloudapi.com/?");
        // An actual request URL has no requirement for the order of parameters
        for (String k : params.keySet()) {
            // The request string needs to be URL-encoded. As the key consists of only English letters, only the value is URL-encoded
			url.append(k).append("=").append(URLEncoder.encode(params.get(k).toString(), CHARSET)).append("&");
        }
        return url.toString().substring(0, url.length() - 1);
    }

    public static void main(String[] args) throws Exception {
        TreeMap<String, Object> params = new TreeMap<String, Object>(); // TreeMap supports automatic sorting
        // A random number should be used during an actual call, such as `params.put("Nonce", new Random().nextInt(java.lang.Integer.MAX_VALUE));`
        params.put("Nonce", 11886); // Common parameter
        // The current system time should be used during an actual call, such as `params.put("Timestamp", System.currentTimeMillis() / 1000);`
        params.put("Timestamp", 1465185768); // Common parameter
        params.put("SecretId", "AKIDz8krbsJ5**********mLPx3EXAMPL"); // Common parameter
        params.put("Action", "DescribeInstances"); // Common parameter
        params.put("Version", "2017-03-12"); // Common parameter
        params.put("Region", "ap-guangzhou"); // Common parameter
        params.put("Limit", 20); // Service parameter
        params.put("Offset", 0); // Service parameter
        params.put("InstanceIds.0", "ins-09dx96dg"); // Service parameter
        params.put("Signature", sign(getStringToSign(params), "Gu5t9xGAR***********EXAMPLE", "HmacSHA1")); // Common parameter
        System.out.println(getUrl(params));
    }
}
```

## API 2.0 Signature

This signature version has been disused. We recommend you use **API 3.0 signature** with better performance. If you still need to use it, please go to [API Explorer](https://console.cloud.tencent.com/api/explorer) > **Signature Generation** and select **API 2.0 Signature** as the signature version.

## Signature Failure

The following error codes may be returned for signature failure. Please resolve the errors accordingly.

| Error Code | Error Description |
| :--------------------------- | :----------------------------------------------------------- |
| AuthFailure.SignatureExpire | The signature expired. The difference between the `Timestamp` and the server time cannot be greater than five minutes. |
| AuthFailure.SecretIdNotFound | The key does not exist. Log in to the console and check whether it is disabled or you copied fewer or more characters. |
| AuthFailure.SignatureFailure | Signature error. It is possible that the signature is calculated incorrectly, the signature does not match the content that is actually sent, or the `SecretKey` is incorrect. |
| AuthFailure.TokenFailure | Temporary credential token error. |
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |

## Returned Result

### Successful response

For example, when calling the CVM API `DescribeInstancesStatus` (version: 2017-03-12) to view the status of instances, if the request succeeds, you may see the following response:

```json
{
    "Response": {
        "TotalCount": 0,
        "InstanceStatusSet": [],
        "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
    }
}
```

- The API will return `Response`, which contains `RequestId`, as long as it processes the request, no matter whether the request is successful or not.
- `RequestId` is the unique ID of an API request. It is required to troubleshoot issues.
- Any fields other than the common fields are API-specific. For more information on such fields, please see the relevant API documentation. In this example, both `TotalCount` and `InstanceStatusSet` are specific to the `DescribeInstancesStatus` API. Since the user who initiated the request does not have a CVM instance yet, 0 is returned for `TotalCount` and `InstanceStatusSet` is empty.

### Error response

 If the call fails, you may see the following response: 

```json
{
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

- `Error` indicates that the request failed. A response for a failed request will always include the `Error`, `Code`, and `Message` fields.
- `Code` indicates the specific error code, which is returned when an API request failed. You can use this code to locate the cause and solution of the error in the common or API-specific error code list.
- `Message` explains the cause of the error. Note that the returned messages are subject to service updates. The information the messages provide may not be up-to-date and should not be the only source of reference.
- `RequestId` is the unique ID of an API request. It is required to troubleshoot issues.

### Common error codes

 The `Error` field in a response indicates that the API call failed. The `Code` field in `Error` indicates the error code. The following table lists the common error codes that any services may return. 

| Error Code | Error Description |
| :-------------------------------- | :---------------------------------------------------------- |
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure. |
| AuthFailure.SecretIdNotFound | The key does not exist. |
| AuthFailure.SignatureExpire | The signature expired. |
| AuthFailure.SignatureFailure | Signature error. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | No CAM authorization. |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | The operation failed. |
| InternalError | Internal error. |
| InvalidAction | The API does not exist. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameterValue | Invalid parameter value. |
| LimitExceeded | The quota limit is exceeded. |
| MissingParameter | A parameter is missing. |
| NoSuchVersion | The API version does not exist. |
| RequestLimitExceeded | The request rate limit is exceeded. |
| ResourceInUse | The resource is in use. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | The resource does not exist. |
| ResourceUnavailable | The resource is unavailable. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter error. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | Unsupported HTTPS request method. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region. |



