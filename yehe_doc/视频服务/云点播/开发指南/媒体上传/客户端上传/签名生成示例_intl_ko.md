## PHP 서명 예시
```php
<?php
// 애플리케이션의 Tencent Cloud API 키를 결정합니다.
$secret_id = "XXXXXXXXXXXXXXXXXX";
$secret_key = "AAAAAAAAAAAAAAAAAAA";

// 서명의 현재 시간과 만료 시간을 결정합니다.
$current = time();
$expired = $current + 86400;  // 서명 유효 기간: 1일

// 매개변수 목록에 매개변수 입력
$arg_list = array(
    "secretId" => $secret_id,
    "currentTimeStamp" => $current,
    "expireTime" => $expired,
    "random" => rand());

// 서명 계산
$original = http_build_query($arg_list);
$signature = base64_encode(hash_hmac('SHA1', $original, $secret_key, true).$original);

echo $signature;
echo "\n";
?>
```

## Java의 서명 예시
```java
import java.util.Random;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import sun.misc.BASE64Encoder;

// 서명 툴
class Signature {
    private String secretId;
    private String secretKey;
    private long currentTime;
    private int random;
    private int signValidDuration;

    private static final String HMAC_ALGORITHM = "HmacSHA1"; //// 서명 알고리즘
    private static final String CONTENT_CHARSET = "UTF-8";

    public static byte[] byteMerger(byte[] byte1, byte[] byte2) {
        byte[] byte3 = new byte[byte1.length + byte2.length];
        System.arraycopy(byte1, 0, byte3, 0, byte1.length);
        System.arraycopy(byte2, 0, byte3, byte1.length, byte2.length);
        return byte3;
    }

    // 서명 획득
    public String getUploadSignature() throws Exception {
        String strSign = "";
        String contextStr = "";

        // 원본 매개변수 문자열 생성
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
        // 애플리케이션의 Tencent Cloud API 키 설정
        sign.setSecretId("API Key의 Secret Id");
        sign.setSecretKey("API Key의 Secret Key");
        sign.setCurrentTime(System.currentTimeMillis() / 1000);
        sign.setRandom(new Random().nextInt(java.lang.Integer.MAX_VALUE));
        sign.setSignValidDuration(3600 * 24 * 2); // 서명 유효 기간: 2일

        try {
            String signature = sign.getUploadSignature();
            System.out.println("signature : " + signature);
        } catch (Exception e) {
            System.out.print("서명 가져오기 실패");
            e.printStackTrace();
        }
    }
}
```

Java v1.9 이상에서는 `sun.misc.BASE64Encoder`와 관련된 패키지가 제거되었습니다. `base64Encode` 메소드의 해당 구현을 `java.util.Base64`로 바꿀 수 있습니다. 자세한 내용은 다음 코드를 참고하십시오.
```java
import java.util.Base64;

private String base64Encode(byte[] buffer) {
    Base64.Encoder encoder = Base64.getEncoder();
    return encoder.encodeToString(buffer);
}
```

## Node.js 서명 예시
```javascript
var querystring = require("querystring");
var crypto = require('crypto');

// app의 Tencent Cloud API 키를 결정합니다.
var secret_id = "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX";
var secret_key = "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

// 서명의 현재 시간과 만료 시간을 결정합니다.
var current = parseInt((new Date()).getTime() / 1000)
var expired = current + 86400;  // 서명 유효 기간: 1일

// 매개변수 목록에 매개변수 입력
var arg_list = {
	secretId : secret_id,
	currentTimeStamp : current,
	expireTime : expired,
	random : Math.round(Math.random() * Math.pow(2, 32))
}

// 서명 계산
var orignal = querystring.stringify(arg_list);
var orignal_buffer = new Buffer(orignal, "utf8");

var hmac = crypto.createHmac("sha1", secret_key);
var hmac_buffer = hmac.update(orignal_buffer).digest();

var signature = Buffer.concat([hmac_buffer, orignal_buffer]).toString("base64");

console.log(signature);
```

## C# 서명 예시
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
        sign.m_strSecId = "API Key의 Secret Id";
        sign.m_strSecKey = "API Key의 Secret Key";
        sign.m_qwNowTime = Signature.GetIntTimeStamp();
        sign.m_iRandom = new Random().Next(0, 1000000);
        sign.m_iSignValidDuration = 3600 * 24 * 2;

        Console.WriteLine(sign.GetUploadSignature());
    }
}

```

## Python 서명 예시
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

## Go 서명 예시
```go
package main

import (
	"crypto/hmac"
	"crypto/sha1"
	"encoding/base64"
	"fmt"
	"math/rand"
	"strconv"
	"time"
)

func generateHmacSHA1(secretToken, payloadBody string) []byte {
	mac := hmac.New(sha1.New, []byte(secretToken))
	sha1.New()
	mac.Write([]byte(payloadBody))
	return mac.Sum(nil)
}

func main() {
	rand.Seed(time.Now().Unix())
	secretId := "IamSecretId"
	secretKey := "IamSecretKey"
	// timestamp := time.Now().Unix()
	timestamp := int64(1571215095)
	expireTime := timestamp + 86400*365*10
	timestampStr := strconv.FormatInt(timestamp, 10)
	expireTimeStr := strconv.FormatInt(expireTime, 10)

	random := 220625
	randomStr := strconv.Itoa(random)
	original := "secretId=" + secretId + "&currentTimeStamp=" + timestampStr + "&expireTime=" + expireTimeStr + "&random=" + randomStr
	signature := generateHmacSHA1(secretKey, original)
	signature = append(signature, []byte(original)...)
	signatureB64 := base64.StdEncoding.EncodeToString(signature)
	fmt.Println(signatureB64)
}
```
