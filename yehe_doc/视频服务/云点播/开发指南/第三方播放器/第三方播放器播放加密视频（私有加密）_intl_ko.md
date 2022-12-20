# 목적

본문은 타사 플레이어를 사용하여 VOD의 암호화된(SimpleAES) 비디오를 재생하는 방법을 보여줍니다.

# 개요

타사 플레이어를 사용하여 암호화된 비디오를 해독하고 재생하려면 재생 정보를 가져와야 합니다.

다음 정보가 필요합니다.

- DrmToken(복호화 키를 얻는 데 사용됨)
- 비디오 콘텐츠의 URL

## 워크플로우

### 개인 암호화

![](https://qcloudimg.tencent-cloud.cn/raw/0869fb5666a8d93a57ae0202f7468c97.jpg)

- 재생 정보 및 서명 가져오기
  인증 성공 후 APP 서버는 재생 정보 및 서명(DrmToken)을 클라이언트로 보냅니다.

- 비디오를 다운로드하고 키 가져오기

  획득한 재생 정보(DrmToken 및 콘텐츠 URL)를 기반으로 재생 URL이 생성됩니다. 플레이어가 비디오를 재생하려고 하면 키 가져오기 요청이 자동으로 전송됩니다.

  키 보호가 활성화되면 VOD의 키 배포 서비스가 콘텐츠 키를 암호화합니다. 예를 들어 보호 모드가 'sha256'인 경우 키 배포 서비스는 대칭 키를 사용하여 콘텐츠 키를 암호화합니다.
  
  키 보호가 비활성화된 경우 키 배포 서비스는 콘텐츠 키를 직접 보냅니다.

- 비디오 해독 및 재생

  키 보호가 활성화된 경우 APP 클라이언트는 수신된 콘텐츠 키를 해독해야 합니다. 예를 들어 보호 모드가 'sha256'인 경우 클라이언트는 비디오를 해독하고 재생하기 전에 얻은 키 정보를 해독하기 위해 대칭 키를 사용해야 합니다.

# DrmToken 생성

DrmToken은 본질적으로 [Json Web Token(JWT)](https://jwt.io/introduction)의 변형입니다. 또한 Header, PayLoad 및 Signature의 세 부분으로 구성됩니다. 하지만 JWT와 달리 VOD는 세 부분을 ~로 연결합니다.

### Header

Header는 JSON 형식이며 JWT에서 사용하는 알고리즘 정보를 나타냅니다. 그 내용은 다음과 같이 수정됩니다.

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

### PayLoad

PayLoad는 JSON 형식이며 플레이어 서명 매개변수를 포함합니다. 예시는 다음과 같습니다.

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "protectSchema": "sha256",
  "issuer": "client"
}
```

#### PayLoad 매개변수

| **매개변수**       | **유형**   | **필수 여부** | **설명**                                                     |
| ---------------- | ---------- | ------------ | ------------------------------------------------------------ |
| type             | string     | Yes           | 서명 유형. `DrmToken`을 입력합니다.                               |
| appId            | int64      | Yes           | AppId.                                                      |
| fileId           | string     | Yes           | 파일 Id.                                                     |
| issuer       | string | Yes       | 발행자. `client`를 입력합니다.                                |
| currentTimeStamp | int64      | Yes           | 현재 시간(Unix 타임스탬프).                                           |
| expireTimeStamp  | int64      | No           | 만료 시간(Unix 타임스탬프). 이를 지정하지 않으면 서명이 만료되지 않습니다.      |
| random           | int64      | No           | 임의의 숫자.                                                     |
| protectSchema    | string     | No           | 보호 모드. 이 매개변수는 암호화 체계가 'SimpleAES'인 경우에만 유효합니다. 이 매개변수를 `sha256`으로 설정하면 `sha256(pkey)`가 대칭 키로 사용되어 콘텐츠 키를 암호화합니다(`pkey`는 재생 키이고 `sha256`은 SHA256 알고리즘을 나타냅니다). |

### Signatrue

#### 계산 방식

`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), pkey)`

?HMACSHA256 알고리즘에 대한 자세한 내용은 [RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3)을 참고하십시오. base64UrlEncode에 대한 자세한 내용은 [RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7)를 참고하십시오.

VOD 콘솔에서 재생 키(pkey)를 볼 수 있습니다.

왼쪽 사이드바에서 **배포 및 재생**>**기본 배포 도메인**을 선택합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/d3bebcb860f8c9900fca9a645a0879be.png)

### DrmToken 예시

- `Header`:

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

인코딩됨(base64UrlEncode): `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.

