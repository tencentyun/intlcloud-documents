트랜스코딩은 소스 오디오/비디오 비트스트림을 변환하는 오프라인 작업입니다. 코덱, 해상도 및 비트레이트와 같은 소스 비트스트림의 매개변수를 변경하여 다른 장치 및 네트워크 조건에 적용합니다. 트랜스코딩을 통해 얻을 수 있는 이점은 다음과 같습니다. 
- 호환성 향상: 원활한 재생을 위해 더 많은 유형의 장치와 호환되는 형식(예: MP4)으로 소스 비디오를 트랜스 코딩합니다.
- 대역폭 적응성 향상: 소스 비디오를 SD, HD 및 UHD로 출력하도록 트랜스 코딩합니다. 최종 사용자는 네트워크 조건에 맞는 비트레이트를 선택할 수 있습니다.
- 재생 효율성 향상: MOOV 아톰은 MP4 파일의 끝에서 시작 부분으로 이동할 수 있으므로 비디오가 완전히 다운로드되기 전에 재생할 수 있습니다.
- 워터마킹: 비디오에 워터마크를 추가하여 소유권 또는 저작권을 표시할 수 있습니다. 자세한 내용은 [워터마킹](https://intl.cloud.tencent.com/document/product/266/33939)을 참고하십시오.
- 대역폭 절약: 트랜스코딩에 고급 인코딩 모드(예: H.265)를 사용하여 원본 품질을 유지하면서 비디오의 비트레이트를 줄여 투자 회수 대역폭 사용량을 줄입니다.

비디오가 트랜스코딩된 후 [결과 가져오기](#jghq)에 따라 출력 비디오의 재생 URL을 얻을 수 있습니다. 자체 플레이어 또는 타사 플레이어를 사용하여 출력 비디오를 재생할 수 있습니다.

>!트랜스코딩 기능은 주로 **UGSV** 시나리오에 적합합니다. **긴 비디오** 시나리오(비디오 웹사이트, 온라인 교육 등)의 경우 [어댑티브 비트레이트 스트리밍으로 트랜스코딩](https://intl.cloud.tencent.com/document/product/266/33942)이 더 나은 사용자 경험을 제공할 수 있습니다.

<span id="zm"></span>
## 트랜스 코딩 템플릿

트랜스코딩 후 출력 비디오의 대상 사양은 코덱, 해상도 및 비트레이트와 같은 매개변수로 지정됩니다. VOD는 아래와 같이 트랜스코딩 템플릿에 이러한 매개변수를 통합합니다.
>?더 많은 오디오/비디오 트랜스코딩 유형은 [지원되는 트랜스코딩 유형](https://intl.cloud.tencent.com/document/product/266/7898)을 참고하십시오.
<table>
    <tr>
        <th style="width:18%">
            유형
        </th>
        <th style="width:22%">
            매개변수
        </th>
        <th>
            설명
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            MU(Muxing) 유형
        </td>
    </tr>
    <tr>
        <td>
            컨테이너 형식
        </td>
        <td>
			트랜스코딩에 지원되는 비디오 및 오디오 컨테이너 형식:
            <li>비디오: MP4、TS、HLS、FLV</li>
            <li>오디오: MP3、M4A、FLAC、OGG</li>
        </td>
    </tr>
    <tr>
        <td>
            비디오 스트림 삭제
        </td>
        <td>
            활성화되면 출력 비디오에는 비디오 스트림이 없는 오디오 스트림만 포함됩니다.
        </td>
    </tr>
    <tr>
        <td>
            오디오 스트림 삭제
        </td>
        <td>
            활성화되면 출력 비디오에는 오디오 스트림이 없는 비디오 스트림만 포함됩니다.
        </td>
    </tr>
    <tr>
        <td rowspan=7>
            비디오 인코딩
        </td>
        <td>
            코덱(Codec)
        </td>
        <td>
            H.264 및 H.265 지원
        </td>
    </tr>
    <tr>
        <td>
            비트레이트(Bitrate)
        </td>
        <td>
            지원되는 비트레이트 범위: 10Kbps - 35Mbps
        </td>
    </tr>
    <tr>
        <td>
            프레임 레이트(Frame Rate)
        </td>
        <td>
            지원되는 프레임 속도 범위: 1fps - 60fps, 공통 값: 24fps, 25fps 및 30fps
        </td>
    </tr>
    <tr>
        <td>
            해상도(Resolution)
        </td>
        <td>
            <li>지원되는 너비 범위: 128px - 4096px</li>
            <li>지원되는 높이 범위: 128px - 4096px</li>
        </td>
    </tr>
    <tr>
        <td>
            GOP 길이
        </td>
        <td>
            지원되는 GOP 길이 범위: 1초 - 10초
        </td>
    </tr>
    <tr>
        <td>
            프로파일(Profile)
        </td>
        <td>
            <li>비디오 코덱이 H.264일 때 Baseline, Main, High 프로파일 지원</li>
            <li>비디오 코덱이 H.265일 때  Main 프로파일만 지원</li>
        </td>
    </tr>
    <tr>
        <td>
            색 공간(Color Space)
        </td>
        <td>
            YUV420P 지원
        </td>
    </tr>
    <tr>
        <td rowspan=4>
            오디오 코덱
        </td>
        <td>
            코덱(Codec)
        </td>
        <td>
            MP3, AAC, AC3 및 FLAC 지원
        </td>
    </tr>
    <tr>
        <td>
            샘플링 레이트(Sample Rate)
        </td>
        <td>
            다음 오디오 샘플 속도 지원
            <li>34000Hz</li>
            <li>44100Hz</li>
            <li>48000Hz</li>
        </td>
    </tr>
    <tr>
        <td>
            비트레이트(Bitrate)
        </td>
        <td>
            지원되는 비트레이트 범위: 26kbps - 256kbps, 다음 값 포함:
            <li>48kbps</li>
            <li>64kbps</li>
            <li>128kbps</li>
        </td>
    </tr>
    <tr>
        <td>
            사운드 채널(Channel)
        </td>
        <td>
        	<li>싱글 사운드 채널</li>
			    <li>스테레오</li>
			    <li>입체 사운드 채널</li>
        </td>
    </tr>
</table>

VOD는 일반적인 트랜스코딩 사양에 대한 [사전 설정 매개변수 템플릿 목록](https://intl.cloud.tencent.com/document/product/266/33932)을 제공합니다. 또한 콘솔(자세한 지침은 [템플릿 설정](https://intl.cloud.tencent.com/document/product/266/14059) 참고) 또는 [서버 API](https://intl.cloud.tencent.com/document/product/266/34164)를 통해 사용자 지정 트랜스코딩 템플릿을 만들고 관리할 수 있습니다.

## 작업 시작

트랜스코딩 작업을 시작하는 방법에는 ‘서버 API를 통해 직접 시작하는 방법’, ‘콘솔을 통해 직접 시작하는 방법’, ‘업로드 시 실행할 작업 지정’의 세 가지가 있습니다. 자세한 내용은 비디오 처리의 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33931)을 참고하십시오.

트랜스코딩 작업 시작 방법:

* 서버 API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 호출하여 작업 시작: 요청의 `MediaProcessTask.AdaptiveDynamicStreamingTaskSet` 매개변수에 [트랜스 코딩 템플릿](#zm) ID를 지정합니다.
* 콘솔을 통해 비디오에 대한 작업 시작: 콘솔에 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 트랜스코딩 출력 사양을 설정하고, [비디오 처리 시작](https://intl.cloud.tencent.com/document/product/266/33892)에 사용합니다.
* 서버에서 업로드 시 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 트랜스코딩 출력 사양을 설정하고, 이를 [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120) API에서 `procedure` 매개변수로 지정합니다.
* 클라이언트에서 업로드 시 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 트랜스코딩 출력 사양을 설정하고, [클라이언트에서 업로드하기 위한 서명](https://intl.cloud.tencent.com/document/product/266/33922)에서 `procedure` 매개변수로 지정합니다.
* 콘솔을 통해 업로드: 콘솔에 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 트랜스코딩 출력 사양을 설정하고, 콘솔을 통해 비디오를 업로드한 후, [업로드 중 비디오 처리](https://intl.cloud.tencent.com/document/product/266/33890)를 선택하고, 비디오 업로드 완료 시 이 태스크 플로우를 실행하도록 지정합니다.
<span id="jghq"></span>
## 결과 가져오기

트랜스코딩 작업을 시작한 후 비동기식으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931)을 기다리거나 동기식으로 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931)를 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 일반 콜백에서 결과 알림을 받는 예입니다(null 값이 있는 필드는 생략됨). 

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
                "Type":"Transcode",
                "TranscodeTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":220
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20.m3u8",
                        "Size":63120997,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Height":480,
                        "Width":640,
                        "Bitrate":513402,
                        "Md5":"084d403c73930ca2f835679af1f37bd3",
                        "Duration":60,
                        "VideoStreamSet":[
                            {
                                "Bitrate":473101,
                                "Codec":"h264",
                                "Fps":24,
                                "Height":480,
                                "Width":640
                            }
                        ],
                        "AudioStreamSet":[
                            {
                                "Bitrate":48581,
                                "Codec":"aac",
                                "SamplingRate":44100
                            }
                        ],
                        "Definition":220
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

콜백 결과에서 `ProcedureStateChangeEvent.MediaProcessResultSet`에는 `Type`이 `Transcode`인 트랜스코딩 결과가 포함되어 있습니다. `Definition`은 220입니다.
