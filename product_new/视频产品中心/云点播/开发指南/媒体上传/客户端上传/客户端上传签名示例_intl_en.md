## Sample of Signature in PHP
```php
<?php
// Determine the TencentCloud API key of the application
$secret_id = "XXXXXXXXXXXXXXXXXX";
$secret_key = "AAAAAAAAAAAAAAAAAAA";

// Determine the current time and expiration time of the signature
$current = time();
$expired = $current + 86400;  // Signature validity period: 1 day

// Enter the parameters into the parameter list
$arg_list = array(
    "secretId" => $secret_id,
    "currentTimeStamp" => $current,
    "expireTime" => $expired,
    "random" => rand());

// Calculate the signature
$original = http_build_query($arg_list);
$signature = base64_encode(hash_hmac('SHA1', $original, $secret_key, true).$original);

echo $signature;
echo "\n";
?>
```

## Sample of Signature in Java
```java
import java.util.Random;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import sun.misc.BASE64Encoder;

class Signature {
    private String secretId;
    private String secretKey;
    private long currentTime;
    private int random;
    private int signValidDuration;

    private static final String HMAC_ALGORITHM = "HmacSHA1";
    private static final String CONTENT_CHARSET = "UTF-8";

    public static byte[] byteMerger(byte[] byte1, byte[] byte2) {
        byte[] byte3 = new byte[byte1.length + byte2.length];
        System.arraycopy(byte1, 0, byte3, 0, byte1.length);
        System.arraycopy(byte2, 0, byte3, byte1.length, byte2.length);
        return byte3;
    }

    public String getUploadSignature() throws Exception {
        String strSign = "";
        String contextStr = "";

        long endTime = (currentTime + signValidDuration);
        contextStr += "secretId=" + java.net.URLEncoder.encode(secretId, "utf8");
        contextStr += "&currentTimeStamp=" + currentTime;
        contextStr += "&expireTime=" + endTime;
        contextStr += "&random=" + random;

        try {
            Mac mac = Mac.getInstance(HMAC_ALGORITHM);
            SecretKeySpec secretKey = new SecretKeySpec(this.secretKey.getBytes(CONTENT_CHARSET), mac.getAlgorithm());
            mac.init(secretKey);

            byte[] hash = mac.doFinal(contextStr.getBytes(CONTENT_CHARSET));
            byte[] sigBuf = byteMerger(hash, contextStr.getBytes("utf8"));
            strSign = base64Encode(sigBuf);
            strSign = strSign.replace(" ", "").replace("\n", "").replace("\r", "");
        } catch (Exception e) {
            throw e;
        }
        return strSign;
    }

    private String base64Encode(byte[] buffer) {
        BASE64Encoder encoder = new BASE64Encoder();
        return encoder.encode(buffer);
    }

    public void setSecretId(String secretId) {
        this.secretId = secretId;
    }

    public void setSecretKey(String secretKey) {
        this.secretKey = secretKey;
    }

    public void setCurrentTime(long currentTime) {
        this.currentTime = currentTime;
    }

    public void setRandom(int random) {
        this.random = random;
    }

    public void setSignValidDuration(int signValidDuration) {
        this.signValidDuration = signValidDuration;
    }
}

public class Test {
    public static void main(String[] args) {
        Signature sign = new Signature();
        sign.setSecretId("Secret Id of your API key");
        sign.setSecretKey("Secret Key of your API key");
        sign.setCurrentTime(System.currentTimeMillis() / 1000);
        sign.setRandom(new Random().nextInt(java.lang.Integer.MAX_VALUE));
        sign.setSignValidDuration(3600 * 24 * 2);

        try {
            String signature = sign.getUploadSignature();
            System.out.println("signature : " + signature);
        } catch (Exception e) {
            System.out.print("Failed to get the signature");
            e.printStackTrace();
        }
    }
}
```

For Java 1.9 and above, the packages related to `sun.misc.BASE64Encoder` have been removed. You can replace the corresponding implementation in the `base64Encode` method with `java.util.Base64`. For more information, please see the following code:
```java
import java.util.Base64;

private String base64Encode(byte[] buffer) {
    Base64.Encoder encoder = Base64.getEncoder();
    return encoder.encodeToString(buffer);
}
```

