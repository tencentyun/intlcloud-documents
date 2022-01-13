풀 스트림 푸시 콜백은 주로 풀 스트림 푸시 작업의 상태 정보를 콜백하는 데 사용됩니다. 풀 스트림 푸시 작업에서 콜백 주소를 설정해야 하며, Tencent Cloud CSS 백그라운드에서 유형 결과를 설정된 수신 서버로 콜백합니다.

본 문서에서는 스트림 푸시 및 중단 콜백 이벤트 발생 시 Tencent Cloud CSS가 사용자에게 전송하는 콜백 메시지 알림 필드에 대해 설명합니다.

 

## 주의 사항

Tencent Cloud CSS의 콜백 기능 설정 방법과 사용자가 콜백 메시지를 수신하는 방법을 숙지한 뒤 본 문서를 열람할 것을 권장합니다. 자세한 내용은 [이벤트 알림 수신 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참고하십시오.

 

## 풀 스트림 푸시 이벤트 매개변수 설명

### 이벤트 유형 매개변수

| 이벤트 유형 | 필드값 설명 |
| :------- | :--------------- |
| 풀 스트림 푸시 | event_type = 314 |


### 콜백 공용 매개변수

| 매개변수           | 유형   | 의미                                              |
| ---------------  | ----------- | ----------- |
| appid            |int        | 사용자 APPID             |
| callback_event  | string     | 콜백 이벤트 유형           |
| source_urls     | string     | 풀 스트림 소스 URL             |
| to_url          | string     | 푸시 스트림 타깃 URL           |
| stream_id       | string     | 라이브 방송 스트림 이름                   |
| task_id         | string           | 작업 ID                |
| [msg](#msg)     | string           | 이벤트별 자세한 콜백 정보 |

[](id:msg)
#### msg 내 매개변수 설명

| 매개변수             | 유형                                        | 의미                     |
| ---------------  | ----------- | ----------- |
| task_start_time  | int        | 작업 시작 시간, 밀리초 타임스탬프  |
| url              | string     | 현재 풀링 중인 소스 URL       |
| index            | string     | VOD 파일이 있는 리스트 인덱스     |
| duration         | int        | VOD 파일 길이, 초         |
| task_exit_time   | int       | 작업 종료 시간, 밀리초 타임스탬프 |
| code             | string           | 작업 종료 오류 코드           |
| message          | string     | 작업 종료 오류 메시지         |

### 콜백 메시지 예시

#### TaskStart - 작업 시작 콜백
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "TaskStart",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"task_start_time\":0}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_230753472*****21162358-upload-45eb/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118148",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>

#### VodSourceFileStart - VOD 파일 시작 시 콜백
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "VodSourceFileStart",
    
    "callback_url": "http://you.callback.url",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"url\":\"http://remit-tx-ugcpub.douyucdn2.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\",\"index\":0,\"duration\":14920}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118145",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>


#### VodSourceFileFinish - VOD 파일 종료 시 콜백
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "VodSourceFileFinish",
    
    "callback_url": "http://you.callback.url",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"url\":\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\",\"index\":0,\"duration\":14920}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118145",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>

#### TaskExit - 작업 종료 콜백
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "TaskExit",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"message\":\"write packet error.\",\"code\":-22,\"task_exit_time\":0}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_230753472*****21162358-upload-4\"]\n"
}
:::
</dx-codeblock>

>!
>- VOD 풀 스트림 푸시 콜백 순서 설정은 다음과 같습니다. 'TaskStart-작업 시작 콜백' > 'VodSourceFileStart-VOD 파일 시작 시 콜백' > 'VodSourceFileFinish-VOD 파일 종료 콜백'.
>- 'TaskStart-작업 시작 콜백' 및 'VodSourceFileStart-VOD 파일 시작 시 콜백' 두 콜백 사이에 **2초 이내**의 간격이 있습니다.
>- 풀 스트림 푸시 콜백 설정은 풀 스트림 푸시 작업에서 설정합니다. 구체적인 방법은 [풀 스트림 푸시](https://intl.cloud.tencent.com/zh/document/product/ 267/2818)를 참고하십시오.


