# 목표

본문은 타사 플레이어를 사용하여 VOD의 암호화된(Widevine, FairPlay) 비디오를 재생하는 방법을 소개합니다.

# 개요

타사 플레이어를 사용하여 암호화된 비디오를 해독하고 재생하려면 재생 정보를 가져와야 합니다.

다음 재생 정보가 필요합니다.

- Widevine
  - DrmToken  (재생 License를 얻기 위해 사용됨)
  - 동영상 콘텐츠의 URL
  - 재생 License의 URL
- FairPlay
  - DrmToken   (재생 License를 얻기 위해 사용됨)
  - 동영상 콘텐츠의 URL
  - 재생 License의 URL
  - 인증서의 URL(Certificate URL)

## 워크플로우

### 상업용 DRM(Widevine 및 FairPlay)

![](https://qcloudimg.tencent-cloud.cn/raw/c77d070232e66d1eef6a6a91b5e8561e.jpg)

- 재생 정보 및 서명 가져오기
  인증 성공 후 APP 서버는 재생 정보 및 서명(DrmToken)을 클라이언트로 보냅니다.

- 비디오 및 인증서 다운로드 및 License 요청

  플레이어가 비디오를 재생하려고 하면 License 및 인증서에 대한 요청이 자동으로 전송됩니다.

- 비디오 해독 및 재생

  플레이어는 획득한 License를 사용하여 비디오를 해독하고 재생합니다.

# DrmToken 생성

DrmToken은 본질적으로 [Json Web Token](https://jwt.io/introduction)의 변형입니다. 또한 Header, PayLoad 및 Signature의 세 부분으로 구성됩니다. 하지만 JWT와 달리 VOD는 세 부분을 ~로 연결합니다.

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
| type             | string     | Yes           | 서명 유형. `DrmToken`을 입력합니다.                               |
| appId            | int64      | Yes           | AppId.                                                      |
| fileId           | string     | Yes           | 파일 Id.                                                     |
| issuer       | string | Yes       | 발행자. `client`를 입력합니다.                                 |
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

- `Signature`: `muHWnxX9dXsUAkCzw4uXGcvwKDoA19BkR-hCJVrXyvY`. `pkey`(값은 `JduzsUuRvGVPRHvIYwLv`)를 사용하여 생성됩니다.

`Header`, `PayLoad`, `Signature`를 `~`로 연결하면 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`인 `DrmToken`을 얻게 됩니다.

# 재생 URL 생성

- [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181)를 호출하여 비디오 콘텐츠의 URL(`MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url `의 값)을 가져옵니다.

- KEY 링크 도용 방지를 활성화한 경우 [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986)를 참고하여 링크 도용 방지 서명이 포함된 URL을 생성합니다.


# 라이선스 URL 생성

상업용 DRM의 경우 플레이어에서 암호화된 비디오를 재생하려면 License가 필요합니다.

## 요청

요청 URI:

- Widevine:  `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2`
- FairPlay: `https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2`

요청 방법: `POST`

요청 매개변수:

| **매개변수**        | **설명**                                                     |
| ---------------- | ------------------------------------------------------------ |
| drmToken     | 인증 토큰입니다. |

>? DRM 클라이언트 모듈에서 생성한 라이선스 요청 데이터(License Request Data)를 요청 BODY에 포함합니다.

## 응답

- 요청이 성공하면 `Status Code`는 200이 되고 License의 이진법 데이터가 반환됩니다.

- 요청이 실패하면 `Status Code`는 200 이외의 값이 됩니다.

### Status Code
| **Status Code**        | **설명**                                                     |
| ---------------- | ------------------------------------------------------------ |
| 200     | 요청 성공. |
| 400     | 매개변수 오류. |
| 403     | 인증 실패. |
| 500     | 내부 오류. |

## License 요청 예시

`Widevine`에 대한 License 요청 URL:  `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`

# License URL 가져오기

`FairPlay`로 암호화된 비디오를 재생하려면 `FairPlay` 인증서를 [신청](https://www.tencentcloud.com/document/product/266/46643)하고 인증서 정보를 VOD에 [제출](https://www.tencentcloud.com/document/product/266/49668)해야 합니다. `Widevine`에는 License URL이 필요하지 않습니다.

정보를 제출하면 VOD 콘솔에서 License URL을 볼 수 있습니다. 각 서브 애플리케이션에는 하나의 License URL만 있습니다.

# 타사 플레이어를 사용하여 비디오 재생

재생 URL, License URL 및 인증서 URL이 있으면 타사 플레이어를 사용하여 DRM 암호화 비디오를 재생할 수 있습니다.

# 요약

이제 타사 플레이어를 사용하여 암호화된 VOD 비디오를 재생하는 방법을 마스터했습니다.