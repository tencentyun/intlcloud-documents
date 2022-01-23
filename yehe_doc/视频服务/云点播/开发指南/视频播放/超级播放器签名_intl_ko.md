Superplayer 서명은 App 재생 서비스가 클라이언트에 재생 권한을 부여하는 데 사용됩니다. App 재생 서비스를 통해 클라이언트가 재생할 수 있는 경우 아래 5단계와 같이 유효한 서명을 클라이언트에 배포합니다. 클라이언트는 서명의 유효 기간 내에서 비디오를 재생할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="700" />

>! 다음과 같은 경우 App 클라이언트는 비디오를 재생하기 위해 Superplayer 서명이 필요합니다.
>- 도메인 이름에  [KEY 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986)가 활성화되어 있습니다.
>- default 이외의 [Superplayer 설정](https://intl.cloud.tencent.com/document/product/266/38296)이 사용됩니다.
>- [암호화](https://intl.cloud.tencent.com/document/product/266/38294)된 비디오가 재생됩니다.

Superplayer 서명 매개변수 및 생성 규칙은 다음과 같습니다.

## 서명 매개변수

| 매개변수 이름 | 필수 | 유형 | 설명 |
| -- | -- | -- | -- |
| appId | Yes | Integer | 계정 appId|
| fileId | Yes | String | 파일 ID|
| currentTimeStamp | Yes | Integer | 서명의 현재 Unix 타임스탬프입니다.|
| expireTimeStamp | No | Integer | 서명의 만료 Unix 타임스탬프입니다. 이 매개변수가 비어 있으면 서명이 만료되지 않습니다. |
| pcfg | No | String | 사용할 Superplayer 설정 이름입니다. default 설정을 사용하려면 이 매개변수를 비워둡니다.|
| urlAccessInfo | No | Object | [UrlAccessInfo 유형](#p1)에 있는 재생 링크의 링크 도용 방지 설정 매개변수입니다. |
| drmLicenseInfo | No | Object | [DrmLicenseInfo 유형](#p2)에 있는 암호화된 콘텐츠의 주요 설정 매개변수입니다. |

<span id = "p1"></span>
#### UrlAccessInfo 유형

| 매개변수 이름 | 필수 | 유형 | 설명 |
| -- | -- | -- | -- |
| t | No | String | <ul style="margin:0;"><li>링크 만료 시간을 나타내는 16진수 문자열.</li><li>특정 설명 및 유효한 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 t 매개변수를 참고하십시오.</li><li>이 매개변수를 비워두면 링크가 만료되지 않습니다.</li>|
| exper | No | Integer | <ul style="margin:0;"> <li>미리보기 시간(초 단위, 십진수). </li><li>미리보기 시간을 지정하려면 30초 이상이어야 합니다.</li><li>특정 설명 및 유효한 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 exper 매개변수를 참고하십시오.</li> |
| rlimit | No | Integer | <ul style="margin:0;"><li>재생에 허용되는 서로 다른 IP를 가진 클라이언트의 최대 십진수</li><li>구체적인 설명과 유효 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 rlimit 매개변수를 참고하십시오.</li> |
| us | No | String | <ul style="margin:0;"><li>링크를 고유하게 식별할 수 있는 링크 ID</li><li>구체적인 설명과 유효한 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 us 매개변수를 참고하십시오.</li> |

<span id = "p2"></span>
#### DrmLicenseInfo 유형

| 매개변수 이름 | 필수 | 유형 | 설명 |
| -- | -- | -- | -- |
| expireTimeStamp | No | Integer | Unix 키 만료 타임스탬프. 이 매개변수를 비워두면 서명이 만료되지 않습니다. |

>?
>- [서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987)을 사용한 경우 서브 애플리케이션의 AppId를 appId 매개변수로 설정합니다.
>- 서명 매개변수의 `t`, `exper`, `rlimit` 및 `us`의 설명 및 유효한 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 설명과 동일합니다.

## 서명 계산

VOD Superplayer는 Header, PayLoad 및 Key를 기반으로 계산 및 형성되는 디지털 토큰인 [JWT](https://tools.ietf.org/html/rfc7519)(JSON Web Token)를 사용합니다.

### Header

Header는 JSON 형식으로 JWT에서 사용하는 알고리즘의 정보를 나타내며 그 내용은 다음과 같이 고정됩니다.

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### PayLoad

PayLoad는 JSON 형식이며 Superplayer 서명 매개변수를 나타냅니다. 예시는 다음과 같습니다.

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546340400,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

### Key

Key는 서명 계산 중에 사용되는 키이며 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 KEY 매개변수와 동일합니다.

### 계산 공식

1. Signature 계산:
`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), KEY)`
2. Token 계산:
`Token = base64UrlEncode(Header) + '.' + base64UrlEncode(Payload) + '.' + base64UrlEncode(Signature)`
최종 Token, 즉 VOD Superplayer 서명입니다.

>?HMACSHA256에 대한 자세한 내용은 [RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3)을 참고하십시오. base64UrlEncode에 대한 자세한 내용은 [RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7)를 참고하십시오.

VOD는 편리한 서명 계산 및 확인을 위해 온라인 서명 생성 및 확인 툴을 제공합니다.
* [Superplayer - 서명 생성 도구](https://vods.cloud.tencent.com/signature/super-player-sign.html)를 사용하여 서명을 빠르게 생성합니다.
* [Superplayer - 서명 확인 도구](https://vods.cloud.tencent.com/signature/super-player-check-sign.html)를 사용하여 서명을 빠르게 확인합니다.

### 과금 예시

예를 들어, appId가 `1255566655`이고, fileId가 `4564972818519602447`이며, 다음 속성을 가진 사용자의 비디오에 대해 Superplayer 서명이 생성됩니다.

* 활성화된 링크 도용 방지 KEY는 `24FEQmTzro4V5u3D5epW`입니다.
* 사용자 정의 Superplayer 설정이 사용되며 이름은 `MyCfg`입니다.
* 플레이어 서명의 배포 시간은 2019/1/1 19:00:00이며 해당 Unix 시간은 `1546340400`입니다.
* 플레이어 서명의 만료 시간은 2019/1/1 20:00:00이며 해당 Unix 시간은 `1546344000`입니다.
* 링크 도용 방지 만료 시간은 2019/1/1 20:00:00이며 해당 Unix 시간은 `5c2b5640`입니다.
* 최대 3개의 다른 IP를 허용하는 재생 URL입니다.
* 생성된 랜덤 문자열은 `72d4cd1101`입니다.

서명은 다음과 같이 생성됩니다.
1. 다음은 Header의 내용입니다.
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
base64UrlEncode를 통해 처리된 결과는 다음과 같습니다.
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
2. 다음은 Payload의 내용입니다.
```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546340400,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```
base64UrlEncode를 통해 처리된 결과는 다음과 같습니다.
```
eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ
```
3. `24FEQmTzro4V5u3D5epW`를 KEY로 사용하여 HMAC 계산을 수행하면 Signature는 다음과 같습니다.
`TRdfy-ctQFRDJzknfKsT0di5tEaweAVumOgxsA8Qd-8`.
4. 최종 Token은 다음과 같습니다.
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.TRdfy-ctQFRDJzknfKsT0di5tEaweAVumOgxsA8Qd-8
```

## 코드 예시

VOD는 Python, Java, Go, C#, PHP, Node.js 등 다양한 프로그래밍 언어에 대한 Superplayer 서명의 코드 예시를 제공합니다. 자세한 내용은 [Superplayer 서명 - 서명 예시](https://intl.cloud.tencent.com/document/product/266/38096)를 참고하십시오.
