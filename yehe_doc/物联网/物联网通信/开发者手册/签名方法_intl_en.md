
## Overview
When a device initiates an HTTP/HTTPS request to the platform, the request message should contain the signature information (X-TC-Signature) for requester identity verification.

## Signing Steps

Sample device request message:
```
curl -X POST https://ap-guangzhou.gateway.tencentdevices.com/device/register \
-H "Content-Type: application/json; charset=utf-8" \
-H "X-TC-Algorithm: hmacsha256" \
-H "X-TC-Timestamp: 155****065" \
-H "X-TC-Nonce: 5456" \
-H "X-TC-Signature: 2230eefd229f582d8b1b891af****b91597240707d778ab3738f756258d7652c" \
-d '{"ProductId":"ASJ****GX","DeviceName":"xyz"}' 
```

### 1. Concatenate the string to sign

```
StringToSign =
    HTTPRequestMethod + \n +
    CanonicalHost + \n + 
    CanonicalURI + \n + 
    CanonicalQueryString + \n + 
    Algorithm + \n +
    RequestTimestamp + \n +
	   Nonce + \n +
    HashedCanonicalRequest
```

| Parameter | Description |
| ---------------------- | ------------------------------------------------------------ |
| HTTPRequestMethod      | HTTP request method. POST is supported                                     |
| CanonicalHost          | Host address of the HTTP request                                          |
| CanonicalURI           | URI of the HTTP request; for example, the URI of `https://ap-guangzhou.gateway.tencentdevices.com/device/register` is `/device/register` |
| CanonicalQueryString   | Query string in the URL of the initiated HTTP request, which is always an empty string `""` for POST requests |
| Algorithm              | Signature algorithm. Currently, HMACSHA256 and HMACSHA1 are supported                      |
| RequestTimestamp       | Request timestamp                                                   |
| Nonce                  | Random number                                                       |
| HashedCanonicalRequest | Hash value of the request body, which is calculated by SHA256 hashing the HTTP request body, performing hexadecimal encoding, and then converting the encoded string to lowercase letters |

According to the above rules, the canonical signature string obtained in the sample is as follows:

<dx-codeblock>
::: http http
POST
ap-guangzhou.gateway.tencentdevices.com
/device/register

hmacsha256
155****065
5456
35e9c5b0e3ae67532d3c9f17ead6c902226****b1ff7f6e89887f1398934f064
:::
</dx-codeblock>


### 2. Calculate the signature

- The pseudo code for using key signatures, including product-level keys and device-level keys, is as follows:
```
Signature = Base64_Encode(HMAC_SHA256(SignSecret, StringToSign))
```
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>SignSecret</td>
<td>Signature key. `ProductSecret` is used for dynamic registration, and `psk` is used for devices to publish messages or report logs</td>
</tr>
<tr>
<td>StringToSign</td>
<td>String to sign</td>
</tr>
</tbody></table>
- The pseudo code for using certificate signatures is as follows:
```
Signature = Base64_Encode(RSA_SHA256(PrivateKey, StringToSign))
```
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>PrivateKey</td>
<td>Certificate private key. Device X.509 private key certificate is used for devices to publish messages or report logs</td>
</tr>
<tr>
<td>StringToSign</td>
<td>String to sign</td>
</tr>
</tbody></table>

### 3. Assemble the request message

Based on the signature string obtained above, the final complete request is as follows:

```
POST https://ap-guangzhou.gateway.tencentdevices.com/devregister
Content-Type: application/json
Host: ap-guangzhou.gateway.tencentdevices.com
X-TC-Algorithm: HmacSha256
X-TC-Timestamp: 155****065
X-TC-Nonce: 5456
X-TC-Signature: 2230eefd229f582d8b1b891af71****1597240707d778ab3738f756258d7652c


{"ProductId":"ASJ****GX","DeviceName":"xyz"}
```


## Sample Code

Below is the sample code in Python 3:
<dx-codeblock>
:::  Python3
import hashlib
import random
import time
import hmac
import base64

if __name__ == '__main__':
    sign_format = '%s\n%s\n%s\n%s\n%s\n%d\n%d\n%s'
    url_format = '%s://ap-guangzhou.gateway.tencentdevices.com/device/register'
    request_format = "{\"ProductId\":\"%s\",\"DeviceName\":\"%s\"}"
device_name = 'dev***'
product_id = 'JCZ****KXS'
product_secret = 'X42fPqw********94cY5sQ1Y'

request_text = request_format % (product_id, device_name)
request_hash = hashlib.sha256(request_text.encode("utf-8")).hexdigest()

nonce = random.randrange(2147483647)
timestamp = int(time.time())
sign_content = sign_format % (
    "POST", "ap-guangzhou.gateway.tencentdevices.com",
    "/device/register", "", "hmacsha256", timestamp,
    nonce, request_hash)
print("\nsign_content: \n" + sign_content)

sign_base64 = base64.b64encode(hmac.new(product_secret.encode("utf-8"),
                sign_content.encode("utf-8"), hashlib.sha256).digest())

print("sign_base64: " + str(sign_base64))
:::
</dx-codeblock>







