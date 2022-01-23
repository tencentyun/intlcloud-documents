비디오 편집은 VOD에서 비디오를 자르고 연결하는 오프라인 작업입니다. 구체적으로 다음과 같은 기능을 포함합니다.

* **동영상 클리핑**: VOD의 파일을 클리핑하여 새 동영상을 생성하는 것을 말합니다.
* **동영상 접합**: VOD의 여러 파일을 연결하여 새 동영상을 생성하는 것을 말합니다.
* **동영상 클립 접합**: VOD에서 여러 파일을 클리핑한 다음 클립을 접합하여 새 동영상을 생성하는 것을 말합니다.
* **라이브 스트림 트랜스코딩**: 스트림을 VOD로 트랜스코딩하여 새 동영상을 생성하는 것을 말합니다.
* **라이브 스트림 클리핑**: 새 동영상을 생성하기 위해 VOD에서 스트림을 클리핑하는 것을 말합니다.
* **라이브 스트림 접합**: VOD의 여러 스트림을 접합하여 새 동영상을 생성하는 것을 말합니다.
* **라이브 스트림 클립 접합**: VOD에서 여러 스트림을 클리핑한 다음 클립을 접합하여 새 동영상을 생성하는 것을 말합니다.

>!라이브 스트림에서 클리핑, 접합 또는 기타 작업을 수행하려면 종료 후 작업해야 합니다. 그렇지 않으면 생성된 동영상이 불완전할 수 있습니다.

생성된 비디오의 컨테이너 형식은 MP4입니다. 비디오 편집 작업을 시작할 때 새 비디오에 대해 [태스크 플로우](https://intl.cloud.tencent.com/document/product/266/33931) 수행 여부를 지정할 수 있습니다.

## 작업 시작

[서버 API](https://intl.cloud.tencent.com/document/product/266/34126)를 호출하여 비디오 편집 작업을 시작할 수 있습니다. API의 반환 결과에는 [결과 가져오기](#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96) 시 해당 작업 결과와 연결하는 데 사용되는 작업 ID가 포함됩니다.

## 결과 가져오기

편집 작업을 시작한 후 비동기화 방식으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931)을 기다리거나 동기적으로 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931)를 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 편집 작업이 시작된 후 일반 콜백 모드로 결과 알림을 받는 예시입니다(null 값이 있는 필드는 생략됨).

```json
{
    "EventType":"EditMediaComplete",
    "EditMediaCompleteEvent":{
        "TaskId":"EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"SUCCESS",
        "Input":{
            "InputType":"File",
            "FileInfoSet":[
                {
                    "FileId":"24961954183381008",
                    "StartTimeOffset":0,
                    "EndTimeOffset":300
                },
                {
                    "FileId":"24961954183381009",
                    "StartTimeOffset":0,
                    "EndTimeOffset":300
                },
                {
                    "FileId":"24961954183381010",
                    "StartTimeOffset":0,
                    "EndTimeOffset":300
                }
            ]
        },
        "Output":{
            "FileType":"mp4",
            "FileId":"24961954183923290",
            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
        },
        "ProcedureTaskId":""
    }
}
```

콜백 결과에서 `Input.InputType`은 `File`로 편집된 동영상의 타입이 파일 타입임을 나타냅니다. `Input.FileInfoSet`에는 `StartTimeOffset`이 `0`이고 `EndTimeOffset`이 `300`인 3개의 요소가 포함되어 있습니다. 이는 3개의 비디오 각각의 처음 5분을 잘라낸 다음 15분 길이의 동영상으로 연결함을 나타냅니다. `Output.FileId`는 재생 URL이 `FileUrl`의 값인 생성된 비디오의 FileId입니다.
