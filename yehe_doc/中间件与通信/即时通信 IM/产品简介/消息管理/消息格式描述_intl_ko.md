## 메시지 바디 MsgBody
메시지 내용은 MsgBody 필드에 입력됩니다. Instant Messaging(IM)은 하나의 메시지에서 여러 메시지 요소를 지원합니다. 예를 들어 메시지에는 텍스트와 이모티콘이 모두 포함될 수 있습니다. 따라서 MsgBody는 메시지 요소를 필요한 만큼 포함할 수 있는 Array로 정의됩니다. 메시지 요소의 이름은 TIMMsgElement입니다. MsgBody를 구성하는 TIMMsgElements의 예시는 [MsgBody 메시지 콘텐츠 예시](https://intl.cloud.tencent.com/document/product/1047/33527)를 참고하십시오.

TIMMsgElement의 형식은 다음과 같습니다.
```
{
    "MsgType": "",
    "MsgContent": {}
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| MsgType | String | 메시지 요소 유형. 현재 지원하는 메시지 객체: TIMTextElem(텍스트 메시지), TIMLocationElem(위치 메시지), TIMFaceElem(이모티콘 메시지), TIMCustomElem(사용자 정의 메시지), TIMSoundElem(음성 메시지), TIMImageElem(이미지 메시지), TIMFileElem(파일 메시지), TIMVideoFileElem(영상 메시지). |
|MsgContent|Object|메시지 요소의 콘텐츠. MsgType별로 MsgContent 형식이 다릅니다. 자세한 내용은 아래 내용을 참고하십시오. |

현재 지원하는 메시지 유형 MsgType은 다음 표를 참고하십시오.

| MsgType 값 | 유형 |
|---------|---------|
| TIMTextElem | 텍스트 메시지|
|TIMLocationElem|지리적 위치 메시지|
|TIMFaceElem|이모티콘 메시지|
|TIMCustomElem|사용자 정의 메시지. 수신측이 iOS 디바이스이며 애플리케이션이 백그라운드 실행 상태인 경우, 이 메시지 유형은 텍스트 이외의 필드를 APNs에 제공합니다. 결합된 메시지에는 TIMCustomElem 사용자 정의 메시지 요소가 하나만 포함될 수 있습니다. |
|TIMSoundElem|음성 메시지|
|TIMImageElem|이미지 메시지|
|TIMFileElem|파일 메시지|
|TIMVideoFileElem| 영상 메시지|

>!상기 유형의 메시지는 모두 서버에 통합된 Rest API를 통해 발송됩니다.

## 메시지 요소 TIMMsgElement

### 텍스트 메시지 요소

```
{
    "MsgType": "TIMTextElem",
    "MsgContent": {
        "Text": "hello world"
    }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| Text | String | 메시지 콘텐츠. 수신측이 iOS 또는 Android 디바이스이며, 백그라운드 실행 상태인 경우, 오프라인 푸시 텍스트로 표시됩니다. |

수신측이 iOS 또는 Android 디바이스이며, 백그라운드 실행 상태인 경우, JSON 요청 패킷의 Text 필드는 오프라인 푸시 텍스트로 표시됩니다. 

### 지리적 위치 메시지 요소

```
{
    "MsgType": "TIMLocationElem", 
    "MsgContent": {
        "Desc": "someinfo", 
        "Latitude": 29.340656774469956, 
        "Longitude": 116.77497920478824
    }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| Desc | String | 지리적 위치 설명 정보 |
|Latitude|Number|위도|
|Longitude|Number|경도|

수신측이 iOS 또는 Android 디바이스이며, 백그라운드 실행 상태인 경우, 영문 버전 오프라인 푸시 텍스트는 ‘[Location]’입니다.

### 이모티콘 메시지 요소

```
{
    "MsgType": "TIMFaceElem", 
    "MsgContent": {
        "Index": 1, 
        "Data": "content"
    }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| Index | Number | 사용자 정의 이모티콘 인덱스 |
|Data|String|추가 데이터|

수신측이 iOS 또는 Android 디바이스이며, 백그라운드 실행 상태인 경우, 영문 버전 오프라인 푸시 텍스트는 ‘[Face]’입니다.


<dx-alert infotype="explain" title="설명">
메시지에 TIMCustomElem 사용자 정의 메시지 요소가 1개만 있는 경우, Desc 필드 및 OfflinePushInfo.Desc 필드 모두 입력하지 않으면 해당 메시지의 오프라인 푸시를 받을 수 없으며 OfflinePushInfo.Desc 필드를 입력해야 메시지의 오프라인 푸시를 받을 수 있습니다. 
</dx-alert>


### 사용자 정의 메시지 요소

```
{
    "MsgType": "TIMCustomElem", 
    "MsgContent": {
        "Data": "message", 
        "Desc": "notification", 
        "Ext": "url", 
        "Sound": "dingdong.aiff"
    }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| Data | String | 사용자 정의 메시지 데이터. APNs의 payload 필드로서 전달되지 않기 때문에 payload에서 Data 필드를 가져올 수 없습니다.|
|Desc|String|사용자 정의 메시지 설명. 수신측이 iOS 또는 Android 디바이스이며, 백그라운드 실행 상태인 경우, 오프라인 푸시 텍스트로 표시됩니다. <br>사용자 정의 메시지 발송과 동시에[OfflinePushInfo.Desc](https://intl.cloud.tencent.com/document/product/1047/33527) 필드를 설정하면 해당 필드가 덮어쓰기 되니, OfflinePushInfo.Desc 필드를 먼저 입력하기 바랍니다. <br><dx-alert infotype="explain" title="설명">
메시지에 TIMCustomElem 사용자 정의 메시지 요소가 1개만 있는 경우, Desc 필드 및 OfflinePushInfo.Desc 필드 모두 입력하지 않으면 해당 메시지의 오프라인 푸시를 받을 수 없으며 OfflinePushInfo.Desc 필드를 입력해야 메시지의 오프라인 푸시를 받을 수 있습니다. 
</dx-alert>|
|Ext|String|확장 필드. 수신측이 iOS 디바이스이며, 백그라운드 실행 상태인 경우, 해당 필드는 APNs 요청 패킷 Payloads의 Ext 키 값으로 전달됩니다. Ext 프로토콜 형식은 비즈니스측에서 결정하며 APNs는 그대로 통과시킵니다. |
|Sound|String|사용자 정의 APNs 푸시 알림음|

수신측이 iOS 디바이스이며, 백그라운드 실행 상태인 경우, Desc는 푸시 텍스트로, Ext 필드는 APNS 요청 패킷 Payloads의 ext 키 값으로 하여 전달되며, Data 필드는 APNs의 Payloads 필드로서 발송되지 않습니다. 결합된 메시지에는 한 개의 TIMCustomElem 사용자 정의 메시지 요소만 포함할 수 있습니다.

### 음성 메시지 요소

>!서버 통합 Rest API를 통해 음성 메시지를 보내려면 음성 Url, UUID, Download_Flag 필드를 입력해야 하며, 해당 음성을 다운로드할 수 있는 Url을 입력해야 합니다. UUID 필드는 전역적으로 고유한 String 값을 입력해야 하는데 일반적으로 음성 파일의 MD5 값을 입력합니다. 메시지 수신자는 V2TIMSoundElem.getUUID()를 통해 설정된 UUID 필드를 수신하며 서비스 App은 해당 필드를 사용하여 음성을 구분할 수 있습니다. Download_Flag 필드는 2를 입력해야 합니다.

4.X 이상 버전의 IM SDK(Android, iOS, Mac 및 Windows용)는 다음 형식으로 음성 메시지 요소를 발송합니다.
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "Url": "https://1234-5678187359-1253735226.cos.ap-shanghai.myqcloud.com/abc123/c9be9d32c05bfb77b3edafa4312c6c7d",
        "UUID": "1053D4B3D61040894AC3DE44CDF28B3EC7EB7C0F",
        "Size": 62351,
        "Second": 1,
        "Download_Flag": 2
    }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| Url | String | 음성 다운로드 주소. 이 URL 주소로 관련 음성을 다운로드 할 수 있습니다. |
| UUID | String | 음성의 유일한 식별자. 클라이언트에서 음성 인덱스에 사용하는 키 값 입니다. |
| Size | Number | 음성 데이터 크기. 단위: 바이트. |
| Second | Number | 음성 시간. 단위: 초. |
| Download_Flag | Number | 음성 다운로드 메소드 플래그. 현재 Download_Flag 값은 2만 가능하며 `Url` 필드에 지정된 URL을 통해 바로 음성을 다운로드할 수 있음을 의미합니다. |

>?2.X 및 3.X 버전의 IM SDK(Android, iOS, Mac 및 Windows용)는 다음 형식으로 음성 메시지 요소를 발송합니다.
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "UUID": "305c0201", //음성의 유일한 식별자로 유형은 String입니다. 클라이언트에서 음성 인덱스 시 키 값으로 사용합니다. 이 필드를 통해 관련 음성을 다운로드할 수 없습니다. 음성을 가져오려면, IM SDK 버전을 4.X로 업데이트하십시오.
        "Size": 62351,      //음성 데이터 크기. 유형: Number. 단위: 바이트.
        "Second": 1         //Number 유형 음성 길이. 단위: 초.
    }
}
```


### 이미지 메시지 요소

>!서버측 REST API를 통해 이미지 메시지를 보내려면 URL, UUID, Width, Height 필드를 입력해야 합니다. URL을 통해 이미지를 다운로드할 수 있는지 확인하여 [Obtaining Basic Image Information](https://intl.cloud.tencent.com/document/product/1045/33722) 및 [Image Processing](https://intl.cloud.tencent.com/document/product/1045/33726) 할 수 있습니다. Width와 Height는 이미지의 너비와 높이(단위: 픽셀)입니다. UUID는 전역적으로 고유한 String 값, 일반적으로 이미지의 MD5 값으로 설정해야 합니다. 메시지 수신자는 V2TIMImageElem.getImageList() 를 호출하여 V2TIMImage 객체를 얻은 다음 V2TIMImage.getUUID() 를 호출하여 지정된 UUID를 얻을 수 있습니다. App은 UUID를 사용하여 이미지를 식별할 수 있습니다.

```
{
    "MsgType": "TIMImageElem",
    "MsgContent": {
        "UUID": "1853095_D61040894AC3DE44CDFFFB3EC7EB720F",
        "ImageFormat": 1,
        "ImageInfoArray": [
            {
                "Type": 1,           //원본 이미지
                "Size": 1853095,
                "Width": 2448,
                "Height": 3264,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/0"
            },
            {
                "Type": 2,      //큰 이미지
                "Size": 2565240,
                "Width": 0,
                "Height": 0,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/720"
            },
            {
                "Type": 3,   //썸네일
                "Size": 12535,
                "Width": 0,
                "Height": 0,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/198"
            }
        ]
    }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| UUID | String | 이미지의 유일한 식별자. 클라이언트에서 이미지 인덱스에 사용하는 키 값입니다. |
| ImageFormat | Number | 이미지 형식. JPG = 1, GIF = 2, PNG = 3, BMP = 4, 기타 = 255. |
| ImageInfoArray | Array | 원본 이미지, 썸네일 또는 큰 이미지 다운로드 정보 |
| Type | Number | 이미지 유형: 1-원본 이미지, 2-큰 이미지, 3-썸네일. |
| Size | Number | 이미지 데이터 크기. 단위: 바이트. |
| Width | Number | 이미지 폭. 단위: 픽셀 |
| Height | Number | 이미지 높이. 단위: 픽셀 |
| URL | String | 이미지 다운로드 주소 |

### 파일 메시지 요소

>!서버 통합 Rest API를 통해 파일 메시지를 보내려면 파일의 Url, UUID, Download_Flag 필드를 입력해야 하며, 해당 파일을 다운로드 할 수 있는 URL을 입력해야 합니다. UUID 필드는 전역적으로 고유한 String 값을 입력해야 하는데 일반적으로 이미지의 MD5 값을 입력합니다. 메시지 수신자는 V2TIMFileElem.getUUID()를 호출하여 설정된 UUID 필드를 수신하며 서비스 App은 이 필드를 사용하여 파일을 구분할 수 있습니다. Download_Flag 필드는 2를 입력해야 합니다.

4.X 이상 버전의 IM SDK(Android, iOS, Mac 및 Windows용)는 다음 형식으로 파일 메시지 요소를 발송합니다.
```
{
    "MsgType": "TIMFileElem",
    "MsgContent": {
        "Url": "https://7492-5678539059-1253735326.cos.ap-shanghai.myqcloud.com/abc123/49be9d32c0fbfba7b31dafa4312c6c7d",
        "UUID": "1053D4B3D61040894AC3DE44CDF28B3EC7EB7C0F",
        "FileSize": 1773552,
        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV",
		"Download_Flag": 2
    }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| Url | String | 파일 다운로드 주소. 이 URL을 통해 관련 파일을 바로 다운로드할 수 있습니다. |
| UUID | String | 파일의 유일한 식별자. 클라이언트에서 파일 인덱스에 사용하는 키 값입니다. |
| FileSize | Number | 파일 데이터 크기. 단위: 바이트. |
| FileName | String | 파일 이름 |
| Download_Flag | Number | 파일 다운로드 메소드 플래그. 현재 Download_Flag 값은 2만 가능하며 `Url` 필드 값의 URL을 통해 바로 파일을 다운로드할 수 있음을 의미합니다. |

>?2.X 및 3.X 버전의 IM SDK(Android, iOS, Mac 및 Windows용)는 다음 형식으로 파일 메시지 요소를 발송합니다.
>```
{
    "MsgType": "TIMFileElem",
    "MsgContent": {
        "UUID": "305c02010", //파일의 유일한 식별자로 유형은 String입니다. 클라이언트에서 파일 인덱스에 사용하는 키 값이며 이 필드를 통해 파일을 다운로드할 수 없습니다. 파일을 가져오려면 IM SDK 버전을 4.X로 업데이트하십시오.
        "FileSize": 1773552, //Number 유형 파일 데이터 크기. 단위: 바이트.
        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV" //파일 이름. 유형: String.
    }
}
```

### 영상 메시지 요소

>!서버 통합 Rest API를 통해 비디오 메시지를 보내려면 VideoUrl, VideoUUID, ThumbUrl, ThumbUUID, ThumbWidth, ThumbHeight, VideoDownloadFlag 및 ThumbDownloadFlag 필드를 입력해야 하며, 해당 비디오를 다운로드할 수 있는 VideoUrl, 해당 비디오 썸네일을 다운로드할 수 있는 ThumbUrl을 입력해야 합니다. VideoUUID와 ThumbUUID 필드는 전역적으로 고유한 String 값을 입력해야 하는데 일반적으로 해당 비디오와 썸네일의 MD5 값을 입력합니다. 메시지 수신자는 V2TIMVideoElem.getVideoUUID()와 V2TIMVideoElem.getSnapshotUUID()를 호출하여 설정한 UUID 필드를 수신하며 서비스 App은 이 필드를 사용하여 비디오를 구분할 수 있습니다. VideoDownloadFlag와 ThumbDownloadFlag 필드는 2를 입력해야 합니다.

4.X 이상 버전의 IM SDK(Android, iOS, Mac 및 Windows용)는 다음 형식으로 영상 메시지 요소를 발송합니다.
```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/f7c6ad3c50af7d83e23efe0a208b90c9",
        "VideoUUID": "5da38ba89d6521011e1f6f3fd6692e35",
        "VideoSize": 1194603,
        "VideoSecond": 5,
		"VideoFormat": "mp4",
		"VideoDownloadFlag":2,
		"ThumbUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/a6c170c9c599280cb06e0523d7a1f37b",
		"ThumbUUID": "6edaffedef5150684510cf97957b7bc8",
		"ThumbSize": 13907,
		"ThumbWidth": 720,
		"ThumbHeight": 1280,
		"ThumbFormat": "JPG",
		"ThumbDownloadFlag":2
    }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| VideoUrl | String | 비디오 다운로드 주소. 해당 URL을 통해 바로 영상을 다운로드 할 수 있습니다.  |
| VideoUUID | String | 비디오의 유일한 식별자. 클라이언트에서 비디오 인덱스에 사용하는 키 값입니다. |
| VideoSize | Number |  비디오 데이터 크기. 단위: 바이트. |
| VideoSecond | Number | 비디오 길이(초). Web 클라이언트의 경우 이 필드를 가져올 수 없으며 값 0이 사용됩니다. |
| VideoFormat | String | mp4 같은 비디오 형식입니다. |
| VideoDownloadFlag | Number | 비디오 다운로드 메소드 플래그. 현재 VideoDownloadFlag 값은 2만 가능하며 `VideoUrl` 필드 값의 URL을 통해 바로 비디오를 다운로드할 수 있음을 의미합니다. |
| ThumbUrl | String | 비디오 썸네일 다운로드 주소. 해당 URL을 통해 바로 비디오 썸네일을 다운로드할 수 있습니다.  |
| ThumbUUID | String | 비디오 썸네일의 유일한 식별자. 클라이언트에서 비디오 썸네일 인덱스에 사용하는 키 값입니다. |
| ThumbSize | Number | 썸네일 크기. 단위: 바이트. |
| ThumbWidth | Number | 썸네일 폭. 단위: 픽셀 |
| ThumbHeight | Number | 썸네일 높이. 단위: 픽셀 |
| ThumbFormat | String | JPG, BMP 같은 썸네일 형식. |
| ThumbDownloadFlag | Number | 비디오 썸네일 다운로드 메소드 플래그. 현재 ThumbDownloadFlag 값은 2만 가능하며 `ThumbUrl` 필드 값의 URL을 통해 바로 비디오 썸네일을 다운로드할 수 있음을 의미합니다. |


>?2.X 및 3.X 버전의 IM SDK(Android, iOS, Mac 및 Windows용)는 다음 형식으로 영상 메시지 요소를 발송합니다.
>```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUUID": "1400123456_dramon_34ca36be7dd214dc50a49238ef80a6b5",// 영상의 유일한 식별자로 유형은 String입니다. 클라이언트에서 영상 인덱스에 사용하는 키 값으로 이 필드를 통해 영상을 다운로드할 수 없습니다. 영상을 가져오려면 IM SDK 버전을 4.X로 업데이트하십시오.
        "VideoSize": 1194603, //영상 데이터 크기. 유형: Number. 단위: 바이트.
        "VideoSecond": 5,     //영상 길이. 유형: Number. 단위: 초.
		"VideoFormat": "mp4", //비디오 형식. 유형: String. 예: mp4.
		"ThumbUUID": "1400123456_dramon_893f5a7a4872676ae142c08acd49c18a",// 비디오 썸네일의 유일한 식별자로 유형은 String입니다. 클라이언트에서 비디오 썸네일 인덱스에 사용하는 키 값으로 이 필드를 통해 비디오 썸네일을 다운로드할 수 없습니다. 비디오 썸네일을 가져오려면 IM SDK 버전을 4.X로 업데이트하십시오.
		"ThumbSize": 13907,   //썸네일 크기. 유형: Number. 단위: 바이트.
		"ThumbWidth": 720,    //썸네일 폭. 유형: Number.
		"ThumbHeight": 1280,  //썸네일 높이. 유형: Number.
		"ThumbFormat": "JPG"  //썸네일 형식. 유형: String. 예: JPG, BMP 등.
    }
}
```

### 결합된 메시지 요소
>!기본 SDK 5.2.210 이상 및 web SDK 2.10.1 이상만 결합된 메시지의 송수신을 지원합니다.

```json
{
  "MsgType": "TIMRelayElem",
  "MsgContent": {
    "Title": "그룹 채팅 기록",
    "MsgNum": 2,
    "CompatibleText": "SDK 버전은 결합된 메시지를 지원하지 않습니다. 최신 버전으로 업그레이드하십시오.",
    "AbstractList": [
      "A: 이에 대해 어떻게 생각하세요?",
      "B: 좋은 것 같아요"
    ],
    "MsgList": [
      {
        "From_Account": "A",
        "GroupId": "group1",
        "MsgSeq": 85,
        "MsgRandom": 3998651049,
        "MsgTimeStamp": 1664437702,
        "MsgBody": [
          {
            "MsgContent": {
              "Text": "이에 대해 어떻게 생각하세요?"
            },
            "MsgType": "TIMTextElem"
          }
        ]
      },
      {
        "From_Account": "B",
        "GroupId": "group1",
        "MsgSeq": 86,
        "MsgRandom": 965790,
        "MsgTimeStamp": 1664437703,
        "MsgBody": [
          {
            "MsgContent": {
              "Text": "좋은 것 같아요"
            },
            "MsgType": "TIMTextElem"
          }
        ]
      }
    ]
  }
}
```

| 필드 | 유형 | 설명|
|---------|---------|---------|
| Title | String | 결합된 메시지 제목. |
| MsgNum | Integer | 결합/전달된 메시지 수. |
| CompatibleText | String | 호환되는 텍스트. 결합된 메시지를 지원하지 않는 이전 버전의 SDK가 결합된 메시지를 수신하면 IM 백엔드는 메시지를 호환 가능한 텍스트로 변환하여 전달합니다. |
| AbstractList | Array | String 배열 형식의 결합된 메시지 다이제스트 목록입니다. |
| MsgList | Array | 메시지 목록. 이 필드는 결합된 메시지의 합계가 12K 이하인 경우에만 사용할 수 있으며 이 경우 JsonMsgKey 필드를 사용할 수 없습니다. |
| JsonMsgKey | String | 결합된 메시지 목록의 키. 이 필드는 결합된 메시지의 합계가 12K보다 큰 경우에만 사용할 수 있으며 이 경우 MsgList 필드를 사용할 수 없습니다. |

MsgList의 각 메시지 구조는 다음과 같습니다.

| 필드 | 유형 | 설명|
|---------|---------|---------|
| From_Account | String | 메시지 발신자의 UserID. 이 필드는 결합된 메시지가 일대일 또는 그룹 메시지인 경우 사용할 수 있습니다. |
| To_Account | String | 메시지 수신자의 UserID. 이 필드는 결합된 메시지가 일대일 메시지인 경우에만 사용할 수 있습니다. |
| GroupId | String | 그룹 ID. 이 필드는 결합된 메시지가 그룹 메시지인 경우에만 사용할 수 있습니다. |
| MsgSeq | Integer | 메시지의 시퀀스 번호(32비트 부호 없는 정수). |
| MsgRandom | Integer | 메시지의 난수(32비트 부호 없는 정수). |
| MsgTimeStamp | Integer | 메시지 타임스탬프(초). |
| MsgBody | Array | 메시지 본문. 형식에 대한 자세한 내용은 [메시지 형식](https://intl.cloud.tencent.com/document/product/1047/33527)을 참고하십시오. (참고: 메시지에는 여러 메시지 요소가 포함될 수 있으며 이 경우 MsgBody는 Array입니다.)  |
| CloudCustomData | String | 사용자 정의 메시지 데이터. 클라우드에 저장되고 피어 엔드로 전송됩니다. 이러한 데이터는 앱을 제거하고 다시 설치한 후에 가져올 수 있습니다. |

## MsgBody 메시지 콘텐츠 예시

### 단일 텍스트 요소 메시지

단일 메시지에 하나의 텍스트 메시지 요소만 포함됩니다. 텍스트 콘텐츠는 hello world 입니다.

```json
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello world"
            }
        }
    ]
}
```

### 결합된 메시지

다음과 같이 텍스트 메시지 요소와 이모티콘 요소 등 2가지 요소가 포함된 단일 메시지입니다. 메시지 요소 순서는 텍스트+이모티콘+텍스트입니다. 
```json
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"
            }
        }, 
        {
            "MsgType": "TIMFaceElem", 
            "MsgContent": {
                "Index": 1, 
                "Data": "content"
            }
        }, 
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "world"
            }
        }
    ]
}
```

>!한 개의 결합된 메시지에는 한 개의 TIMCustomElem 사용자 정의 메시지 요소만 포함할 수 있으며 다른 메시지 요소 수량은 제한이 없습니다. 

##  메시지 사용자 정의 데이터 CloudCustomData
모든 메시지는 사용자 정의 데이터 CloudCustomData를 포함할 수 있습니다.

CloudCustomData는 해당 메시지 MsgBody와 함께 클라우드에 저장됩니다. CloudCustomData는 피어에 발송되며 애플리케이션 삭제 및 재설치 후에도 계속 풀링할 수 있습니다. 

CloudCustomData 및 MsgBody 형식 예시는 다음과 같습니다. 
```json
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

