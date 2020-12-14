
TencentCloud API has been upgraded to v3.0. This version is optimized for performance and deployed in all regions. It supports nearby access and access by region for significantly reduced access latency. In addition, it features more detailed API descriptions and error codes and API-level comments for SDKs, enabling you to use Tencent Cloud services more conveniently and quickly. This document describes how to call APIs for C++.
This version currently supports various [Tencent Cloud services](https://intl.cloud.tencent.com/product) such as CVM, CBS, VPC, and TencentDB and will support more services in the future. 


## Request Structure

### 1. Service address (endpoint)

TencentCloud API supports access from either a nearby region (such as `cvm.tencentcloudapi.com` for CVM) or a specified region (such as `cvm.ap-guangzhou.tencentcloudapi.com` for CVM in the Guangzhou region). For values of the region parameter, please see the region list in the "Common Parameters" section below. To check whether a region is supported by a specific Tencent Cloud service, please see its "Request Structure" document.

>!For latency-sensitive businesses, we recommend you specify a domain name with a region.

### 2. Communications protocol

 All TencentCloud APIs communicate over HTTPS, providing highly secure communications tunnels. 

### 3. Request method

Supported HTTP request methods:

- POST (recommended)
- GET

`Content-Type` types supported by POST request:
- application/json (recommended). The signature algorithm v3 (TC3-HMAC-SHA256) must be used.
- application/x-www-form-urlencoded. The signature algorithm v1 (HmacSHA1 or HmacSHA256) must be used.
- multipart/form-data (only supported by certain APIs). The signature algorithm v3 (TC3-HMAC-SHA256) must be used.

The size of a GET request packet cannot exceed 32 KB. The size of a POST request cannot exceed 1 MB for the signature algorithm v1 (HmacSHA1 or HmacSHA256) or 10 MB for the signature algorithm v3 (TC3-HMAC-SHA256).

### 4. Character encoding

<kbd>UTF-8</kbd> encoding is always used.



## Common Parameters

>?The common parameters are used to identity the user and API signature. They should be carried by each request to initiate properly. 

### Signature algorithm v3

The signature algorithm v3 (sometimes referred to as "TC3-HMAC-SHA256") is more secure than the signature algorithm v1 (referred to as signature algorithm in certain documents), supports larger request packets and POST JSON format, and has a higher performance. We recommend you use it to calculate signatures. For more information on how to use it, please see below. 

| Parameter Name | Type | Required | Description |
| :------------- | :------ | :----- | :----------------------------------------------------------- |
| X-TC-Action | String | **Yes** | Name of the API for the desired operation. For the specific value, please see the description of common parameter `Action` in the input parameters in the related API document. For example, the API for querying CVM instance list is `DescribeInstances`. |
| X-TC-Region | String | - | Region parameter, which is used to identify the region where the data you want to manipulate resides. For values supported for an API, please see the description of common parameter `Region` in the input parameters in related API documentation. **Note: this parameter is not required for some APIs (which will be indicated in related API documentation) and will not take effect even if it is passed.** |
| X-TC-Timestamp | Integer | **Yes** | The current UNIX timestamp that records the time when the API request was initiated, such as 1529223702. **Note: if the difference between the UNIX timestamp and the server time is greater than 5 minutes, a signature expiration error may occur.** |
| X-TC-Version | String | **Yes** | Version of the API for the desired operation, such as 2017-03-12 for CVM. For the specific value, please see the description of common parameter `Version` in the input parameters in related API documentation. |
| Authorization | String | **Yes** | HTTP authentication request header, such as TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea8******************************************a96525168 <br>Here, <li>TC3-HMAC-SHA256: signature algorithm, currently fixed as this value. </li><li>Credential: signature credential. `AKIDEXAMPLE` indicates the `SecretId`. </li><li>`Date` indicates a UTC date which must match the value of `X-TC-Timestamp` (a common parameter) in UTC format. </li><li>`service` indicates the name of the service and is generally a domain name prefix; for example, the domain name `cvm.tencentcloudapi.com` means the CVM service, and the value for this service is `cvm`. </li><li>SignedHeaders: the headers that contain the authentication information. `content-type` and `host` are required. </li><li>Signature: signature digest. For the calculation process, please see below. </li> |
| X-TC-Token | String | No | Token used for temporary credentials. It must be used with a temporary key. You can get the temporary key and token by calling a CAM API. No token is required for a long-term key. |



### Region list

As the supported regions vary by service, please refer to the region list in each service's product documentation for specific details.
For example, you can see the [region list](https://intl.cloud.tencent.com/document/product/213/31574) of CVM.



## API Call Method for C++

TencentCloud API authenticates every request, that is, the request must be signed with the security credentials in the designated steps. Each request must contain the signature information in the common request parameters and be sent in the specified way and format.
>!Currently, API 3.0 signature v1 is not supported for C++.

Suppose your `SecretId` and `SecretKey` are `AKIDz8krbsJ5**********mLPx3EXAMPLE` and `Gu5t9xGAR***********EXAMPLE`, respectively. If you want to view the status of an unnamed instance in the Guangzhou region and have only one data entry returned, the request may be: 
```
curl -X POST https://cvm.tencentcloudapi.com \
-H "Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5**********mLPx3EXAMPLE/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea809ad7a8c8f7a4507b9bddcbaa8e581f516e8da2f66e2c5a96525168" \
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

- SecretId: identifies the user that calls an API, which is similar to a username.
- SecretKey: authenticates the user that calls the API, which is similar to a password.

>! **You must keep your security credentials private and avoid disclosure; otherwise, your assets may be compromised. If they are disclosed, please disable them as soon as possible.**

Go to the [API key management](https://console.cloud.tencent.com/cam/capi) page to get API keys as shown below:
![](https://main.qcloudimg.com/raw/12b5b846c057addb6ea5eab9010bc42f.png)

### Step 2. Get an API 3.0 signature v3
The signature algorithm v3 (TC3-HMAC-SHA256) is compatible with the previous signature algorithm v1 and more secure, supports larger request packets and POST JSON format, and has a higher performance. We recommend you use it to calculate signatures as shown below:
>?If you are using the signature algorithm for the first time, we recommend you use the "signature string generation" feature in [API Explorer](https://console.cloud.tencent.com/api/explorer) and select "API 3.0 signature v3" as the signature version, which can generate a signature for demonstration and verification. Plus, it can also generate SDK code directly. Seven common open-source programming language SDKs are available for TencentCloud API, including [Python](https://github.com/TencentCloud/tencentcloud-sdk-python), [Java](https://github.com/TencentCloud/tencentcloud-sdk-java), [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php), [Go](https://github.com/TencentCloud/tencentcloud-sdk-go), [Node.js](https://github.com/TencentCloud/tencentcloud-sdk-nodejs), [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet), and [C++](https://github.com/TencentCloud/tencentcloud-sdk-cpp).
>
![](https://main.qcloudimg.com/raw/2bd7aa3a0f840da675a8eb768aa3dc72.png)


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
| CanonicalHeaders | Header information for signature calculation, including at least `host` and `content-type`. Custom headers can also be added to the signature process to improve the uniqueness and security of the request. Concatenation rules: both the key and value of a header should be converted to lowercase with the leading and trailing spaces removed so that they are concatenated in the `key:value\n` format. If there are multiple headers, they should be sorted in ASCII ascending order by header key (lowercase). The calculation result in this example is `content-type:application/json; charset=utf-8\nhost:cvm.tencentcloudapi.com\n`. Note: `content-type` must match the content that is actually sent. In some programming languages, a `charset` value is automatically added even if it is not specified. In this case, the request sent will be different from the one signed, and the sever will return a signature verification failure. |
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

>!
> - `Date` must be calculated from the timestamp `X-TC-Timestamp` and the time zone is UTC+0. If you add the local time zone information (such as UTC+8) in the system, calls can succeed both day and night but will definitely fail at 00:00. For example, if the timestamp is 1551113065 and the time in UTC+8 is 2019-02-26 00:44:25, the UTC+0 date in the calculated `Date` value should be 2019-02-25 instead of 2019-02-26.
> - `Timestamp` must be the same as your current system time, and your system time must be in sync with the UTC time. If the difference between the timestamp and your current system time is greater than five minutes, the request will fail. If your system time is out of sync with the UTC time for a prolonged period, the request will fail, and a signature expiration error will be returned.

 According to the rules above, the string to sign obtained in the example is as follows: 

```
TC3-HMAC-SHA256
1551113065
2019-02-25/cvm/tc3_request
5ffe6a04c0664d6b969fab9a13bdab201d63ee709638e2749d62a09ca18d7031
```

#### 3. Calculate the signature (pseudocode)

Please see the following sample code:
1) Calculate the derived signature key with the following pseudocode:

```c++
#include <tencentcloud/core/Sign.h>
#include <tencentcloud/core/utils/Utils.h>


using namespace TencentCloud;
using namespace std;

string Sign::Tc3Sign(const string &credDate, const string &serviceName, const string &signStr)
{
    string kKey = "TC3"+this->m_secretKey;
    string kDate = Utils::HmacSha256(kKey, credDate);
    string kService = Utils::HmacSha256(kDate, serviceName);
    string kSigning = Utils::HmacSha256(kService, "tc3_request");
    return Utils::HexEncode(Utils::HmacSha256(kSigning, signStr));
}
```

The derived key `SecretDate`,` SecretService`, and `SecretSigning` are binary data and may contain non-printable characters. Intermediate results are not displayed here.

>! The order of the parameters in the HMAC library functions may vary by programming language. In the pseudo code here, key parameters are at the second half, and the actual requirement of the used programming language shall prevail. Generally, standard library functions will provide calculated values in binary format, which is also used here. They will also provide print-friendly calculated values in hexadecimal format, which will be used in calculating the signature result below.

| Field | Description |
| :---------- | :----------------------------------------------------------- |
| m_secretKey | Original `SecretKey`, i.e., `Gu5t9xGAR***********EXAMPLE`. |
| credDate | Value of the `Date` field in `Credential`, such as `2019-02-25` in this example. |
| serviceName | Value of the `Service` field in `Credential`, such as `cvm` in this example. |
| signStr     | String to be signed.                                               |

2) Calculate the signature

The calculation result in this example is `72e494ea8******************************************a96525168`.

#### 4. Concatenate the Authorization string

Concatenate the `Authorization` string in the following format:
```
Authorization =
    Algorithm + ' ' +
    'Credential=' + SecretId + '/' + CredentialScope + ', ' +
    'SignedHeaders=' + SignedHeaders + ', ' +
    'Signature=' + Signature
```

| Field | Description |
| :-------------- | :----------------------------------------------------------- |
| Algorithm | Signature algorithm, which is always `TC3-HMAC-SHA256`. |
| SecretId | `SecretId` in the key pair, i.e., `AKIDz8krbsJ5**********mLPx3EXAMPLE`. |
| CredentialScope | Credential scope (see above). The calculation result in this example is `2019-02-25/cvm/tc3_request`. |
| SignedHeaders | Header information for signature calculation (see above), such as `content-type;host` in this example. |
| Signature       | Signature value. The calculation result in this example is `72e494ea8******************************************a96525168`. |

According to the rules above, the values obtained in this example are:

```
TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5**********mLPx3EXAMPLE/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea8******************************************a96525168
```

The complete call information is as follows:

```
POST https://cvm.tencentcloudapi.com/
Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5**********mLPx3EXAMPLE/2019-02-25/cvm/tc3_request, SignedHeaders=content-type;host, Signature=72e494ea8******************************************a96525168
Content-Type: application/json; charset=utf-8
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1551113065
X-TC-Region: ap-guangzhou

{"Limit": 1, "Filters": [{"Values": ["\u672a\u547d\u540d"], "Name": "instance-name"}]}
```

#### 5. Sample API 3.0 signature v3

```c++
#include <iostream>
#include <iomanip>
#include <sstream>
#include <string>
#include <stdio.h>
#include <time.h>
#include <openssl/sha.h>
#include <openssl/hmac.h>

using namespace std;

string get_data(int64_t &timestamp)
{
    string utcDate;
    char buff[20] = {0};
    // time_t timenow;
    struct tm sttime;
    sttime = *gmtime(&timestamp);
    strftime(buff, sizeof(buff), "%Y-%m-%d", &sttime);
    utcDate = string(buff);
    return utcDate;
}
string int2str(int64_t n)
{
    std::stringstream ss;
    ss << n;
    return ss.str();
}
string sha256Hex(const string &str)
{
    char buf[3];
    unsigned char hash[SHA256_DIGEST_LENGTH];
    SHA256_CTX sha256;
    SHA256_Init(&sha256);
    SHA256_Update(&sha256, str.c_str(), str.size());
    SHA256_Final(hash, &sha256);
    std::string NewString = "";
    for(int i = 0; i < SHA256_DIGEST_LENGTH; i++)
    {
        snprintf(buf, sizeof(buf), "%02x", hash[i]);
        NewString = NewString + buf;
    }
    return NewString;
}
string HmacSha256(const string &key, const string &input)
{
    unsigned char hash[32];

    HMAC_CTX *h;
#if OPENSSL_VERSION_NUMBER < 0x10100000L
    HMAC_CTX hmac;
    HMAC_CTX_init(&hmac);
    h = &hmac;
#else
    h = HMAC_CTX_new();
#endif

    HMAC_Init_ex(h, &key[0], key.length(), EVP_sha256(), NULL);
    HMAC_Update(h, ( unsigned char* )&input[0], input.length());
    unsigned int len = 32;
    HMAC_Final(h, hash, &len);

#if OPENSSL_VERSION_NUMBER < 0x10100000L
    HMAC_CTX_cleanup(h);
#else
    HMAC_CTX_free(h);
#endif

    std::stringstream ss;
    ss << std::setfill('0');
    for (int i = 0; i < len; i++)
    {
        ss  << hash[i];
    }

    return (ss.str());
}
string HexEncode(const string &input)
{
    static const char* const lut = "0123456789abcdef";
    size_t len = input.length();
    
    string output;
    output.reserve(2 * len);
    for (size_t i = 0; i < len; ++i)
    {
        const unsigned char c = input[i];
        output.push_back(lut[c >> 4]);
        output.push_back(lut[c & 15]);
    }
    return output;
}

int main()
{
    // Key parameter
    string SECRET_ID = "AKIDz8krbsJ5**********mLPx3EXAMPLE";
    string SECRET_KEY = "Gu5t9xGAR***********EXAMPLE";

    string service = "cvm";
    string host = "cvm.tencentcloudapi.com";
    string region = "ap-guangzhou";
    string action = "DescribeInstances";
    string version = "2017-03-12";
    int64_t timestamp = 1551113065;
    string date = get_data(timestamp);

    // ************* Step 1. Concatenate the canonical request string *************
    string httpRequestMethod = "POST";
    string canonicalUri = "/";
    string canonicalQueryString = "";
    string canonicalHeaders = "content-type:application/json; charset=utf-8\nhost:" + host + "\n";
    string signedHeaders = "content-type;host";
    string payload = "{\"Limit\": 1, \"Filters\": [{\"Values\": [\"\\u672a\\u547d\\u540d\"], \"Name\": \"instance-name\"}]}";
    string hashedRequestPayload = sha256Hex(payload);
    string canonicalRequest = httpRequestMethod + "\n" + canonicalUri + "\n" + canonicalQueryString + "\n"
            + canonicalHeaders + "\n" + signedHeaders + "\n" + hashedRequestPayload;
    cout << canonicalRequest << endl;
    cout << "-----------------------" << endl;

    // ************* Step 2. Concatenate the string to sign *************
    string algorithm = "TC3-HMAC-SHA256";
    string RequestTimestamp = int2str(timestamp);
    string credentialScope = date + "/" + service + "/" + "tc3_request";
    string hashedCanonicalRequest = sha256Hex(canonicalRequest);
    string stringToSign = algorithm + "\n" + RequestTimestamp + "\n" + credentialScope + "\n" + hashedCanonicalRequest;
    cout << stringToSign << endl;
    cout << "-----------------------" << endl;

    // ************* Step 3. Calculate the signature ***************
    string kKey = "TC3" + SECRET_KEY;
    string kDate = HmacSha256(kKey, date);
    string kService = HmacSha256(kDate, service);
    string kSigning = HmacSha256(kService, "tc3_request");
    string signature = HexEncode(HmacSha256(kSigning, stringToSign));
    cout << signature << endl;
    cout << "-----------------------" << endl;

    // ************* Step 4. Concatenate the `Authorization` string *************
    string authorization = algorithm + " " + "Credential=" + SECRET_ID + "/" + credentialScope + ", "
            + "SignedHeaders=" + signedHeaders + ", " + "Signature=" + signature;
    cout << authorization << endl;
    cout << "------------------------" << endl;
    
    string headers = "curl -X POST https://" + host + "\n"
                   + " -H \"Authorization: " + authorization + "\n"
                   + " -H \"Content-Type: application/json; charset=utf-8\"" + "\n"
                   + " -H \"Host: " + host + "\n"
                   + " -H \"X-TC-Action: " + action + "\n"
                   + " -H \"X-TC-Timestamp: " + RequestTimestamp + "\n"
                   + " -H \"X-TC-Version: " + version + "\n"
                   + " -H \"X-TC-Region: " + region + "\n"
                   + " -d '" + payload;
    cout << headers << endl;
    return 0;
};
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
    "Response": {``
        "TotalCount": 0,
        "InstanceStatusSet": [],
        "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
    }
}
```

* The API will return `Response`, which contains `RequestId`, as long as it processes the request, no matter whether the request is successful or not.
* `RequestId` is the unique ID of an API request. It is required to troubleshoot issues.
* Any fields other than the common fields are API-specific. For more information on such fields, please see the relevant API documentation. In this example, both `TotalCount` and `InstanceStatusSet` are specific to the `DescribeInstancesStatus` API. Since the user who initiated the request does not have a CVM instance yet, 0 is returned for `TotalCount` and `InstanceStatusSet` is empty.

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

* `Error` indicates that the request failed. A response for a failed request will always include the `Error`, `Code`, and `Message` fields.
* `Code` indicates the specific error code, which is returned when an API request failed. You can use this code to locate the cause and solution of the error in the common or API-specific error code list.
* `Message` explains the cause of the error. Note that the returned messages are subject to service updates. The information the messages provide may not be up-to-date and should not be the only source of reference.
* `RequestId` is the unique ID of an API request. It is required to troubleshoot issues.

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
