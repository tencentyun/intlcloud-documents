ABS(Adaptive Bitrate Streaming) 트랜스 코딩이란 비디오를 트랜스 코딩 및 패키징하여 ABS 출력 파일로 만드는 과정을 가리킵니다. 특징으로 다양한 비트 레이트의 멀티미디어 파일과 설명 파일(manifest)이 포함되어 있으며, 플레이어는 현재 대역폭에 따라 최적의 비트 레이트를 동적으로 선택하여 재생할 수 있습니다. 현재 가장 널리 사용되는 ABS 포맷은 [Master Playlist](https://developer.apple.com/documentation/http_live_streaming/example_playlists_for_http_live_streaming/creating_a_master_playlist) 포맷의 HLS입니다.

VOD는 비디오를 HLS 및 MPEG-DASH 포맷의 ABS로 전환해주며, 이 기능을 통해 다음과 같은 효과를 얻을 수 있습니다.
* 플레이어는 현재 대역폭에 따라 적합한 비트 레이트를 동적으로 선택하여 시청자에게 우수한 시청 환경을 제공합니다.
* 메인 스트림 플레이어는 플레이어를 사용자 정의할 필요없이 기본적으로 HLS ABS를 지원합니다.
* VOD는 통합 후 편리하고 신속하게 ABS를 재생할 수 있는 [Player+ SDK](https://intl.cloud.tencent.com/document/product/266/7836)를 지원합니다.



## [](id:zsy)ABS 트랜스 코딩 템플릿

ABS 트랜스 코딩 매개변수로 ABS의 각 서브 스트림의 ‘비디오 트랜스 코딩 매개변수’, ‘오디오 트랜스 코딩 매개변수’ 등의 매개변수를 제어할 수 있습니다. VOD는 ABS 트랜스 코딩 템플릿을 사용하여 매개변수 집합을 나타내며, ABS 트랜스 코딩을 통해 다음과 같은 관련 매개변수를 지정할 수 있습니다.

| 매개변수 | 설명 |
| -- | -- |
| 먹싱 유형 | 어댑티브 스트림 형식, 현재 HLS 및 MPEG-DASH 지원 |
|암호화 유형|암호화 유형 현재 HLS 형식만 SimpleAES 암호화를 지원하고 DASH는 암호화는 미지원|
| 서브 스트림 사양 | 출력되는 서브 스트림 수와 각 서브 스트림의 비디오 트랜스 코딩 매개변수 및 오디오 트랜스 코딩 매개변수: <li>비디오 트랜스 코딩 매개변수: 해상도, 비트 레이트, 프레임 레이트, 인코딩 포맷 등</li><li>오디오 트랜스 코딩 매개변수: 샘플링 레이트, 사운드 채널 수, 인코딩 포맷 등</li> |
| ‘저해상도에서 고해상도로 전환’ 필터링 여부 | 일반적으로 저해상도의 원본 비디오를 고해상도로 트랜스 코딩하여 화질이나 음질을 향상시키는 것은 불가능합니다. ‘저해상도에서 고해상도로 전환’ 필터링을 활성화하면 불필요한 트랜스 코딩을 방지할 수 있습니다|

일반적인 매개변수 조합에 대해 VOD는 [사전 설정 ABS 트랜스 코딩 템플릿](https://intl.cloud.tencent.com/document/product/266/33932)을 제공하며, 사용자 정의 ABS 트랜스 코딩 템플릿도 지원합니다.

## 작업 시작

ABS 트랜스 코딩 작업을 시작하는 방법에는 ‘서버 API를 통한 직접 시작’, ‘콘솔을 통한 직접 시작’ 및 ‘업로드 시 실행할 작업 지정’ 세 가지 방법이 있습니다. 자세한 내용은 비디오 처리의 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33931)을 참조하십시오.

다음은 ABS 트랜스 코딩을 시작하는 다양한 방식에 관한 설명입니다.

* 서버 API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 호출하여 작업 시작: 요청의 `MediaProcessTask.AdaptiveDynamicStreamingTaskSet` 매개변수에 [ABS 트랜스 코딩 템플릿](#zsy)의 템플릿 ID를 지정합니다.
* 콘솔을 통해 비디오에 대한 작업 시작: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고, 태스크 플로우에 ABS 트랜스 코딩(`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`에서 지정) 작업을 구성하고, 콘솔에서 태스크 플로우를 사용하여 [비디오 처리 시작](https://intl.cloud.tencent.com/document/product/266/33892)을 진행합니다.
* 서버 업로드 시 작업 지정: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고 태스크 플로우에 ABS 트랜스 코딩(`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`에서 지정) 작업을 구성한 뒤, [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120)의 `procedure` 매개변수를 해당 태스크 플로우로 지정합니다.
* 클라이언트 업로드 시 작업 지정: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고 태스크 플로우에 ABS 트랜스 코딩(`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`에서 지정) 작업을 구성한 뒤, [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922)의 `procedure`를 해당 태스크 플로우로 지정합니다.
* 콘솔 업로드: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고, 태스크 플로우에 ABS 트랜스 코딩(`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`에서 지정) 작업을 구성합니다. 콘솔을 통해 비디오를 업로드한 뒤 [[업로드와 동시에 비디오 처리 작업 진행]](https://intl.cloud.tencent.com/document/product/266/33890)을 선택하고 비디오 업로드 후 해당 태스크 플로우를 실행하도록 지정합니다.

## 결과 가져오기

ABS 트랜스 코딩 작업을 시작한 후 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931)을 비동기적으로 기다리거나 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931)를 동기적으로 수행하여 ABS 트랜스 코딩 작업의 실행 결과를 얻을 수 있습니다. 다음은 ABS 트랜스 코딩 작업 시작 후 일반 콜백 방식으로 결과 알림을 받는 예시입니다(값이 null인 필드는 생략됨).

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
                "Type":"AdaptiveDynamicStreaming",
                "AdaptiveDynamicStreamingTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "Package":"hls",
                        "DrmType":"",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.10.m3u8"
                    }
                }
            },
            {
                "Type":"AdaptiveDynamicStreaming",
                "AdaptiveDynamicStreamingTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":20
                    },
                    "Output":{
                        "Definition":20,
                        "Package":"dash",
                        "DrmType":"",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.20.mpd"
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

콜백 결과 중 `ProcedureStateChangeEvent.MediaProcessResultSet`에는 `Type`이 `AdaptiveDynamicStreaming` 유형이고 `Definition`이 각각 10, 20인 두 개의 ABS 트랜스 코딩 결과가 존재합니다.

