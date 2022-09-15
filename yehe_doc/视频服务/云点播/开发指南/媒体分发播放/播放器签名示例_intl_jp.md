## Python署名の例
[pyjwt](https://github.com/jpadilla/pyjwt/) ライブラリを使用して署名を計算します。`pip install pyjwt`を使用してインストールしてください。

```python
#!/usr/bin/python
#coding=utf-8

import jwt

AppId = 1255566655
FileId = "4564972818519602447"
CurrentTime = 1546340400
PsignExpire = 1546344000
UrlTimeExpire = "5c2b5640"
Key = "24FEQmTzro4V5u3D5epW"

Original = {
    "appId": AppId,
    "fileId": FileId,
    "currentTimeStamp": CurrentTime,
    "expireTimeStamp": PsignExpire,
    "urlAccessInfo": {
        "t": UrlTimeExpire
    }
}

Signature = jwt.encode(Original, Key, algorithm='HS256')

print("Original: ", Original)
print("Signature: ", Signature)
```

## Java署名の例
[java-jwt](https://github.com/auth0/java-jwt) ライブラリを使用して署名を計算します。

```java
import java.util.*;
import com.auth0.jwt.algorithms.Algorithm;
import com.auth0.jwt.exceptions.JWTCreationException;
import com.auth0.jwt.JWT;

class Main {
    public static void main(String[] args) {
        Integer AppId = 1255566655;
        String FileId = "4564972818519602447";
        Integer CurrentTime = 1589448067;
        Integer PsignExpire = 1589548067;
        String UrlTimeExpire = "5ebe9423‬";
        String Key = "24FEQmTzro4V5u3D5epW";
        HashMap<String, String> urlAccessInfo = new HashMap<String, String>();
        urlAccessInfo.put("t", UrlTimeExpire);

        try {
            Algorithm algorithm = Algorithm.HMAC256(Key);
            String token = JWT.create().withClaim("appId", AppId).withClaim("fileId", FileId)
                    .withClaim("currentTimeStamp", CurrentTime).withClaim("expireTimeStamp", PsignExpire)
                    .withClaim("urlAccessInfo", urlAccessInfo).sign(algorithm);
            System.out.println("token:" + token);
        } catch (JWTCreationException exception) {
            // Invalid Signing configuration / Couldn't convert Claims.
        }
    }
}
```

## Go署名の例

[jwt-go](https://github.com/dgrijalva/jwt-go) ライブラリを使用して署名を計算します。コマンドgo get github.com/dgrijalva/jwt-go`を使用してインストールしてください。

```go

package main

import (
        "fmt"
        "time"
        "strconv"
        "github.com/dgrijalva/jwt-go"
)

func main() {
        appId := 1255566655 // ユーザー appid
        fileId := "4564972818519602447" // ターゲット FileId
        currentTime := time.Now().Unix()
        psignExpire := currentTime + 3600 // 有効期限は、1hなど任意に設定できます
        urlTimeExpire := strconv.FormatInt(psignExpire, 16) // 有効期限は、1hなどの16進文字列で任意に設定できます
        key := []byte("24FEQmTzro4V5u3D5epW")

        // Create a new token object, specifying signing method and the claims
        // you would like it to contain.
        token := jwt.NewWithClaims(jwt.SigningMethodHS256, jwt.MapClaims{
                "appId":            appId,
                "fileId":           fileId,
                "currentTimeStamp": currentTime,
                "expireTimeStamp":  psignExpire,
                "urlAccessInfo": map[string]string{
                        "t": urlTimeExpire,
                },
        })

        // Sign and get the complete encoded token as a string using the secret
        tokenString, err := token.SignedString(key)

        fmt.Println(tokenString, err)
}
```

## C# 署名の例


[jose-jwt](https://github.com/dvsekhvalnov/jose-jwt) を使用して署名を計算します。NuGetコマンド`Install-Package jose-jwt`を使用してインストールしてください。

```C#
using System;
using System.Text;
using System.Collections.Generic;
using Jose;

public class Program
{
        public static void Main()
        {
                var appId = 1255566655; // ユーザー appid
                var fileId = "4564972818519602447"; // ターゲット FileId
                var currentTime = DateTimeOffset.UtcNow.ToUnixTimeSeconds();
                var psignExpire = currentTime + 3600; // 有効期限は、1hなど任意に設定できます
                var urlTimeExpire = psignExpire.ToString("X4"); // 有効期限は、1hなどの16進文字列で任意に設定できます
                var key = "24FEQmTzro4V5u3D5epW";
                var keyBytes = Encoding.ASCII.GetBytes(key);
                var payload = new Dictionary<string, object>()
                {
                        {"appId", appId}, 
                        {"fileId", fileId}, 
                        {"currentTimeStamp", currentTime}, 
                        {"expireTimeStamp", psignExpire}, 
                        {"urlAccessInfo", new Dictionary<string, object>()
                                {
                                        {"t", urlTimeExpire}
                                }
                        }
                };
                string token = Jose.JWT.Encode(payload, keyBytes, JwsAlgorithm.HS256);
                Console.WriteLine(token);
        }
}
```


## PHP署名の例

[php-jwt](https://github.com/firebase/php-jwt) を使用して署名を計算します。コマンド`composer require firebase/php-jwt`を使用してインストールしてください。

```php
<?php
require 'vendor/autoload.php';
use \Firebase\JWT\JWT;

$appId = 1255566655; // ユーザー appid
$fileId = "4564972818519602447"; // ターゲット FileId
$currentTime = time();
$psignExpire = $currentTime + 3600; // 有効期限は、1hなど任意に設定できます
$urlTimeExpire = dechex($psignExpire); // 有効期限は、1hなどの16進文字列で任意に設定できます
$key = "24FEQmTzro4V5u3D5epW";

$payload = array(
    "appId" => $appId,
    "fileId" => $fileId,
    "currentTimeStamp" => $currentTime,
    "expireTimeStamp" => $psignExpire,
    "urlAccessInfo" => array(
        "t" => $urlTimeExpire
    )
);

$jwt = JWT::encode($payload, $key, 'HS256');
print_r($jwt);
?>
```

## Node.js署名の例


[jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) を使用して署名を計算します。コマンド`npm install jsonwebtoken`を使用してインストールしてください。
```node
var jwt = require('jsonwebtoken');

var appId = 1255566655 // ユーザー appid
var fileId = "4564972818519602447" // ターゲット FileId
var currentTime = Math.floor(Date.now()/1000)
var psignExpire = currentTime + 3600 // 有効期限は、1hなど任意に設定できます
var urlTimeExpire = psignExpire.toString(16) // 有効期限は、1hなどの16進文字列で任意に設定できます
var key = '24FEQmTzro4V5u3D5epW'

var payload = {
        appId: appId,
        fileId: fileId,
        currentTimeStamp: currentTime,
        expireTimeStamp: psignExpire,
        urlAccessInfo: {
                t: urlTimeExpire
        }
}
var token = jwt.sign(payload, key);
console.log(token);
```



