
## Overview
This document describes the signature authentication methods of TPNS.

The HMAC-SHA256 algorithm is used to generate signing information according to `SecretKey`. The authentication is performed by verifying the signature, which ensures higher security and is recommended.


#### Parameter description

| Parameter | Description |
| --- | --- |
| AccessId | Application ID assigned by the TPNS backend, which can be obtained in the TPNS Console |
| SecretKey | `SecretKey` assigned by the TPNS backend, which corresponds to `AccessId` and can be obtained in the TPNS Console |
| LoginUin | Tencent Cloud login account |
| OwnerUin | Root account of Tencent Cloud account |
| Sign | API signature method |
| timeStamp |      Request timestamp |


## Signature Generation Method

1. Splice the request timestamp + `accessId` + request body to get the original string to be signed:
`String to be signed = ${timeStamp} + ${accessId} + ${request body}`
2. Use `secretKey` as the key to sign the original string to be signed to generate a signature:
`sign = Base64(HMAC_SHA256(string to be signed, secretKey))`

## HTTP Protocol Assembly Method

In addition to the general header protocol, the HTTP protocol header also needs to carry the current request timestamp, `AccessId`, and signature's `Sign` information. The specific parameters are as follows:

| Parameter Key in Header | Description | Required |
| --- | --- | --- |
| Sign | Request signature | Yes |
| AccessId | Application ID | Yes |
| TimeStamp | Request timestamp | Yes |

The specific HTTP request packet is as follows:
``` xml
POST /v3/push/app HTTP/1.1
Host: api.tpns.tencent.com
Content-Type: application/json
AccessId: 1500001048
TimeStamp: 1565314789
Sign: Y2QyMDc3NDY4MmJmNzhiZmRiNDNlMTdkMWQ1ZDU2YjNlNWI3ODlhMTY3MGZjMTUyN2VmNTRjNjVkMmQ3Yjxxxx==
{"audience_type": "account","platform": "android","message": {"title": "test title","content": "test content","android": { "action": {"action_type": 3,"intent": "xgscheme://com.xg.push/notify_detail?param1=xg"}}},"message_type": "notify","account_list": ["5822f0eee44c3625ef0000bb"] }
```

## Signature Generation Sample

1. The generated string to be signed is as follows:
```
String to be encrypted =15653147891500001048{"audience_type": "account","platform": "android","message": {"title": "test title","content": "test content","android": { "action": {"action_type": 3,"intent": "xgscheme://com.xg.push/notify_detail?param1=xg"}}},"message_type": "notify","account_list": ["5822f0eee44c3625ef0000bb"] }
```
2. Generate a hexadecimal hash based on the key through the HMAC-SHA256 algorithm, i.e., `secretKey =1452fcebae9f3115ba794fb0fff2fd73` in the sample.
```
hashcode= hmac-sha256(string to be signed, secretKey)
Get hashcode="cd20774682bf78bfdb43e17d1d5d56b3e5b789a1670fc1527ef54c65d2d7b76d"
```
3. Base64-encode the hashcode to get the following signature string:
```
Get Sign=Base64(hashcode)
Sign="Y2QyMDc3NDY4MmJmNzhiZmRiNDNlMTdkMWQ1ZDU2YjNlNWI3ODlhMTY3MGZjMTUyN2VmNTRjNjVkMmQ3Yjxxxx=="
```

**Sample Python signature**
```python
#!/usr/bin/env python
import hmac
import base64
from hashlib import sha256

s = '15653147891500001048{"audience_type": "account","platform": "android","message": {"title": "test title","content": "test content","android": { "action": {"action_type": 3,"intent": "xgscheme://com.xg.push/notify_detail?param1=xg"}}},"message_type": "notify","account_list": ["5822f0eee44c3625ef0000bb"] }'
key = '1452fcebae9f3115ba794fb0fff2fd73'
hashcode = hmac.new(key, s, digestmod=sha256).hexdigest()
print base64.b64encode(hashcode)

```
**Sample Java signature**
```java
package com.tencent.xg;

import java.io.UnsupportedEncodingException;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Base64;
import org.apache.commons.codec.binary.Hex;

public class SignTest {
    public static void main(String[] args) {
        try{
            String stringToSign = "15653147891500001048{\"audience_type\": \"account\",\"platform\": \"android\",\"message\": {\"title\": \"test title\",\"content\": \"test content\",\"android\": { \"action\": {\"action_type\": 3,\"intent\": \"xgscheme://com.xg.push/notify_detail?param1=xg\"}}},\"message_type\": \"notify\",\"account_list\": [\"5822f0eee44c3625ef0000bb\"] }";
            String appSecret = "1452fcebae9f3115ba794fb0fff2fd73";

            Mac mac;
            mac = Mac.getInstance("HmacSHA256");
            mac.init(new SecretKeySpec(appSecret.getBytes("UTF-8"), "HmacSHA256"));
            byte[] signatureBytes = mac.doFinal(stringToSign.getBytes("UTF-8"));

            String hexStr = Hex.encodeHexString(signatureBytes);
            String signature = Base64.encodeBase64String(hexStr.getBytes());

            System.out.println(signature);
        } catch (NoSuchAlgorithmException | InvalidKeyException | UnsupportedEncodingException e) {
            e.printStackTrace();
        }
    }
}

```
**Sample Go signature**
``` go
import(
   "crypto/hmac"
   "crypto/sha256"
   "encoding/base64"
   "encoding/hex"
   "testing"
)

func TestSign(t *testing.T) {
   requestBody := "15653147891500001048{\"audience_type\": \"account\",\"platform\": \"android\",\"message\": {\"title\": \"test title\",\"content\": \"test content\",\"android\": { \"action\": {\"action_type\": 3,\"intent\": \"xgscheme://com.xg.push/notify_detail?param1=xg\"}}},\"message_type\": \"notify\",\"account_list\": [\"5822f0eee44c3625ef0000bb\"] }"
   secretKey := "1452fcebae9f3115ba794fb0fff2fd73"

   h := hmac.New(sha256.New, []byte(secretKey))
   h.Write([]byte(requestBody))
   sha := hex.EncodeToString(h.Sum(nil))
   sign := base64.StdEncoding.EncodeToString([]byte(sha))
   println(sign)
}

```
