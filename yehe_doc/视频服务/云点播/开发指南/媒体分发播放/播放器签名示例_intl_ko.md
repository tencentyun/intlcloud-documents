## Python 서명 예시
[pyjwt](https://github.com/jpadilla/pyjwt/) 라이브러리를 사용하여 서명을 계산합니다. `pip install pyjwt` 명령을 실행하여 설치할 수 있습니다.

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

## Java의 서명 예시
[java-jwt](https://github.com/auth0/java-jwt) 라이브러리를 사용하여 서명을 계산합니다.

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
        HashMap<String, String> urlAccessInfo = new HashMap<String, String>();
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

## Go 서명 예시

[jwt-go](https://github.com/dgrijalva/jwt-go) 라이브러리를 사용하여 서명을 계산합니다. `go get github.com/dgrijalva/jwt-go` 명령을 실행하여 설치할 수 있습니다.

```go

package main

import (
        "fmt"
        "time"
        "strconv"
        "github.com/dgrijalva/jwt-go"
)

func main(){
        appId := 1255566655 // 사용자 appid
        fileId := "4564972818519602447" // 타깃 FileId
        audioVideoType := "RawAdaptive" // 재생되는 오디오/비디오 유형
        rawAdaptiveDefinition := 10 // 암호화되지 않은 어댑티브 비트레이트 템플릿 ID 허용
        imageSpriteDefinition := 10 // 진행률 표시줄 미리보기 생성에 사용되는 이미지 스프라이트 템플릿 ID
        currentTime := time.Now().Unix()
        psignExpire := currentTime + 3600 // 필요에 따라 만료 시간을 설정합니다(예시: 1h).
        urlTimeExpire := strconv.FormatInt(psignExpire, 16) // 필요에 따라 만료 시간을 16진수 문자열로 설정합니다(예시: 1h).
        playKey := []byte("TxtyhLlgo7J3iOADIron")

        // Create a new token object, specifying signing method and the claims
        // you would like it to contain.
        token := jwt.NewWithClaims(jwt.SigningMethodHS256, jwt.MapClaims{
                "appId":            appId,
                "fileId":           fileId,
                "contentInfo": {
                        "audioVideoType": audioVideoType,
                        "rawAdaptiveDefinition": rawAdaptiveDefinition,
                        "imageSpriteDefinition": imageSpriteDefinition,
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

## C# 서명 예시


[jose-jwt](https://github.com/dvsekhvalnov/jose-jwt) 라이브러리를 사용하여 서명을 계산합니다. NuGet의 `Install-Package jose-jwt` 명령을 실행하여 설치할 수 있습니다.

```C#
using System;
using System.Text;
using System.Collections.Generic;
using Jose;

public class Program
{
        public static void Main()
        {
                var appId = 1255566655; // 사용자 appid
                var fileId = "4564972818519602447"; // 타깃 FileId
                var audioVideoType = "RawAdaptive"; // 재생되는 오디오/비디오 유형
                var rawAdaptiveDefinition = 10; // 암호화되지 않은 어댑티브 비트레이트 템플릿 ID 허용
                var imageSpriteDefinition = 10; // 진행률 표시줄 미리보기 생성에 사용되는 이미지 스프라이트 템플릿 ID
                var currentTime = DateTimeOffset.UtcNow.ToUnixTimeSeconds();
                var psignExpire = currentTime + 3600; // 필요에 따라 만료 시간을 설정합니다(예시: 1h).
                var urlTimeExpire = psignExpire.ToString("X4"); // 필요에 따라 만료 시간을 16진수 값으로 설정합니다(예시: 1h).
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


## PHP 서명 예시

[php-jwt](https://github.com/firebase/php-jwt) 라이브러리를 사용하여 서명을 계산합니다. `composer require firebase/php-jwt` 명령을 실행하여 설치할 수 있습니다.

```php
<?php
require 'vendor/autoload.php';
use \Firebase\JWT\JWT;

$appId = 1255566655; // 사용자 appid
$fileId = "4564972818519602447"; // 타깃 FileId
$audioVideoType = "RawAdaptive"; // 재생되는 오디오/비디오 유형
$rawAdaptiveDefinition = 10; // 암호화되지 않은 어댑티브 비트레이트 템플릿 ID 허용
$imageSpriteDefinition = 10; // 진행률 표시줄 미리보기 생성에 사용되는 이미지 스프라이트 템플릿 ID
$currentTime = time();
$psignExpire = $currentTime + 3600; // 필요에 따라 만료 시간을 설정합니다(예시: 1h).
$urlTimeExpire = dechex($psignExpire); // 필요에 따라 만료 시간을 16진수 문자열로 설정합니다(예시: 1h).
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

## Node.js 서명 예시


[jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) 라이브러리를 사용하여 서명을 계산합니다. `npm install jsonwebtoken` 명령을 실행하여 설치할 수 있습니다.
```javascript
var jwt = require('jsonwebtoken');

var appId = 1255566655 // 사용자 appid
var fileId = "4564972818519602447" // 타깃 FileId
var audioVideoType = "RawAdaptive" // 재생되는 오디오/비디오 유형
var rawAdaptiveDefinition = 10 // 암호화되지 않은 어댑티브 비트레이트 템플릿 ID 허용
var imageSpriteDefinition = 10 // 진행률 표시줄 미리보기 생성에 사용되는 이미지 스프라이트 템플릿 ID
var currentTime = Math.floor(Date.now()/1000)
var psignExpire = currentTime + 3600 // 필요에 따라 만료 시간을 설정합니다(예시: 1h).
var urlTimeExpire = psignExpire.toString(16) // 필요에 따라 만료 시간을 16진수 문자열로 설정합니다(예시: 1h).
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
