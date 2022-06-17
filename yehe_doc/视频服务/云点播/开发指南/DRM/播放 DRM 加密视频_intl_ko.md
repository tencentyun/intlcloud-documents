## 학습 목표

이 문서에서는 DRM 솔루션을 사용하여 동영상을 암호화하고 플레이어를 사용하여 암호화된 동영상을 재생하는 방법을 보여줍니다.

## 전제 조건
시작하기 전에 다음을 수행하십시오.

### VOD 활성화
VOD를 활성화하려면 다음 단계를 따르십시오.

1. [Tencent Cloud 계정](https://intl.cloud.tencent.com/document/product/378/17985) 등록 및 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료합니다.
2. VOD 서비스를 구매합니다. 자세한 내용은 [과금 개요](https://intl.cloud.tencent.com/document/product/266/2838)를 참고하십시오.
3. **클라우드 서비스**>**비디오 서비스**>[**VOD**](https://console.cloud.tencent.com/vod)를 선택하여 VOD 콘솔로 이동합니다.

이제 VOD가 활성화됐습니다. 

### FairPlay 인증서 신청 및 제출
자세한 내용은 [Applying for FairPlay Certificate and Submitting Certificate Information](https://intl.cloud.tencent.com/document/product/266/46643)을 참고하십시오. 정보를 제출한 후 나중에 사용할 수 있도록 콘솔에서 인증서 URL을 보고 기록해 두십시오.

## 1단계: 링크 도용 방지 활성화

아래 예시는 계정 아래의 기본 배포 도메인에 대한 Key 링크 도용 방지를 활성화하는 방법을 보여줍니다.
>? 이미 사용 중인 도메인 이름에 대해 링크 도용 방지를 활성화하지 않는 것이 좋습니다. 재생이 실패할 수 있기 때문입니다.

1. VOD 콘솔에 로그인하여 [배포 및 재생]>[[도메인 관리]](https://console.cloud.tencent.com/vod/distribute-play/domain)를 선택하고 ‘기본 배포 도메인’을 찾아 오른쪽의 [설정]을 클릭합니다. 독립 실행형 [액세스 제어] 설정 페이지로 이동합니다.
   <img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. [랜덤 Key 생성]을 클릭하고 [Key 링크 도용 방지]를 켭니다. 팝업 창에서 생성을 클릭하여 임의 키(`testtest`)를 생성합니다. superplayer 서명을 생성하는 데 필요한 Key를 복사하고 [확인]을 클릭하여 구성을 저장합니다.
   ![image-KEY](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## 2단계: 비디오 DRM 암호화

1. VOD 콘솔에서 **미디어 자산**>[**비디오 관리**](https://console.cloud.tencent.com/vod/media)를 선택하고 타깃 비디오(FileId: 387702299667618135)를 선택한 후 **비디오 처리**를 클릭하십시오.

   ![image-20220426211316803](https://qcloudimg.tencent-cloud.cn/raw/4eab2858c67f4efbf1383a3b03810428.png)

2. 비디오 처리 페이지에서:
 - **처리 유형**으로 **작업 흐름**을 선택합니다.
 - **작업 흐름 템플릿**으로 **WidevineFairPlayPreset**을 선택합니다.
 ![image-20220425192205432](https://qcloudimg.tencent-cloud.cn/raw/cef2c1e79343ea9688654791b6fb6762.png)

>?
>- WidevineFairPlayPreset은 사전 설정된 작업 흐름입니다. 어댑티브 비트레이트 스트리밍 템플릿 11 또는 13, 포인트 스크린샷 템플릿 10(썸네일 생성용) 및 이미지 스프라이트 템플릿 10을 사용합니다.
>- 어댑티브 비트레이트 스트리밍 템플릿 11은 `FairPlay`에 의해 암호화된 다중 비트레이트 스트림을 생성하고, 어댑티브 비트레이트 스트리밍 템플릿 13은 `Widevine`에 의해 암호화된 다중 비트레이트 스트림을 생성합니다.

3. **확인**을 클릭하고 ‘비디오 상태’가 ‘처리 중’에서 ‘정상’으로 변경될 때까지 기다리십시오. 이는 비디오 처리가 완료되었음을 나타냅니다.
<img src="https://main.qcloudimg.com/raw/885b68427d36faefe8f2bb5b489e1e19.png" width="" />
4. 비디오의 ‘작업’ 열에서 **관리**를 클릭하여 관리 페이지로 이동합니다.
 - ‘기본 정보’ 탭을 클릭하면 생성된 썸네일과 어댑티브 비트레이트 스트리밍 출력(템플릿 ID: 11 및 13)을 볼 수 있습니다.

   ![image-20220426201159056](https://qcloudimg.tencent-cloud.cn/raw/696e894ed0c3665990c12cc57ebf23bf.png)

 - 생성된 이미지 스프라이트(템플릿 ID: 10)를 보려면 ‘스크린샷 정보’ 탭을 클릭합니다.

   ![image-20220426201309975](https://qcloudimg.tencent-cloud.cn/raw/1a5878fd0286c46ef487bdf81ad8503a.png)

## 3단계: Superplayer 서명 생성

Superplayer 서명은 재생 정보를 가져오는 데 사용됩니다. 생성 방법은 [Superplayer 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 참고하십시오. Superplayer 서명의 PayLoad는 다음과 같습니다.

```json
{
  "appId": 1500012416,
  "fileId": "387702299667618135",
  "currentTimeStamp": 1650886156,
  "expireTimeStamp": 1966435200,
  "urlAccessInfo": {
    "t": "75356B80",
    "us": "72d4cd1101"
  },
  "pcfg":"advanceDrmPreset"
}
```

Key는 `testtest`입니다. 생성된 Superplayer 서명(`psign`)은 다음과 같습니다.

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`

##  4단계: 재생 정보 가져오기

다음 예시는 URL에서 재생 정보를 가져오는 방법을 보여줍니다.

HTTP GET 요청 방식을 사용하며 URL은 `https://playvideo.qcloud.com/getplayinfo/v4/{appId}/{fileId}?psign={psign}`입니다.

여기서 `{appId}` 속성은 애플리케이션 Id입니다. 서브 애플리케이션을 사용하는 경우 [서브 애플리케이션 id](https://intl.cloud.tencent.com/document/product/266/33987)를 전달합니다. fileId 속성은 미디어 파일의 ID입니다.

`psign` 속성은 3단계에서 생성되며, 요청 URL은 다음과 같습니다.

`https://playvideo.qcloud.com/getplayinfo/v4/1500012416/387702299667618135?psign=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`

응답은 다음과 같습니다.

```json
{
  "code": 0,
  "message": "",
  "requestId": "9c7fab8704994c6b96375393e6544b5c",
  ...
  "media":{
	...
    "streamingInfo":{
      "drmOutput":[
        {
          "type": "FairPlay",
          "url": "http://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.11.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b",
          ...
        },
        {
          "type": "Widevine",
          "url": "http://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.13.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b",
          ...
        }
      ],
      "drmToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8",
      "widevineLicenseUrl": "https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2",
      "fairplayLicenseUrl": "https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2"
    },
    ...
  }
}
```



상기 응답에서 다음 재생 정보를 얻을 수 있습니다.

1. DRM으로 암호화된 비디오의 URL입니다.
2. License Server URL:
   - `Widevine` 암호화를 위한 라이선스 서버 URL은 `drmToken` 및 `widevineLicenseUrl`을 사용하여 연결됩니다.
   - `FairPlay` 암호화를 위한 라이선스 서버 URL은 `drmToken` 및 `fairplayLicenseUrl`을 사용하여 연결됩니다.

다음은 위의 샘플에서 얻은 재생 정보입니다.

`Widevine` 암호화:

- 암호화된 비디오의 URL: `https://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.13.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b`
- 라이선스 서버 URL: `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8`

`FairPlay` 암호화:

- 암호화된 비디오의 URL: `https://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.11.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b`
- 라이선스 서버 URL: `https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8`


## 5단계: 플레이어에서 DRM으로 암호화된 비디오 재생.

아래 예시는 각각 Widevine 및 FairPlay를 사용하여 암호화된 비디오를 재생하는 방법을 보여줍니다.

#### `Widevine`을 사용하여 암호화된 비디오 재생

`Chrome`을 통해 [Shaka Player 데모 페이지](https://shaka-player-demo.appspot.com/demo/#audiolang=zh-CN;textlang=zh-CN;uilang=zh-CN;panel=CUSTOM%20CONTENT;build=uncompiled)로 이동합니다.

![image-20220426163418989](https://qcloudimg.tencent-cloud.cn/raw/e58eb9f3795a328b2ba01d15943389e7.png)

**+** 아이콘을 클릭하고 `Manifest URL`에 3단계에서 얻은 암호화된 동영상의 URL을 입력합니다. `Name`으로 `Widevine`을 전달합니다.

![image-20220426163853470](https://qcloudimg.tencent-cloud.cn/raw/0846706a160112ccea2712cd9c6b4d4c.png)

3단계에서 얻은 Widevine의 `Custom License Server URL`을 입력하고 **Save**를 클릭합니다.

![image-20220426163939777](https://qcloudimg.tencent-cloud.cn/raw/702199c544c829db6f5d4815dcd4ff48.png)

`Widevine` 재생 옵션이 페이지에 나타납니다.

![image-20220426164129657](https://qcloudimg.tencent-cloud.cn/raw/7d70df750e283d8a5a0d42596e08c14b.png)

**Play**를 클릭하여 암호화된 비디오를 재생합니다.

#### `FairPlay`를 사용하여 암호화된 동영상 재생

`Safari`를 통해 [Shaka Player 데모 페이지](https://shaka-player-demo.appspot.com/demo/#audiolang=zh-CN;textlang=zh-CN;uilang=zh-CN;panel=CUSTOM%20CONTENT;build=uncompiled)로 이동합니다.

![image-20220426163418989](https://qcloudimg.tencent-cloud.cn/raw/0b9b5ae58e65c6b3c0789b8d98af57a1.png)

**+** 아이콘을 클릭하고 `Manifest URL`에 3단계에서 얻은 암호화된 비디오의 URL을 입력합니다. `Name`으로 `FairPlay`를 전달하십시오.

![image-20220426164907499](https://qcloudimg.tencent-cloud.cn/raw/70f01463b0afdf231dd014ea4782728f.png)

`Custom License Server URL`에 대해 3단계에서 얻은 FairPlay용 라이선스 서버 URL을 입력합니다. `Custom License Certificate URL`에 대해 `FairPlay` 인증서(VOD 콘솔에서 인증서를 받을 수 있음)를 입력하고 **Save**를 클릭합니다.

![image-20220426164950762](https://qcloudimg.tencent-cloud.cn/raw/bdd9c3ecd2882537df76d657768855e9.png)

`FairPlay` 재생 옵션이 페이지에 나타납니다.

![image-20220426165137520](https://qcloudimg.tencent-cloud.cn/raw/9da228ea1db9ab54a1631f605e24d806.png)

**Play**를 클릭하여 암호화된 동영상을 재생합니다.

## 결론

이제 DRM 솔루션을 사용하여 동영상을 암호화하고 플레이어에서 암호화된 동영상을 재생하는 방법을 배웠습니다.