## Sample of Signature in Node.js
```javascript
var querystring = require("querystring");
var crypto = require('crypto');

// Determine the TencentCloud API key of the application
var secret_id = "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX";
var secret_key = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

// Determine the current time and expiration time of the signature
var current = parseInt((new Date()).getTime() / 1000)
var expired = current + 86400;  // Signature validity period: 1 day

// Enter the parameters into the parameter list
var arg_list = {
	secretId : secret_id,
	currentTimeStamp : current,
	expireTime : expired,
	random : Math.round(Math.random() * Math.pow(2, 32))
}

// Calculate the signature
var orignal = querystring.stringify(arg_list);
var orignal_buffer = new Buffer(orignal, "utf8");

var hmac = crypto.createHmac("sha1", secret_key);
var hmac_buffer = hmac.update(orignal_buffer).digest();

var signature = Buffer.concat([hmac_buffer, orignal_buffer]).toString("base64");

console.log(signature);
```

## Sample of Signature in C#
```csharp
using System;
using System.Security.Cryptography;
using System.Text;
using System.Threading;

class Signature
{
    public string m_strSecId;
    public string m_strSecKey;
    public int m_iRandom;
    public long m_qwNowTime;
    public int m_iSignValidDuration;
    public static long GetIntTimeStamp()
    {
        TimeSpan ts = DateTime.UtcNow - new DateTime(1970, 1, 1);
        return Convert.ToInt64(ts.TotalSeconds);
    }
    private byte[] hash_hmac_byte(string signatureString, string secretKey)
    {
        var enc = Encoding.UTF8; HMACSHA1 hmac = new HMACSHA1(enc.GetBytes(secretKey));
        hmac.Initialize();
        byte[] buffer = enc.GetBytes(signatureString);
        return hmac.ComputeHash(buffer);
    }
    public string GetUploadSignature()
    {
        string strContent = "";
        strContent += ("secretId=" + Uri.EscapeDataString((m_strSecId)));
        strContent += ("&currentTimeStamp=" + m_qwNowTime);
        strContent += ("&expireTime=" + (m_qwNowTime + m_iSignValidDuration));
        strContent += ("&random=" + m_iRandom);

        byte[] bytesSign = hash_hmac_byte(strContent, m_strSecKey);
        byte[] byteContent = System.Text.Encoding.Default.GetBytes(strContent);
        byte[] nCon = new byte[bytesSign.Length + byteContent.Length];
        bytesSign.CopyTo(nCon, 0);
        byteContent.CopyTo(nCon, bytesSign.Length);
        return Convert.ToBase64String(nCon);
    }
}
class Program
{
    static void Main(string[] args)
    {
        Signature sign = new Signature();
        sign.m_strSecId = "Secret Id of your API key";
        sign.m_strSecKey = "Secret Key of your API key";
        sign.m_qwNowTime = Signature.GetIntTimeStamp();
        sign.m_iRandom = new Random().Next(0, 1000000);
        sign.m_iSignValidDuration = 3600 * 24 * 2;

        Console.WriteLine(sign.GetUploadSignature());
    }
}

```

## Sample of Signature in Python
```Python
#!/usr/local/bin/python3
#coding=utf-8

import time
import random
import hmac
import hashlib
import base64

SecretId = 'IamSecretId'
SecretKey = 'IamSecretKey'
#TimeStamp = int(time.time())
TimeStamp = 1571215095
ExpireTime = TimeStamp + 86400 * 365 * 10
#Random = random.randint(0, 999999)
Random = 220625

Original = "secretId=" + SecretId + "&currentTimeStamp=" + str(TimeStamp) + "&expireTime=" + str(ExpireTime) + "&random=" + str(Random)

Hmac = hmac.new(bytes(SecretKey, 'utf-8'), bytes(Original, 'utf-8'), hashlib.sha1)
Sha1 = Hmac.digest()
Signature = bytes(Sha1) + bytes(Original, 'utf-8')
Signature2 = base64.b64encode(Signature)

#return str(signature2, 'UTF-8')

print("Original: ", Original)
print("HMAC-SHA1: ", Sha1)
print("Signature before BASE64: ", Signature)
print("Signature after BASE64: ", str(Signature2))
```
