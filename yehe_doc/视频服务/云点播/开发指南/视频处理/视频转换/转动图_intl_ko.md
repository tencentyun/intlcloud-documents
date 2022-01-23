애니메이션 이미지는 비디오의 일정 부분을 선택해 움직이는 이미지(GIF, WEBP 등)를 생성하는 오프라인 작업입니다. 애니메이션 이미지는 연속 프레임의 매끄러운 순환이며, 적은 용량으로 애니메이션 효과를 구현합니다.
>? 애니메이션 이미지 생성이 지원되는 경우 원본 비디오에서 시작 시간과 종료 시간을 지정할 수 있으며 세그먼트는 애니메이션 이미지를 생성하기 위해 ‘캡처’됩니다.

<span id = "zdt"></span>
## 애니메이션 이미지 생성 템플릿


애니메이션 이미지의 대상 사양은 애니메이션 이미지 파일 형식, 너비, 높이 및 프레임 속도와 같은 매개변수의 적용을 받으며 아래와 같이 VOD 애니메이션 이미지 생성 템플릿의 형태로 사용자 정의할 수 있습니다.

| 매개변수             | 설명                                         |
| ---------------- | -------------------------------------------- |
| 포맷(Format)   | 애니메이션 이미지 파일의 출력 형식으로 현재 GIF와 WEBP만 지원. |
| 폭(Width)    | 애니메이션 이미지 너비. 값 범위: 128px - 4096px.              |
| 높이(Height) | 애니메이션 이미지 높이. 값 범위: 128px - 4096px.              |
| 프레임 레이트(FPS)      | 지원되는 프레임 속도 범위: 1fps - 60fps.                  |

공통 사양의 경우 VOD는 [사전 설정된 애니메이션 이미지 생성 템플릿](https://intl.cloud.tencent.com/document/product/266/33932#cinemagraph)을 제공합니다. 또한 콘솔에서 사용자 지정 애니메이션 이미지 생성 템플릿을 만들고 관리할 수도 있습니다. 자세한 내용은 [템플릿 설정](https://intl.cloud.tencent.com/document/product/266/14059#.E8.BD.AC.E5.8A.A8.E5.9B.BE.E6.A8.A1.E6.9D.BF)을 참고하십시오.

## 작업 시작
애니메이션 이미지 생성 작업을 시작하는 방법에는 ‘서버 API를 통해 직접 시작’, ‘콘솔을 통해 직접 시작’, ‘업로드 시 실행할 작업 지정’의 세 가지 방법이 있습니다. 자세한 내용은 비디오 처리의 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask)을 참고하십시오.

다음은 이러한 방식으로 애니메이션 이미지 생성 작업을 시작하기 위한 내용입니다.

* 서버 API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 호출하여 작업 시작: 요청의 `MediaProcessTask.AnimatedGraphicTaskSet` 매개변수에 [애니메이션 이미지 생성 템플릿](#zdt) ID를 지정합니다.
* 콘솔을 통해 비디오 작업 시작: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 애니메이션 이미지 사양을 설정하고, 태스크 플로우를 사용하여 [비디오 처리 시작](https://intl.cloud.tencent.com/document/product/266/33890)합니다.
* 서버에서 업로드 시 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 애니메이션 이미지 사양을 설정하고, 이 태스크 플로우를 [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) 요청의 `procedure`로 지정합니다.
* 클라이언트에서 업로드 시 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 애니메이션 이미지 사양을 설정하고, [클라이언트에서 업로드하기 위한 서명](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0)에서 이 태스크 플로우를 `procedure` 매개변수로 지정합니다.
* 콘솔을 통해 업로드: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 애니메이션 이미지 사양을 설정하고, 콘솔을 통해 비디오를 업로드한 후, [[업로드 중 비디오 처리]](https://intl.cloud.tencent.com/document/product/266/33890)를 선택하고, 비디오 업로드 완료 시 이 태스크 플로우를 실행하도록 지정합니다.

## 결과 가져오기

애니메이션 이미지 생성 작업을 시작한 후 비동기적으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification)을 기다리거나 동기적으로 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery)를 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 애니메이션 이미지 생성 작업이 시작된 후 일반 콜백 모드에서 결과 알림을 받는 예시입니다(null 값이 있는 필드는 생략됨).

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1256768367-Procedure-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "FileId":"5285890784246869930",
        "FileName":"동물의 세계",
        "FileUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/AtUCmy6gmIYA.mp4",
        "MetaData":{
            "AudioDuration":60,
            "AudioStreamSet":[
                {
                    "Bitrate":383854,
                    "Codec":"aac",
                    "SamplingRate":48000
                }
            ],
            "Bitrate":1021028,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":60,
            "Height":480,
            "Rotate":0,
            "Size":7700180,
            "VideoDuration":60,
            "VideoStreamSet":[
                {
                    "Bitrate":637174,
                    "Codec":"h264",
                    "Fps":23,
                    "Height":480,
                    "Width":640
                }
            ],
            "Width":640
        },
        "MediaProcessResultSet":[
            {
                "Type":"AnimatedGraphics",
                "AnimatedGraphicTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":20001,
                        "StartTimeOffset":2,
                        "StartTimeOffset":5
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20001.webp",
                        "Definition":20001,
                        "Container":"webp",
                        "Height":480,
                        "Width":640,
                        "Bitrate":324271,
                        "Size":121601,
                        "Md5":"084d403c73930ca2f835679af1f37bd3",
                        "StartTimeOffset":3,
                        "EndTimeOffset":5
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

콜백 결과에서 `ProcedureStateChangeEvent.MediaProcessResultSet`은 `Type`이 `AnimatedGraphics`인 트랜스코딩 결과를 포함합니다. `Definition`은 20001입니다.
