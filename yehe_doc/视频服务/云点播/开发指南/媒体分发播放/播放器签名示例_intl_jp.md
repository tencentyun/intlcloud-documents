## Python署名の例
[pyjwt](https://github.com/jpadilla/pyjwt/) ライブラリを使用して署名を計算します。`pip install pyjwt`を使用してインストールしてください。

```python
#!/usr/bin/python
#coding=utf-8

import jwt

AppId = 1255566655
FileId = "4564972818519602447"
AudioVideoType = "RawAdaptive"
RawAdaptiveDefinition = 10
ImageSpriteDefinition = 10
CurrentTime = 1546340400
PsignExpire = 1546344000
UrlTimeExpire = "5c2b5640"
PlayKey = "TxtyhLlgo7J3iOADIron"

Original = {
    "appId": AppId,
    "fileId": FileId,
    "contentInfo": {
        "audioVideoType": AudioVideoType,
        "rawAdaptiveDefinition": RawAdaptiveDefinition,
        "imageSpriteDefinition": ImageSpriteDefinition
    },
    "currentTimeStamp": CurrentTime,
    "expireTimeStamp": PsignExpire,
    "urlAccessInfo": {
        "t": UrlTimeExpire
    }
}

Signature = jwt.encode(Original, PlayKey, algorithm='HS256')

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
        String AudioVideoType = "RawAdaptive";
        Integer RawAdaptiveDefinition = 10;
        Integer ImageSpriteDefinition = 10;
        Integer CurrentTime = 1589448067;
        Integer PsignExpire = 1589548067;
        String UrlTimeExpire = "5ebe9423‬";
        String PlayKey = "TxtyhLlgo7J3iOADIron";
        HashMap<String, Object> urlAccessInfo = new HashMap<String, Object>();
        urlAccessInfo.put("t", UrlTimeExpire);
        HashMap<String, Object> contentInfo = new HashMap<String, Object>();
        contentInfo.put("audioVideoType", AudioVideoType);
        contentInfo.put("rawAdaptiveDefinition", RawAdaptiveDefinition);
        contentInfo.put("imageSpriteDefinition", ImageSpriteDefinition);

        try {
            Algorithm algorithm = Algorithm.HMAC256(PlayKey);
            String token = JWT.create().withClaim("appId", AppId).withClaim("fileId", FileId)
                    .withClaim("contentInfo", contentInfo)
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

func main(){
        appId := 1255566655 // ユーザー appid
        fileId := "4564972818519602447" // ターゲット FileId
        audioVideoType := "RawAdaptive" // 再生するオーディオビデオのタイプ
        rawAdaptiveDefinition := 10 // 出力が許可される、暗号化されていないABSテンプレートID
        imageSpriteDefinition := 10 // プログレスバープレビュー用のスプライトイメージテンプレートID
        currentTime := time.Now().Unix()
        psignExpire := currentTime + 3600 // 有効期限は、1hなど任意に設定できます
        urlTimeExpire := strconv.FormatInt(psignExpire, 16) // 有効期限は、1hなどの16進文字列で任意に設定できます
        playKey := []byte("TxtyhLlgo7J3iOADIron")

        // Create a new token object, specifying signing method and the claims
        // you would like it to contain.
        token := jwt.NewWithClaims(jwt.SigningMethodHS256, jwt.MapClaims{
                "appId":            appId,
                "fileId":           fileId,
                "contentInfo": {
                        "audioVideoType"=> audioVideoType,
                        "rawAdaptiveDefinition"=> rawAdaptiveDefinition,
                        "imageSpriteDefinition"=> imageSpriteDefinition,
                },
                "currentTimeStamp": currentTime,
                "expireTimeStamp":  psignExpire,
                "urlAccessInfo": map[string]string{
                        "t": urlTimeExpire,
                },
        })

        // Sign and get the complete encoded token as a string using the secret
        tokenString, err := token.SignedString(playKey)

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
                var audioVideoType = "RawAdaptive"; // 再生するオーディオビデオのタイプ
                var rawAdaptiveDefinition = 10; // 出力が許可される、暗号化されていないABSテンプレートID
                var imageSpriteDefinition = 10; // プログレスバープレビュー用のスプライトイメージテンプレートID
                var currentTime = DateTimeOffset.UtcNow.ToUnixTimeSeconds();
                var psignExpire = currentTime + 3600; // 有効期限は、1hなど任意に設定できます
                var urlTimeExpire = psignExpire.ToString("X4"); // 有効期限は、1hなどの16進文字列で任意に設定できます
                var playKey = "TxtyhLlgo7J3iOADIron";
                var playKeyBytes = Encoding.ASCII.GetBytes(playKey);
                var payload = new Dictionary<string, object>()
                {
                        {"appId", appId},
                        {"fileId", fileId},
                        {"contentInfo": new Dictionary<string, object>()
                                {
                                        {"audioVideoType": audioVideoType},
                                        {"rawAdaptiveDefinition": rawAdaptiveDefinition},
                                        {"imageSpriteDefinition": imageSpriteDefinition}
                                }
                        },
                        {"currentTimeStamp", currentTime},
                        {"expireTimeStamp", psignExpire},
                        {"urlAccessInfo", new Dictionary<string, object>()
                                {
                                        {"t", urlTimeExpire}
                                }
                        }
                };
                string token = Jose.JWT.Encode(payload, playKeyBytes, JwsAlgorithm.HS256);
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
$audioVideoType = "RawAdaptive"; // 再生するオーディオビデオのタイプ
$rawAdaptiveDefinition = 10; // 出力が許可される、暗号化されていないABSテンプレートID
$imageSpriteDefinition = 10; // プログレスバープレビュー用のスプライトイメージテンプレートID
$currentTime = time();
$psignExpire = $currentTime + 3600; // 有効期限は、1hなど任意に設定できます
$urlTimeExpire = dechex($psignExpire); // 有効期限は、1hなどの16進文字列で任意に設定できます
$playKey = "TxtyhLlgo7J3iOADIron";

$payload = array(
    "appId" => $appId,
    "fileId" => $fileId,
    "contentInfo" => array(
        "audioVideoType": $audioVideoType,
				"rawAdaptiveDefinition": $rawAdaptiveDefinition,
				"imageSpriteDefinition": $imageSpriteDefinition
    ),
    "currentTimeStamp" => $currentTime,
    "expireTimeStamp" => $psignExpire,
    "urlAccessInfo" => array(
        "t" => $urlTimeExpire
    )
);

$jwt = JWT::encode($payload, $playKey, 'HS256');
print_r($jwt);
?>
```

## Node.js署名の例


[jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) を使用して署名を計算します。コマンド`npm install jsonwebtoken`を使用してインストールしてください。
```javascript
var jwt = require('jsonwebtoken');

var appId = 1255566655 // ユーザー appid
var fileId = "4564972818519602447" // ターゲット FileId
var audioVideoType = "RawAdaptive" // 再生するオーディオビデオのタイプ
var rawAdaptiveDefinition = 10 // 出力が許可される、暗号化されていないABSテンプレートID
var imageSpriteDefinition = 10 // プログレスバープレビュー用のスプライトイメージテンプレートID
var currentTime = Math.floor(Date.now()/1000)
var psignExpire = currentTime + 3600 // 有効期限は、1hなど任意に設定できます
var urlTimeExpire = psignExpire.toString(16) // 有効期限は、1hなどの16進文字列で任意に設定できます
var playKey = 'TxtyhLlgo7J3iOADIron'

var payload = {
        appId: appId,
        fileId: fileId,
        contentInfo: {
                audioVideoType: audioVideoType,
                rawAdaptiveDefinition: rawAdaptiveDefinition,
                imageSpriteDefinition: imageSpriteDefinition
        },
        currentTimeStamp: currentTime,
        expireTimeStamp: psignExpire,
        urlAccessInfo: {
                t: urlTimeExpire
        }
}
var token = jwt.sign(payload, playKey);
console.log(token);
```
