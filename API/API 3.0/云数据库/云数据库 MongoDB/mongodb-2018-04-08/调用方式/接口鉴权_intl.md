Tencent Cloud API authenticates each access request, so each request is required to include the Signature in the common request parameters for user identity authentication.
The signature is generated with user's security credentials, which consist of a SecretId and a SecretKey. If you don't have security credentials, apply for the credentials on the [Cloud API Key](https://console.cloud.tencent.com/capi) page. Otherwise, you will not be able to call the cloud APIs.

## 1. Apply for Security Credentials
Before using cloud APIs for the first time, you need to apply for security credentials on the [Cloud API Key](https://console.cloud.tencent.com/capi) page.
Security credentials consist of a SecretId and a SecretKey:
* The SecretId: Identify of the API requester.
* The SecretKey: A key that can be used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the requester.
* <font color='red'>The security credentials must be kept confidential to avoid leakage.</font>

Apply for security credentials by following the steps below:

1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/).
1. Go to the [Cloud API Key](https://console.cloud.tencent.com/capi) console page.
1. On the [Cloud API Key](https://console.cloud.tencent.com/capi) page, click **Create** to create a pair of SecretId/SecretKey.

Note: A developer account can have up to two pairs of SecretId/SecretKey.

## 2. Generate Signature String

With the SecretId and SecretKey, a signature string can be generated. The following describes how to generate a signature string:

Suppose that you have the following SecretId and SecretKey:

* SecretId: AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE
* SecretKey: Gu5t9xGARNpq86cd98joQYCN3EXAMPLE

**Note: This is only for demonstration purpose. Make sure you proceed with your actual SecretId and SecretKey.**

For example, if you call the API "View CVM Instance List" (DescribeInstances), the possible request parameters are as follows:

| Parameter Name | Description | Parameter Value |
|---------|---------|---------|
| Action | Method name | DescribeInstances |
| SecretId | Key ID | AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE |
| Timestamp | Current timestamp | 1465185768 |
| Nonce | A random positive integer | 11886 |
| Region | The region where the instance resides | ap-guangzhou |
| InstanceIds.0 | ID of the instance to be queried | ins-09dx96dg |
| Offset | Offset value | 0 |
| Limit | Maximum number of output results | 20 |
| Version | API version | 2017-03-12 |


### 2.1. Sort parameters

First, sort all the request parameters in an ascending lexicographical order (ASCII code) by their names. Notes: (1) Parameters are sorted by their names instead of their values; (2) The parameters are sorted based on ASCII code, not in an alphabetical order or by values. For example, InstanceIds.2 should be arranged after InstanceIds.12. You can complete the sorting process using a sorting function in a programming language, such as the ksort function in PHP. The parameters in the example are sorted as follows:

```
{
    'Action' : 'DescribeInstances',
    'InstanceIds.0' : 'ins-09dx96dg',
    'Limit' : 20,
    'Nonce' : 11886,
    'Offset' : 0,
    'Region' : 'ap-guangzhou',
    'SecretId' : 'AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE',
    'Timestamp' : 1465185768,
    'Version': '2017-03-12',
}
```
Any other programming language can be used to sort these parameters as long as the same result is produced.

### 2.2. Generate a request string

This step is to generate the request string.
Format the request parameters sorted in the previous step as "parameter name"="parameter value". For example, if the parameter value of "Action" is "DescribeInstances", the resulting format is Action=DescribeInstances.
**Note: "Parameter value" is the original value rather than the URL encoded value.**

Then, join the formatted parameters together with "&" to generate the final request string:

```
Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.3. Generate the original signature string
This step is to generate the original signature string.
The original signature string is composed of the following parameters:

1. Request method: The POST and GET methods are supported. In this case, a GET request is used. Please note that the methods must be in upper-case.
2. Request host: The request domain name for the API "View Instance List" (DescribeInstances) is cvm.tencentcloudapi.com. The actual request domain name varies with the module to which the API belongs. For more information, see the relevant API description.
3. Request path: The request path for the current version of cloud API is always "/".
4. Request string: The request string generated in the previous step.

The original signature string is constructed as follows: Request Method + Request Host + Request Path + ? + Request String

The resulting string is:

```
GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12
```

### 2.4. Generate a signature string
This step is to generate a signature string.
Sign the **original signature string** obtained in the previous step using HMAC-SHA1 algorithm, and then encode the signature string using Base64 to obtain the final signature string.

For example, the code is as follows if written in PHP:

```
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3EXAMPLE';
$srcStr = 'GETcvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Timestamp=1465185768&Version=2017-03-12';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

The resulting signature string is as follows:

```
EliP9YW3pW28FpsEdkXt/+WcGeI=
```

When you're using any other programming language, you can use the original signature string in the above example for signature verification, as long as the resulting signature string is same as the one in the example.

## 3. Encode the Signature String

The generated signature string cannot be directly used as the request parameter, and needs to be URL encoded.

For example, the signature string "EliP9YW3pW28FpsEdkXt/+WcGeI=" generated in the previous step is converted to the final signature string request parameter (Signature): EliP9YW3pW28FpsEdkXt%2f%2bWcGeI%3d, which will be used to generate the final request URL.

**Note: If GET method is used, or if POST method is used and Content-Type is application/x-www-form-urlencoded, all request parameters need to be URL encoded. Encoding is not required for parameter keys and equal sign ("="). Non-ASCII characters should be encoded with UTF-8 before they can be URL encoded.**

**Note: For some programming languages, their HTTP libraries can encode URLs automatically for all parameters. In this case, URL encoding is not required for the signature string, because repeated URL encoding will cause signature failure.**

**Note: Other parameters need to be encoded using [RFC 3986](http://tools.ietf.org/html/rfc3986). For special characters such as Chinese characters, %XY is used to do percentage encoding, in which "X" and "Y" are hexadecimal characters (0-9 and A-F). Lower cases will cause an error.**

## 4. Signature Failure
The following signature error codes may be returned depending on the actual situation.

| Error Code | Description |
|----------|---------|
| AuthFailure.SignatureExpire | Signature expired |
| AuthFailure.SecretIdNotFound | Key does not exist |
| AuthFailure.SignatureFailure | Invalid signature |
| AuthFailure.TokenFailure | Invalid token |
| AuthFailure.InvalidSecretId | Invalid key (it is not a cloud API key) |

## 5. Signature Demonstration

When calling the API 3.0, you're recommended to use the supplied Tencent Cloud SDK 3.0, which encapsulates the signature process to allow you to focus on the APIs provided by the product during development. For more information, see [SDK Center](https://cloud.tencent.com/document/sdk). The following programming languages are supported:

* [Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [JavaScript](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [.NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

The following examples show how the above signature process is implemented in various programming languages. The request domain name, APIs and parameter values to be used are same as the ones in the above signature process. The code below is only for demonstration purpose. Please use the SDK in your actual development.

The resulting URL may be: `https://cvm.tencentcloudapi.com/?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Limit=20&Nonce=11886&Offset=0&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE&Signature=EliP9YW3pW28FpsEdkXt%2F%2BWcGeI%3D&Timestamp=1465185768&Version=2017-03-12`

Note: Since the key used in the examples is fictitious and the timestamp is not the current system time, the authentication error "The signature expired" will be returned when you open this URL in a browser or call it with a command such as curl. To allow the URL to be returned normally, replace the SecretId and SecretKey in the examples with the real keys, and use the current system timestamp as the Timestamp.

Note: In the following examples, the order in which the parameters are arranged in the resulting URL may vary with different programming languages, even with each execution of the code in the same programming language. But this does not affect the correctness of the URL, provided that all parameters are included and the resulting signature is correct.

Note: The following code only applies to API 3.0 and cannot be directly used in other signature processes. Even in the earlier versions of API, the differences in specifics between versions may lead to signature computing error. For more information, see the relevant documentation.

### Java

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
        // The parameters are required to be sorted in lexicographic order during the generation of signature, and TreeMap is used here to implement the sorting.
        for (String k : params.keySet()) {
            s2s.append(k).append("=").append(params.get(k).toString()).append("&");
        }
        return s2s.toString().substring(0, s2s.length() - 1);
    }

    public static String getUrl(TreeMap<String, Object> params) throws UnsupportedEncodingException {
        StringBuilder url = new StringBuilder("https://cvm.tencentcloudapi.com/?");
        // There is no requirement for the order of parameters in the actual request URL.
        for (String k : params.keySet()) {
            // The request string should be URL-encoded. Since key is comprised of letters only, its value must be URL-encoded.
            url.append(k).append("=").append(URLEncoder.encode(params.get(k).toString(), CHARSET)).append("&");
        }
        return url.toString().substring(0, url.length() - 1);
    }

    public static void main(String[] args) throws Exception {
        TreeMap<String, Object> params = new TreeMap<String, Object>(); // TreeMap is used for auto-sorting.
        // A random number should be used in the actual request, for example: params.put("Nonce", new Random().nextInt(java.lang.Integer.MAX_VALUE));
        params.put("Nonce", 11886); // Common parameters
        // The current system time should be used in the actual request, for example: params.put("Timestamp", System.currentTimeMillis() / 1000);
        params.put("Timestamp", 1465185768); // Common parameters
        params.put("SecretId", "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"); // Common parameters
        params.put("Action", "DescribeInstances"); // Common parameters
        params.put("Version", "2017-03-12"); // Common parameters
        params.put("Region", "ap-guangzhou"); // Common parameters
        params.put("Limit", 20); // Service parameter
        params.put("Offset", 0); // Service parameter
        params.put("InstanceIds.0", "ins-09dx96dg"); // Service parameter
        params.put("Signature", sign(getStringToSign(params), "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE", "HmacSHA1")); // Common parameters
        System.out.println(getUrl(params));
    }
}
```

### Python

Note: Before you can run the code in a Python 2 environment, install the requests dependency package `pip install requests`.

```python
# -*- coding: utf8 -*-
import base64
import hashlib
import hmac
import time

import requests

secret_id = "AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE"
secret_key = "Gu5t9xGARNpq86cd98joQYCN3EXAMPLE"

def get_string_to_sign(method, endpoint, params):
    s = method + endpoint + "/?"
    query_str = "&".join("%s=%s" % (k, params[k]) for k in sorted(params))
    return s + query_str

def sign_str(key, s, method):
    hmac_str = hmac.new(key.encode("utf8"), s.encode("utf8"), method).digest()
    return base64.b64encode(hmac_str)

if __name__ == '__main__':
    endpoint = "cvm.tencentcloudapi.com"
    data = {
        'Action' : 'DescribeInstances',
        'InstanceIds.0' : 'ins-09dx96dg',
        'Limit' : 20,
        'Nonce' : 11886,
        'Offset' : 0,
        'Region' : 'ap-guangzhou',
        'SecretId' : secret_id,
        'Timestamp' : 1465185768, # int(time.time())
        'Version': '2017-03-12'
    }
    s = get_string_to_sign("GET", endpoint, data)
    data["Signature"] = sign_str(secret_key, s, hashlib.sha1)
    print(data["Signature"])
 # The API will be called actually, and a fee may be incurred if the call is successful.
    # resp = requests.get("https://" + endpoint, params=data)
    # print(resp.url)
```