- `PayLoad`:

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "protectSchema": "sha256",
  "issuer": "client"
}
```

인코딩됨(base64UrlEncode): `eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ`.

- `Signature`: `dK42jB0KP4sXCd7Dunng9AcQ2WlnANuB87PwxmTc3_g`. `pkey`(값은 `JduzsUuRvGVPRHvIYwLv`)를 사용하여 생성됩니다.

`Header`, `PayLoad`, `Signature`를 `~`로 연결하면 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ`인 `DrmToken`을 얻게 됩니다.

# 재생 URL 생성

- [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181)를 호출하여 비디오 콘텐츠의 URL(`MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url `의 값)을 가져옵니다.

- KEY 링크 도용 방지를 활성화한 경우 [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986)를 참고하여 링크 도용 방지 서명이 포함된 URL을 생성합니다.

- `SimpleAES` 암호화 동영상의 경우 재생 URL 형식은 다음과 같습니다.

  원본 비디오 URL이 `http(s)://xxx.com/xxx/xxx/test.m3u8`이라고 가정합니다.

  재생 URL은 `http(s)://xxx.com/xxx/xxx/voddrm.token.<DrmToken>.test.m3u8`입니다.

  접두어 `voddrm.token.`이 파일 이름에 추가되고 `<DrmToken>`의 값은 위에서 생성된 `DrmToken`입니다.
  
### 재생 URL 예시

동영상 콘텐츠의 URL이 ` https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff `라고 가정합니다

`DrmToken`은 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ`입니다

재생 URL은 `https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/voddrm.token.eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ.adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff`입니다

# 타사 플레이어를 사용하여 비디오 재생

재생 URL이 있으면 타사 플레이어를 사용하여 동영상을 재생할 수 있지만 VOD의 키 배포 서비스에서 얻은 콘텐츠 키를 암호화해야 합니다.

플레이어는 비디오 재생을 시도할 때 콘텐츠 키(`CipherContentKey`)에 대한 요청을 보냅니다. 요청 URL은 `m3u8` 파일에서 `#EXT-X-KEY`로 지정됩니다. 아래는 예시입니다.

```text
#EXT-X-KEY:METHOD=AES-128,URI="https://drm.vod2.myqcloud.com/getlicense/v1?drmType=SimpleAES&token=<DrmToken>"
```

키를 해독하는 방법:

- 대칭 키 생성(`SymmetricKey`):

  `SymmetricKey=SHA256(pkey)`

  `SHA256`은 `SHA256` 알고리즘을 나타내고 `pkey`는 재생 키입니다.

- 콘텐츠 키(`ContentKey`)를 해독합니다.

  `ContentKey=AES-CBC-Descrypt(CipherContentKey, SymmetricKey, IV)`

  'CipherContentKey'는 암호화된 콘텐츠 키로 VOD의 키 분배 서비스에서 반환되며 IV 데이터를 포함하지 않습니다. 'AES-CBC-Descrypt'는 AES-CBC 알고리즘을 나타냅니다. IV는 `0x00000000000000000000000000000000`인 초기화 벡터입니다.

## 복호화 예시

가정:

- 재생 키(`pkey`)는 `JduzsUuRvGVPRHvIYwLv`이고, 대칭 키(`SymmetricKey`)는 `0xece0bae38fbbd66f79c62acefb9ea994dc834d79b45cc4556962d9f00508b9b3 `(32 Bytes)입니다.
- 암호화된 콘텐츠 키(`CipherContentKey`)는 0x68addf7984478a3e4797d3a13ecbb6fb `(16 Bytes)입니다.
- IV는 항상 ` 0x00000000000000000000000000000000`(16 Bytes)입니다.

해독된 콘텐츠 키(`ContentKey`)는 `0xbed3747b8510b040826163c04956a4c1`(16 Bytes)입니다.

# 요약

이제 타사 플레이어를 사용하여 암호화된 VOD 비디오를 재생하는 방법을 마스터했습니다.