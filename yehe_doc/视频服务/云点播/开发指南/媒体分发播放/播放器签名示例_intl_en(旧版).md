## Sample Code for Calculating Signature for Python
Use the [pyjwt](https://github.com/jpadilla/pyjwt/) library to calculate the signature. You can install it by running the `pip install pyjwt` command.

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

## Sample Code for Calculating Signature for Java
Use the [java-jwt](https://github.com/auth0/java-jwt) library to calculate the signature.

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

## Sample Code for Calculating Signature for Go

Use the [jwt-go](https://github.com/dgrijalva/jwt-go) library to calculate the signature. You can install it by running the `go get github.com/dgrijalva/jwt-go` command.

```go

package main

import (
        "fmt"
        "time"
        "strconv"
        "github.com/dgrijalva/jwt-go"
)

func main(){
        appId := 1255566655 // User `appid`
        fileId := "4564972818519602447" // Target `FileId`
        currentTime := time.Now().Unix()
        psignExpire := currentTime + 3600 // Set the expiration time as needed, such as in 1 hour
        urlTimeExpire := strconv.FormatInt(psignExpire, 16) // Set the expiration time to a hexadecimal string as needed, such as in 1 hour
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

## Sample Code for Calculating Signature for C#


Use the [jose-jwt](https://github.com/dvsekhvalnov/jose-jwt) library to calculate the signature. You can install it by running the `Install-Package jose-jwt` command of NuGet.

```C#
using System;
using System.Text;
using System.Collections.Generic;
using Jose;

public class Program
{
        public static void Main()
        {
                var appId = 1255566655; // User `appid`
                var fileId = "4564972818519602447"; // Target `FileId`
                var currentTime = DateTimeOffset.UtcNow.ToUnixTimeSeconds();
                var psignExpire = currentTime + 3600; // Set the expiration time as needed, such as in 1 hour
                var urlTimeExpire = psignExpire.ToString("X4"); // Set the expiration time to a hexadecimal value as needed, such as in 1 hour
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


## Sample Code for Calculating Signature for PHP

Use the [php-jwt](https://github.com/firebase/php-jwt) library to calculate the signature. You can install it by running the `composer require firebase/php-jwt` command.

```php
<?php
require 'vendor/autoload.php';
use \Firebase\JWT\JWT;

$appId = 1255566655; // User `appid`
$fileId = "4564972818519602447"; // Target `FileId`
$currentTime = time();
$psignExpire = $currentTime + 3600; // Set the expiration time as needed, such as in 1 hour
$urlTimeExpire = dechex($psignExpire); // Set the expiration time to a hexadecimal string as needed, such as in 1 hour
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

## Sample Code for Calculating Signature for Node.js


Use the [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) library to calculate the signature. You can install it by running the `npm install jsonwebtoken` command.
```node
var jwt = require('jsonwebtoken');

var appId = 1255566655 // User `appid`
var fileId = "4564972818519602447" // Target `FileId`
var currentTime = Math.floor(Date.now()/1000)
var psignExpire = currentTime + 3600 // Set the expiration time as needed, such as in 1 hour
var urlTimeExpire = psignExpire.toString(16) // Set the expiration time to a hexadecimal string as needed, such as in 1 hour
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



