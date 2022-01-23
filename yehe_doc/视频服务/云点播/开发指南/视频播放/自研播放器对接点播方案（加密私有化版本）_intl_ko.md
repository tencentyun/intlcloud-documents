VOD는 긴 동영상 및 동영상 암호화 시나리오를 위해 Android, iOS 및 Web용 [재생 SDK](https://intl.cloud.tencent.com/document/product/266/7836)를 제공합니다. VOD SDK를 사용하여 VOD 재생 기능을 빠르게 통합할 수 있습니다. VOD Superplayer SDK가 사용자 정의 요구 사항을 충족할 수 없는 경우 아래에 자세히 설명된 대로 SDK와 VOD 백엔드 간의 통신 프로토콜을 참고하여 자체 제작 플레이어를 구현할 수도 있습니다. 

## 프로토콜
HTTP Get에서 요청이 시작되고 URL은 `https://playvideo.qcloud.com/{interface}/{version}/{appId}/{fileId}?psign=xxx`입니다.

### 도메인 이름
* 기본 도메인 이름: `playvideo.qcloud.com`
* 백업 도메인 이름: `bkplayvideo.qcloud.com`

### 요청 필드
#### path 필드

| 필드 | 필수 입력 여부 | 필드 값 |
| -- | -- | -- |
| appId | Yes | appid를 입력합니다(서브 애플리케이션을 사용하는 경우 subappid 입력). |
| fileId | Yes | 재생할 비디오 파일의 ID입니다. |
| version | Yes | 항상 v4를 입력합니다. |
| interface | Yes | 항상 getplayinfo를 입력합니다. |

#### querystring 필드

| 필드 | 필수 입력 여부 | 필드 값 |
| -- | -- | -- |
| psign | No | Superplayer 서명. 매개변수는 아래의 Superplayer 서명 섹션을 참고하십시오. 서명 알고리즘은 [Superplayer 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 참고하십시오. |

### 응답 필드

| 매개변수 | 유형 | 설명 |
| -- | -- | -- |
| code | Integer | 오류 코드. code가 0이 아닐 때 오류를 나타냅니다. |
| message | String | 오류 메시지. code가 0이 아닐 때 값을 가집니다. |
| version | Integer | 현재 반환된 결과 버전의 유형으로 4로 고정됩니다. |
| warning | String | 경고 메시지. psign 매개변수가 전달되지만 링크 도용 방지가 활성화되지 않은 경우 경고가 반환됩니다. |
| media | Object | 미디어 정보. 요소 유형은 미디어입니다.|

#### Media 유형

| 매개변수 | 유형 | 설명 |
| -- | -- | -- |
| basicInfo | Object | BasicInfo 유형의 기본 비디오 정보입니다. |
| streamingInfo | Object | StreamingInfo 유형의 다중 비트 전송률 비디오 정보입니다. |
| imageSpriteInfo | Object | 플레이어가 비디오를 미리 보기 위해 주로 사용하는 ImageSpriteInfo 유형의 썸네일 정보입니다. |
| keyFrameDescInfo | Object | 플레이어가 비디오를 타임스탬프하는 데 사용하는 KeyFrameDescInfo 유형의 비디오 타임스탬프 정보입니다. |

#### BasicInfo 유형

| 매개변수 | 유형 | 설명 |
| -- | -- | -- |
| Name     | String   | 비디오 이름.  |
| size | Integer | 비디오 크기, 단위: 바이트. |
| duration | Float | 비디오 지속 시간, 단위: 초. |
| description | String | 비디오 설명. |
| coverUrl | String | 비디오 썸네일의 URL. |

#### StreamingInfo 유형

| 매개변수 | 유형 | 설명 |
| -- | -- | -- |
|plainOutput|String|암호화되지 않은 출력, 유형은 StreamingOutput. |
|drmOutput|Array|동영상이 DRM으로 암호화된 후 출력, 유형은 StreamingOutput. |
|drmToken|String|DRM 암호화 출력이 재생될 때 사용되는 DRM Token입니다. 재생하려면 이 필드를 streamingOutput.url에 추가해야 합니다. |

#### StreamingOutput 유형

| 매개변수 | 유형 | 설명 |
| -- | -- | -- |
| type | String | 어댑티브 비트스트림 보호 유형. 유효한 값: plain(암호화 없음), simpleAES(HLS 공통 암호화). |
| url | String | 재생 URL. |
| subStreams | Array | SubStreamInfo 유형의 서브 스트림 정보입니다. |

#### SubStreamInfo 유형

| 매개변수 | 유형 | 설명 |
| -- | -- | -- |
| type | String | 서브스트림 유형. 유효한 값: 비디오. |
| width | Integer | 서브스트림 비디오 너비. 단위: px. |
| height | Integer | 서브스트림 비디오 높이. 단위: px. |
| resolutionName | String | 플레이어에 표시되는 서브 스트림 비디오의 사양 이름입니다. |

#### ImageSpriteInfo 유형

| 매개변수 | 유형 | 설명 |
| -- | -- | -- |
| imageUrls | Array | String 유형의 썸네일 다운로드 URL 배열입니다. |
| webVttUrl | String | 썸네일 VTT 파일 다운로드 URL. |

### 재생
#### 암호화되지 않은 출력 재생
요청의 반환 결과가 암호화되지 않은 비디오인 경우(즉, streamingOutput.type이 plain인 경우) streamingOutput.url의 링크를 직접 사용하여 재생합니다.

#### 암호화된 출력 재생
요청의 반환 결과가 암호화된 비디오인 경우(즉, streamingOutput.type이 simpleAES인 경우), streamingInfo.drmToken을 streamingOutput.url의 파일 이름에 추가하여 재생 링크를 생성해야 합니다.

**접합 규칙**: 새 파일 이름 = voddrm.token.{추가할 token}.{기존 파일 이름}

예를 들어, streamingOutput.url이 `http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.m3u8?t=5c08d9fa&us=someus&sign=xxx`이고 drmToken이 `JhbGciOxxxsInR5cCI6Ikp`인 경우.
재생 URL은 다음과 같습니다.
`http://125xxx167.vod2.myqcloud.com/xxx/xxx/voddrm.token.JhbGciOxxxsInR5cCI6Ikp.xx.m3u8?t=5c08d9fa&us=someus&sign=xxx`.

### 비즈니스 흐름도
#### 암호화되지 않은 체계의 전체 비즈니스 흐름도

![](https://main.qcloudimg.com/raw/33e3cdeb424ca34f0ec2cb873a35ff7f.png)

#### 업그레이드된 암호화 체계의 전체 비즈니스 흐름도

![](https://main.qcloudimg.com/raw/8533090da512fe2d87b9a6a7d15add6a.png)



## 예시
다음은 비디오의 암호화된 출력을 재생하는 예시입니다.

### 요청
`https://playvideo.qcloud.com/getplayinfo/v4/125xxx167/52858xxx74597?psign=0eef1a12dxxxf0f48ebf34b4`

### 응답
```json
{
    "code":0,
    "message":"",
    "requestId":"377d94185f0342c5b67b038501f54974",
    "version":4,
    "context":"",
    "warning":"",
    "media":{
        "basicInfo":{
            "name":"동물의 세계",
            "size":26246026,
            "duration":30.5,
            "description":"CCTV의 고전 동물 프로그램",
            "coverUrl":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.jpg?t=5c08d9fa&amp;someus&amp;sign=xxx"
        },
        "streamingInfo":{
            "plainOutput":{

            },
            "drmOutput":[
                {
                    "type":"simpleAes",
                    "url":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.m3u8?t=5c08d9fa&amp;us=someus&amp;sign=xxx",
                    "subStreams":[
                        {
                            "type":"video",
                            "width":427,
                            "height":240,
                            "resolutionName":"Smooth"
                        },
                        {
                            "type":"video",
                            "width":853,
                            "height":480,
                            "resolutionName":"SD"
                        },
                        {
                            "type":"video",
                            "width":1280,
                            "height":720,
                            "resolutionName":"HD"
                        }
                    ]
                }
            ],
            "drmToken":"JhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9xxx",
        },
        "imageSpriteInfo":{
            "imageUrls":[
                "http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.jpg?t=5c08d9fa&amp;us=someus&amp;sign=xxx"
            ],
            "webVttUrl":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.vtt?t=5c08d9fa&amp;us=someus&amp;sign=xxx"
        },
        "keyFrameDescInfo":{
            "keyFrameDescList":[
                {
                    "timeOffset":1.1,
                    "content":"곧 시작합니다..."
                },
                {
                    "timeOffset":100.2,
                    "content":"곧 끝납니다..."
                }
            ]
        }
    }
}
```

## 용어 사전
| 이름 |의미 |
| -- | -- |
| 콘텐츠 키 Key | SimpleAES로 비디오를 암호화한 후 m3u8 파일의 EXT-X-KEY 태그에 있는 URI에서 콘텐츠 키를 가져올 주소를 지정하면 플레이어 재생시 실시간으로 키를 획득한 후 재생을 위해 복호화합니다. 128바이트의 이진 데이터. |


## 디버깅 제안
디버깅을 위해 다음을 확인하는 것이 좋습니다.
1. 암호화되지 않은 재생.
2. 개인 암호화 재생.



