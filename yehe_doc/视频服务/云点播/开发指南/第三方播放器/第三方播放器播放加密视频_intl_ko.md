# 목표

본문은 타사 플레이어를 사용하여 VOD의 암호화된(SimpleAES) 비디오를 재생하는 방법을 소개합니다.

# 개요

타사 플레이어를 사용하여 암호화된 비디오를 해독하고 재생하려면 재생 정보를 가져와야 합니다.

다음 정보가 필요합니다.

- DrmToken (복호화 키를 얻는 데 사용됨).
- 동영상 콘텐츠의 URL

## 워크플로우

![](https://qcloudimg.tencent-cloud.cn/raw/0869fb5666a8d93a57ae0202f7468c97.jpg)

- 재생 정보 및 서명 가져오기
  인증 성공 후 APP 서버는 재생 정보 및 서명(DrmToken)을 클라이언트로 보냅니다.

- 비디오를 다운로드하고 키 가져오기

  획득한 재생 정보(DrmToken 및 콘텐츠 URL)를 기반으로 재생 URL이 생성됩니다. 플레이어가 비디오를 재생하려고 하면 키 가져오기 요청이 자동으로 전송됩니다.

- 비디오 해독 및 재생

  플레이어는 얻은 키를 사용하여 비디오를 해독하고 재생합니다.

# DrmToken 생성

DrmToken은 본질적으로 [Json Web Token](https://jwt.io/introduction)의 변형입니다. 또한 Header, PayLoad, Signature의 세 부분으로 구성됩니다. 하지만 JWT와 달리 VOD는 세 부분을 ~로 연결합니다.

### Header

Header는 JSON 형식으로 JWT에서 사용하는 알고리즘의 정보를 나타내며 그 내용은 다음과 같이 수정됩니다.

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

### PayLoad

PayLoad는 JSON 형식이며 Player 서명 매개변수를 포함합니다. 예시는 다음과 같습니다.

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "issuer": "client"
}
```

#### PayLoad 매개변수

| **매개변수**       | **유형**   | **필수 여부** | **설명**                                                     |
| ---------------- | ---------- | ------------ | ------------------------------------------------------------ |
| type             | string     |Yes           | 서명 유형. `DrmToken`을 입력합니다.                               |
| appId            | int64      | Yes           | AppId.                                                      |
| fileId           | string     | Yes           | 파일 Id.                                                     |
| issuer       | string | Yes       | 발행자. `client`를 입력합니다.                                |
| currentTimeStamp | int64      | Yes           | 현재 시간(Unix 타임스탬프).                                           |
| expireTimeStamp  | int64      | No           | 만료 시간(Unix 타임스탬프). 이를 지정하지 않으면 서명이 만료되지 않습니다.      |
| random           | int64      | No           | 임의의 숫자.                                                     |

### Signatrue

#### 계산 방식

`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), pkey)`

>? HMACSHA256 알고리즘에 대한 자세한 내용은 [RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3)을 참고하십시오. base64UrlEncode에 대한 자세한 내용은 [RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7)를 참고하십시오.

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
  "issuer": "client"
}
```

인코딩됨(base64UrlEncode): `eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9`.

- `Signature`: `NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`. `pkey`(값은 `JduzsUuRvGVPRHvIYwLv`)를 사용하여 생성됩니다.

`Header`, `PayLoad`, `Signature`를 `~`로 연결하면 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`인 `DrmToken`을 얻게 됩니다.

# 재생 URL 생성

- [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181)를 호출하여 비디오 콘텐츠의 URL(`MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url `의 값)을 가져옵니다.

- KEY 링크 도용 방지를 활성화한 경우 [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986)를 참고하여 링크 도용 방지 서명이 포함된 URL을 생성합니다.

- 재생 URL 생성:

  원본 비디오 URL이 `http(s)://xxx.com/xxx/xxx/test.m3u8`이라고 가정합니다.

  재생 URL은 `http(s)://xxx.com/xxx/xxx/voddrm.token.<DrmToken>.test.m3u8`입니다.

  접두어 `voddrm.token.`이 파일 이름에 추가되고 `<DrmToken>`의 값은 위에서 생성된 `DrmToken`입니다.

### 예시

동영상 콘텐츠의 URL이 ` https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff `라고 가정합니다

`DrmToken`은 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`입니다

재생 URL은 다음과 같습니다.

`https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/voddrm.token.eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY.adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff`

# 타사 플레이어를 사용하여 비디오 재생

재생 URL이 있으면 타사 플레이어를 사용하여 동영상을 재생할 수 있습니다.

# 요약

이제 타사 플레이어를 사용하여 암호화된 VOD 비디오를 재생하는 방법을 마스터했습니다.