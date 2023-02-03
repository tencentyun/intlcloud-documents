플레이어 서명은 비디오를 재생하기 위해 재생 장치를 인증하는 데 사용됩니다. App 재생 서비스가 장치에 유효한 서명을 발급하면(아래 그림의 6단계) 장치는 서명의 유효 기간 내에서 비디오를 재생할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="700" />

Player 서명의 매개변수 및 생성 규칙은 다음과 같습니다.

## 서명 매개변수[](id:p0)

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
| -- | -- | -- | -- |
| appId | Yes | Integer | 계정 appId.|
| fileId | Yes | String | VOD 파일 ID.|
| contentInfo | Yes | Object | 유형이 [ContentInfo](#p1)인 지정된 파일 ID의 내용입니다. 세 가지 유형의 콘텐츠가 지원됩니다. <li> [어댑티브 비트레이트 스트리밍](https://intl.cloud.tencent.com/document/product/266/33942) 오디오/비디오(암호화되거나 암호화되지 않은) </li><li>[트랜스코딩](https://intl.cloud.tencent.com/document/product/266/33938) 오디오/비디오. </li><li>[업로드](https://intl.cloud.tencent.com/document/product/266/9760) 원본 오디오/비디오. </li>|
| currentTimeStamp | Yes | Integer | 서명의 현재 Unix 타임스탬프입니다.|
| expireTimeStamp | No | Integer | 서명의 만료 Unix 타임스탬프입니다. 이 매개변수가 비어 있으면 서명이 만료되지 않습니다. |
| urlAccessInfo | No | Object | [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986) 매개변수, 재생 도메인 및 프로토콜을 포함한 재생 URL 액세스 매개변수. 유형은 [UrlAccessInfo ](#p4)입니다. |
| drmLicenseInfo | No | Object | [DrmLicenseInfo](#p5)에 있는 암호화된 콘텐츠의 키입니다. |

#### ContentInfo[](id:p1)

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
| -- | -- | -- | -- |
| audioVideoType | Yes | String | 재생되는 오디오/비디오 유형입니다. 유효한 값: <li>RawAdaptive: 암호화되지 않은 [어댑티브 비트레이트 스트리밍](https://intl.cloud.tencent.com/document/product/266/33942) 출력. </li><li>ProtectedAdaptive: 개인 프로토콜 또는 DRM으로 암호화된 [어댑티브 비트레이트 스트리밍](https://intl.cloud.tencent.com/document/product/266/33942) 출력. <li>Transcode: [트랜스코딩](https://intl.cloud.tencent.com/document/product/266/33938) 출력. </li><li>Original: [업로드](https://intl.cloud.tencent.com/document/product/266/9760) 원본 오디오/비디오. </li> |
| rawAdaptiveDefinition | No | Integer | 암호화되지 않은 [ABS 트랜스 코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) ID가 허용됩니다. 이 매개변수는 audioVideoType이 RawAdaptive인 경우 유효하며 필수입니다. |
| drmAdaptiveInfo | No | Object | 암호화된 [ABS 트랜스 코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) ID가 허용됩니다. 이 매개변수는 audioVideoType이 ProtectedAdaptive인 경우 유효하며 필수입니다. 유형은 [DRMAdaptiveInfo](#p2)입니다. |
| transcodeDefinition | No | Integer | [트랜스코딩](https://intl.cloud.tencent.com/document/product/266/33938#.3Ca-id.3D.22zm.22.3E.3C.2Fa.3E.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF) 템플릿의 ID가 허용됩니다. 이 매개변수는 audioVideoType이 Transcode인 경우 유효하며 필수입니다. |
| imageSpriteDefinition | No | Integer | 썸네일 미리보기를 생성하는 데 사용되는 [스프라이트 이미지](https://intl.cloud.tencent.com/document/product/266/33940) 템플릿의 ID입니다. |
| resolutionNames | No | Array of Object | [ResolutionNameInfo](#p3) 배열인 플레이어에 표시되는 여러 스트림(해상도가 다름)의 이름입니다. 기본: </br>MinEdgeLength: 240, Name: 240P. </br>MinEdgeLength: 480, Name: 480P. </br>MinEdgeLength: 720, Name: 720P. </br>MinEdgeLength: 1080, Name: 1080P. </br>MinEdgeLength: 1440, Name: 2K. </br>MinEdgeLength: 2160, Name: 4K. </br>MinEdgeLength: 4320, Name: 8K. |


#### DRMAdaptiveInfo[](id:p2)

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
| -- | -- | -- | -- |
| privateEncryptionDefinition | No | Integer | [DrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate)이 SimpleAES인 경우 [ABS 트랜스 코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) ID입니다. |
| widevineDefinition | No | Integer |  [DrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate)이 Widevine일 때 [ABS 트랜스 코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF) ID입니다. |
| fairPlayDefinition | No | Integer |  [DrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate)이 FairPlay일 때 [ABS 트랜스 코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF)ID입니다. |

#### ResolutionNameInfo[](id:p3)

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
| -- | -- | -- | -- |
| MinEdgeLength | Yes | Integer | 비디오 짧은 면. 단위: 픽셀(px).|
| Name | Yes | String | 스트림 이름. |

#### UrlAccessInfo 유형[](id:p4)

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
| -- | -- | -- | -- |
| t | No | String | <ul style="margin:0;"><li>링크 만료 시간을 나타내는 16진수 문자열.</li><li>특정 설명 및 유효한 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 t 매개변수를 참고하십시오.</li><li>이 매개변수를 비워두면 링크가 만료되지 않습니다.</li></ul>|
| exper | No | Integer | <ul style="margin:0;"> <li>미리보기 시간(초 단위, 십진수). </li><li>미리보기 시간을 지정하려면 30초 이상이어야 합니다.</li><li>특정 설명 및 유효한 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 exper 매개변수를 참고하십시오.</li></ul> |
| rlimit | No | Integer | <ul style="margin:0;"><li>재생에 허용되는 최대 IP 주소 수(10진수)입니다. </li><li>구체적인 설명과 유효 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 rlimit 매개변수를 참고하십시오.</li></ul> |
| us | No | String | <ul style="margin:0;"><li>링크를 고유하게 식별할 수 있는 URL ID입니다. </li><li>구체적인 설명과 유효한 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 us 매개변수를 참고하십시오. </li></ul> |
| domain | No | String | 재생 도메인. 지정되지 않거나 Default가 전달되면 [기본 배포 설정](https://intl.cloud.tencent.com/document/product/266/35768)의 도메인 사용. |
| scheme | No | String | 재생 Scheme. 지정되지 않거나 Default가 전달되면 [기본 배포 설정](https://intl.cloud.tencent.com/document/product/266/35768)의 Scheme 사용. 기타 유효 값: <ul style="margin:0;"><li>HTTP. </li><li>HTTPS. </li></ul>|

#### DrmLicenseInfo 유형[](id:p5)

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
| -- | -- | -- | -- |
| expireTimeStamp | No | Integer | Unix 키 만료 타임스탬프. 이 매개변수를 비워두면 서명이 만료되지 않습니다. |

>?
>- [서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987)을 사용한 경우 서브 애플리케이션의 AppId를 appId 매개변수로 설정합니다.
>- 서명 매개변수의 `t`, `exper`, `rlimit` 및 `us`의 설명 및 유효한 값은 [링크 도용 방지 매개변수](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 설명과 동일합니다.
## 서명 계산
VOD Player 서명은 Header, PayLoad 및 Key로 구성된 [JWT(JSON Web Token)](https://tools.ietf.org/html/rfc7519)입니다.

### Header

Header는 JSON 형식으로 JWT에서 사용하는 알고리즘의 정보를 나타내며 그 내용은 다음과 같이 고정됩니다.

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### PayLoad

PayLoad는 JSON 형식이며 Player 서명 매개변수를 나타냅니다. 예시는 다음과 같습니다.

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "contentInfo": {
    "audioVideoType": "RawAdaptive",
    "rawAdaptiveDefinition": 10,
    "imageSpriteDefinition": 10
  },
  "currentTimeStamp": 1663064276,
  "expireTimeStamp": 1663294210,
  "urlAccessInfo": {
    "t": "6323e6b0",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

### Key[](id:p6)

Key는 서명을 계산하는 데 사용됩니다. 아래 예시에서는 [기본 배포 설정](https://intl.cloud.tencent.com/document/product/266/35768)의 `재생 키`가 사용됩니다.

### 계산 공식

1. Signature 계산:
`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), Key)`
2. Token 계산:
`Token = base64UrlEncode(Header) + '.' + base64UrlEncode(Payload) + '.' + base64UrlEncode(Signature)`
생성된 Token은 VOD Player 서명입니다.

>?HMACSHA256에 대한 자세한 내용은 [RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3)을 참고하십시오. base64UrlEncode에 대한 자세한 내용은 [RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7)를 참고하십시오.

VOD는 서명 생성 도구와 서명 확인 도구를 제공합니다.
* [Player 서명 툴](https://console.cloud.tencent.com/vod/distribute-play/signature) .
### 계산 예시

appId가 `1255566655`이고, fileId가 `4564972818519602447`인 비디오에 대한 플레이어 서명을 생성하려고 한다고 가정합니다. 다른 매개변수는 다음과 같습니다.

* 재생 키는 `TxtyhLlgo7J3iOADIron`입니다.
* 플레이어 서명의 배포 시간은 2022-09-13 18:17:56이며 Unix 타임스탬프로 변환된 시간은 `1663064276`입니다.
* 플레이어 서명의 만료 시간은 2022-09-16 10:10:10이며 Unix 타임스탬프로 변환된 시간은 `1663294210`입니다.
* 링크 도용 방지 만료 시간은 2022-09-16 11:00:00이며 Unix 타임스탬프로 변환된 시간은 `6323e6b0`입니다.
* 재생 URL을 사용하여 동영상 재생 시 최대 3개의 IP 주소가 허용됩니다.
* URL ID에 대해 생성된 임의의 문자열은 `72d4cd1101`입니다.

다음과 같이 서명을 계산합니다.
1. Header의 내용을 결정합니다.
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
base64UrlEncode 이후에 생성된 결과는 다음과 같습니다.
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
2. Payload의 내용을 결정합니다.
```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "contentInfo": {
    "audioVideoType": "RawAdaptive",
    "rawAdaptiveDefinition": 10,
    "imageSpriteDefinition": 10
  },
  "currentTimeStamp": 1663064276,
  "expireTimeStamp": 1663294210,
  "urlAccessInfo": {
    "t": "6323e6b0",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```
base64UrlEncode 이후에 생성된 결과는 다음과 같습니다.
`eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImNvbnRlbnRJbmZvMSI6eyJhdWRpb1ZpZGVvVHlwZSI6IlJhd0FkYXB0aXZlIiwicmF3QWRhcHRpdmVEZWZpbml0aW9uIjoxMCwiaW1hZ2VTcHJpdGVEZWZpbml0aW9uIjoxMH0sImN1cnJlbnRUaW1lU3RhbXAiOjE2NjMwNjQyNzYsImV4cGlyZVRpbWVTdGFtcCI6MTY2MzI5NDIxMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNjMyM2U2YjAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ`.
3.  재생 Key(`TxtyhLlgo7J3iOADIron`)를 사용하여 HMAC Signature를 생성합니다.
`QFcBX9830ysTzJIyZxoOlRmNb2Gqy2fns9yOfriaDI8`。
4. 생성된 Token은 다음과 같습니다.
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImNvbnRlbnRJbmZvMSI6eyJhdWRpb1ZpZGVvVHlwZSI6IlJhd0FkYXB0aXZlIiwicmF3QWRhcHRpdmVEZWZpbml0aW9uIjoxMCwiaW1hZ2VTcHJpdGVEZWZpbml0aW9uIjoxMH0sImN1cnJlbnRUaW1lU3RhbXAiOjE2NjMwNjQyNzYsImV4cGlyZVRpbWVTdGFtcCI6MTY2MzI5NDIxMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNjMyM2U2YjAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.QFcBX9830ysTzJIyZxoOlRmNb2Gqy2fns9yOfriaDI8`.

## 코드 예시

VOD는 Python, Java, Go, C#, PHP, Node.js 등 다양한 프로그래밍 언어에 대한 Player 서명의 코드 예시를 제공합니다. 자세한 내용은 [Player 서명 예시](https://intl.cloud.tencent.com/document/product/266/38096)를 참고하십시오.

## 일반적인 오류
플레이어 서명을 사용하고 플레이어 SDK가 에러 코드를 반환하는 경우 일반적인 원인은 다음과 같습니다.
- **잘못된 서명 계산 [KEY](#p6)**. [KEY 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)의 `KEY` 매개변수가 아닌 [기본 배포 구성](https://intl.cloud.tencent.com/document/product/266/35768)의 `재생 키`를 사용해야 합니다.
- **잘못된 [서명 매개변수](#p0)**; 예를 들어:
 - **잘못된 매개변수 유형**; 예를 들어 appId는 정수이지만 입력된 값은 `appId:"125000123"`(문자열)입니다. 또는 `contentInfo`의 트랜스코딩 템플릿 매개변수가 정수인데 입력한 값이 `transcodeDefinition: "14011"`(문자열 유형)입니다.
 - **잘못된 매개변수 값**; 예를 들어 `contentInfo`의 오디오/비디오 유형 매개변수에 `audioVideoType: "Transocde"`(오타)가 입력되었습니다.
