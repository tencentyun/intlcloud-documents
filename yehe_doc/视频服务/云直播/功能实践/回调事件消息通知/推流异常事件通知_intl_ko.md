푸시 오류 콜백은 푸시 오류의 세부 정보를 알려줍니다. CSS 콘솔에서 콜백 주소를 구성해야 하며 Tencent Cloud CSS는 설정된 서버로 푸시 오류 콜백을 보냅니다.
본 문서에서는 푸시 오류가 발생한 후 CSS에서 보내는 콜백 알림의 필드를 설명합니다.

## 주의 사항

Tencent Cloud CSS의 콜백 기능 구성 방법과 사용자가 콜백 메시지를 수신하는 방법을 숙지한 뒤 본 문서를 읽을 것을 권장합니다. 자세한 내용은 [이벤트 알림 수신 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참고하십시오.

## 푸시 오류 콜백 매개변수
### 이벤트 유형

| 이벤트 유형 | 매개변수 값     |
| :------- | :--------------- |
| 푸시 오류 | event_type = 321 |

### 일반 콜백 매개변수

| 매개변수            | 유형   | 설명                             |
| :-------------- | :----- | :------------------------------- |
| appid           | int    | 사용자 APPID                       |
| stream_id       | string | 스트림 ID                       |
| data_time       | int    | 콜백 시간(ms)       |
| report_interval | int    | 푸시 오류 발생 시 리포트 간격(ms) |
| abnormal_event  | json | 푸시 오류 세부 정보               |

#### abnormal_event 매개변수

<table>
<tr><th>매개변수</th><th>유형</th><th>설명</th></tr>
<tr>
<td>type</td>
<td>int</td>
<td>오류 유형</td>
</tr><tr>
<td>count</td>
<td>int</td>
<td>두 리포트 사이에 오류가 발생한 횟수(리포트 간격 내)</td>
</tr><tr>
<td>detail</td>
<td>json</td>
<td><li>desc: 오류 설명<li>occur_time: 오류 발생 시간</td>
</tr><tr>
<td>type_desc_cn</td>
<td>string</td>
<td>오류 중국어 설명</td>
</tr><tr>
<td>type_desc_en</td>
<td>string</td>
<td>오류 영어 설명</td>
</tr></table>
오류 유형

| 유형 | 설명                             |
| :--- | :------------------------------- |
| 1    | 비디오 타임스탬프가 뒤로 이동했습니다                   |
| 2    | 오디오 타임스탬프가 뒤로 이동했습니다                   |
| 3    | 비디오 타임스탬프가 갑자기 증가했습니다(1s 이상)     |
| 4    | 오디오 타임스탬프가 갑자기 증가했습니다(1s 이상)     |
| 5    | chunk size가 너무 큽니다(8192 이상)       |
| 6    | 2개의 연속 비디오 프레임이 늦게 도착했습니다(3s 이상) |
| 7    | 2개의 연속 오디오 프레임이 늦게 도착했습니다(3s 이상) |
| 8    | 비디오 코덱이 변경되었습니다             |
| 9    | 오디오 코덱이 변경되었습니다             |
| 10   | 비디오 프레임 도달 전에 codec 헤더가 없습니다          |
| 11   | 오디오 프레임 도달 전에 codec 헤더가 없습니다          |


>! 
>- 현재 특정 유형의 푸시 오류에 대한 콜백을 구성할 수 없습니다. 푸시 오류 콜백에는 리포트 간격 동안 발생한 모든 푸시 오류에 대한 정보가 포함됩니다. 푸시 오류가 발생하지 않으면 콜백이 전송되지 않습니다.
>- 푸시 오류 콜백은 현재 리포트 주기의 푸시 오류에 대한 데이터만 수집합니다. 시스템에서 오류를 처리하지 않습니다.


### 콜백 메시지 예시

```JSON
{
    "abnormal_event":[
        {
            "count":2,
            "detail":[
                {
                    "desc":"video frame arrive interval too long, interval=3046(msec)",
                    "occur_time":1670588070569
                },
                {
                    "desc":"video frame arrive interval too long, interval=2953(msec)",
                    "occur_time":1670588073522
                }
            ],
            "type":6,
            "type_desc_cn":"비디오 프레임 도착 간격이 1000(ms)보다 큽니다",
            "type_desc_en":"video frame arrive interval bigger than 1000(ms)"
        },
        {
            "count":2,
            "detail":[
                {
                    "desc":"audio frame arrive interval too long, interval=3009(msec)",
                    "occur_time":1670588070532
                },
                {
                    "desc":"audio frame arrive interval too long, interval=2917(msec)",
                    "occur_time":1670588073486
                }
            ],
            "type":7,
            "type_desc_cn":"오디오 프레임 도착 간격이 1000(ms)보다 큽니다",
            "type_desc_en":"audio frame arrive interval bigger than 1000(ms)"
        }
    ],
    "appid":0,
    "data_time":1670588074971,
    "domain":"xxxx.xxxxx.xxxx.xxxx",
    "event_type":321,
    "interface":"general_callback",
    "path":"xxxx",
    "report_interval":5000,
    "sequence":"000000000000000000",
    "stream_id":"xxxxxx",
    "stream_param":"txSecret=f5828cd4a8a09109304b060172fb3960&txTime=665982e4",
    "timeout":5000
}
```