## Apple Push Notification Service(APNs)
### 클라이언트 푸시가 표시되는 형식
- **닉네임 미설정 계정**
계정에 닉네임을 설정하지 않은 경우 APNs 푸시에는 푸시된 텍스트 콘텐츠만 표시됩니다. 1:1 채팅 메시지는 ‘푸시 텍스트’, 그룹 채팅 메시지에는 ‘(그룹 이름): 푸시 텍스트’만 표시됩니다. 
![](https://main.qcloudimg.com/raw/7bdb0f41aaa943190ce949fea8d20095.png)

- **닉네임 설정 계정**
계정에 닉네임을 설정한 경우 1:1 채팅 메시지에는 ‘닉네임: 푸시 텍스트’ 형식으로 표시되고, 그룹 채팅 메시지에는 ‘닉네임(그룹 이름): 푸시 텍스트’ 형식으로 표시됩니다.
![](https://main.qcloudimg.com/raw/7bdb0f41aaa943190ce949fea8d20095.png)

- **결합된 메시지가 표시되는 형식**
결합된 메시지의 경우, 순서에 따라 각 메시지 요소의 푸시 텍스트가 순서대로 표시됩니다. 계정에 닉네임을 설정한 1:1 채팅 메시지의 경우 푸시 텍스트는 ‘helloworld’가 됩니다. 텍스트(예:helloworld)에는 공백이 포함되어 있지 않습니다. 백엔드에서 순서대로 각 메시지 요소를 순서대로 연결하며 텍스트 사이에 어떤 것도 추가하지 않습니다. 메시지 요소 사이에 빈 칸이나 다른 문자를 추가하려면 호출측에서 자체적으로 제어해야 합니다. 
```json
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"  
            }
        },
        {
            "MsgType": "TIMCustomElem",
            "MsgContent": {
                "Data": "message",
                "Desc": "world",
                "Ext": "https://www.example.com",               
                "Sound": "dingdong.aiff"
            }
        }
    ] 
}
```
다음 표에는 다양한 메시지 요소의 푸시 텍스트 필드가 요약되어 있습니다.

| MsgType 값 | 유형 |메시지 요소 푸시 텍스트|
|---------|---------|---------|
| TIMTextElem | 텍스트 메시지|Text  필드. |
|TIMLocationElem|지리적 위치 메시지.|영문 버전: "[Location]".|
|TIMFaceElem|이모티콘 메시지.|영문 버전: "[Face]".|
|TIMCustomElem|사용자 정의 메시지.|Desc  필드. |

### 닉네임 및 그룹 이름 설정 REST API
계정 닉네임 설정 REST API: [프로필 정보 설정](https://intl.cloud.tencent.com/document/product/1047/34916).
그룹 이름 설정 REST API: [그룹 프로필 정보 수정](https://intl.cloud.tencent.com/document/product/1047/34962).

### 고급 애플리케이션
#### APN에서 제공하는 푸시 알림음 및 확장 필드 사용자 정의
TIMCustomElem을 사용하여 메시지 요소를 사용자 정의합니다. Sound에 사용자 정의 오디오 파일 이름을 입력하고 Ext에 전달할 확장 필드를 입력합니다. 확장 요청 필드는 APNs 푸시 PayLoad의 Ext 필드에서 가져올 수 있습니다.
```
{
    "To_Account": "lumotuwe5", 
    "MsgRandom": 121212, 
    "MsgBody": [
        {
            "MsgType": "TIMCustomElem", 
            "MsgContent": {
                "Data": "other information", 
                "Desc": "hello", 
                "Ext": "www.qq.com", 
                "Sound": "dingdong.aiff"
            }
        }, 
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "world"
            }
        }
    ]
}

```

클라이언트에서 수신하는 APNs 푸시 JSON Payload는 다음과 같습니다. 

```
{
    "aps": {
        "alert": "Nickname:helloworld",   //각 메시지 요소의 푸시 텍스트는 순서대로 연결됩니다.
        "badge": 5,                       
        "sound": "dingdong.aiff"         //TIMCustomElem의 Sound 필드에 해당됨 
    }, 
    "ext": "www.qq.com"                //TIMCustomElem의 Ext 필드에 해당됨
}

```

## OfflinePushInfo 설명

OfflinePushInfo는 오프라인 푸시 설정에 사용되는 JSON 객체로 해당 메시지의 푸시를 비활성화 여부, 푸시 텍스트 설명 콘텐츠, 메시지에 대한 푸시 패스스루 문자열 등을 설정할 수 있습니다. OfflinePushInfo를 사용하여 TIMCustomElem을 캡슐화하지 않고도 편리하게 오프라인 푸시 정보를 설정할 수 있습니다.

>!OfflinePushInfo가 입력되면 TIMCustomElem의 오프라인 푸시 관련 설정은 무시됩니다. 현재 OfflinePushInfo는 APN 푸시 및 다양한 Android 디바이스(Xiaomi, Huawei, Meizu, OPPO 및 Vivo) 푸시 서비스와 연동할 수 있습니다.

OfflinePushInfo의 형식 예시는 다음과 같습니다. 

```
{
    // ...
    "MsgBody": [...] // MsgBody 관련 설명과 동일
    "OfflinePushInfo": {
        "PushFlag": 0,
        "Title":"푸시 제목",
        "Desc": "오프라인 푸시 콘텐츠",
        "Ext": "패스스루 콘텐츠",
        "AndroidInfo": { 
			"Sound": "android.mp3",
			"OPPOChannelID": "test_OPPO_channel_id",
			"VIVOClassification": 1
        },
        "ApnsInfo": {
            "Sound": "apns.mp3",
            "BadgeMode": 1,
            "Title":"apns title",
            "SubTitle":"apns subtitle",
            "Image":"www.image.com",
            "MutableContent": 1
        }
    }
}
```

 필드 설명은 다음과 같습니다.

| 필드 | 유형 | 필수 | 설명 |
|---------|---------|---------|---------|
| PushFlag | Integer | 옵션 | 0: 푸시 활성화, 1: 오프라인 푸시 비활성화  |
| Title | String | 옵션| 오프라인 푸시 제목. 이 필드는 iOS 및 Android에 모두 적용됩니다.|
| Desc | String | 옵션| 오프라인 푸시 콘텐츠. 이 필드는 위에서 언급한 [TIMMsgElement](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement) 메시지 요소의 오프라인 푸시 텍스트를 덮어씁니다.<br> 발송된 메시지에 [TIMCustomElem](https://intl.cloud.tencent.com/document/product/1047/33527#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0)이 하나만 있는 경우, 이 Desc 필드는 TIMCustomElem의 Desc 필드를 덮어씁니다. 2개의 Desc 필드를 모두 입력하지 않으면 해당 사용자 정의 메시지에 대한 오프라인 푸시를 수신할 수 없습니다.|
| Ext | String | 옵션| 오프라인 푸시 패스스루 콘텐츠. 중국 내 Android 휴대폰 벤더의 푸시 플랫폼 요구 사항이 모두 다르기 때문에 해당 필드는 JSON 형식을 사용하기 바랍니다. 그렇지 않으면 일부 벤더의 오프라인 푸시를 수신할 수 없습니다. |
| AndroidInfo.Sound | String | 옵션| Android 오프라인 푸시 알림음 파일 경로 |
| AndroidInfo.HuaWeiChannelID | String | 옵션| EMUI 10.0 이후 버전이 설치된 Huawei 휴대폰의 알림 채널 필드. 해당 필드가 채워져 있으면 콘솔에서 설정한 ChannelID 값을 덮어쓰기합니다. 해당 필드가 공란일 경우, 콘솔에서 설정한 ChannelID 값을 덮어쓰지 않습니다. |
| AndroidInfo.XiaoMiChannelID | String | 옵션| MIUI 10 이후 버전이 설치된 Xiaomi 휴대폰의 알림 채널 필드. 해당 필드가 채워져 있으면 콘솔에서 설정한 ChannelID 값을 덮어쓰기합니다. 해당 필드가 공란일 경우, 콘솔에서 설정한 ChannelID 값을 덮어쓰지 않습니다. |
| AndroidInfo.OPPOChannelID | String | 옵션| Android 8.0 이상이 설치된 OPPO 휴대폰의 NotificationChannel 필드. 해당 필드가 채워져 있으면 콘솔에서 설정한 ChannelID 값을 덮어쓰기합니다. 해당 필드가 공란일 경우, 콘솔에서 설정한 ChannelID 값을 덮어쓰지 않습니다. |
| AndroidInfo.GoogleChannelID | String | 옵션| Android 8.0 이상이 설치된 Google 휴대전화의 알림 채널 필드. Google 푸시 신규 인터페이스(인증서 파일 업로드)는 channel id를 지원하며, 구 인터페이스(서버 키 입력)는 지원하지 않습니다. |
| AndroidInfo.VIVOClassification | Integer | 옵션| VIVO 휴대폰 푸시 메시지 분류. ‘0’: 운영 메시지, ‘1’: 시스템 메시지를 의미하며, 입력하지 않으면 기본값은 1입니다.|
| AndroidInfo.HuaWeiImportance | String | 옵션| Huawei 푸시 공지 메시지 분류. 값은 LOW, NORMAL이며, 입력하지 않으면 기본값은 NORMAL입니다.|
| AndroidInfo.ExtAsHuaweiIntentParam | Integer | 옵션| 콘솔에서 Huawei 푸시를 ‘지정된 인앱 페이지 열기’로 설정한 경우, ‘1’은 패스스루 콘텐츠 Ext를 Intent 매개변수로 함을 의미하고 ‘0’은 패스스루 콘텐츠 Ext를 Action 매개변수로 함을 의미합니다. 입력하지 않으면 기본값은 0입니다. 두 매개변수의 차이점 관련 자세한 내용은 [Huawei 푸시 문서](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/andorid-basic-clickaction-0000001087554076#section20203190121410)를 참고하십시오.|
| AndroidInfo.HuaWeiCategory | String | 옵션 | Huawei 휴대폰은 메시지 유형 식별에 사용됩니다. 이 필드가 비어 있지 않으면 콘솔에 구성된 category 값을 재정의하고, 이 필드가 비어 있으면 콘솔에 구성된 category 값을 덮어쓰지 않습니다. 자세한 내용은 [category 설명](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-References/https-send-api-0000001050986197#section13271045101216)을 참고하십시오.|
| ApnsInfo.BadgeMode | Integer | 옵션| 기본값 또는 0은 카운트 필요함을 나타내며 1은 이 메시지에 대해 카운트가 필요하지 않음을 나타냅니다. 이 경우 우측 상단의 숫자는 증가하지 않습니다.|
| ApnsInfo.Title|String|옵션|APNs 푸시 메시지의 제목. 입력하면 가장 상단의 Title을 덮어쓰기합니다.|
| ApnsInfo.SubTitle|String|옵션|APNs 푸시 메시지의 부제목.|
| ApnsInfo.Image|String|옵션|해당 필드는 APNs에 포함된 이미지 URL. 클라이언트에서 이 필드를 획득하면 URL을 통해 이미지를 다운로드하여 팝업 창에 이미지를 표시합니다. |
| ApnsInfo.MutableContent | Integer | 옵션| 1: iOS 10+ 푸시 확장 활성화. 기본값: 0.|

>!APNs 푸시에서 지원하는 최대 데이터 패킷 크기는 4K입니다. Desc와 Ext 필드의 총 크기는 3K를 초과하지 않는 것이 좋습니다.

## 참고

Apple Push Notification Service(APNs) [Apple 푸시 개발 문서](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/Introduction.html#//apple_ref/doc/uid/TP40008194-CH1-SW1).
iOS 오프라인 메시지 푸시 설정: [Offline Push (iOS)](https://www.tencentcloud.com/document/product/1047/34347).
