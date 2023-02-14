Push error callbacks notify you of the details of push errors. You need to configure a callback address in the CSS console, and CSS will send push error callbacks to the server you configured.
This document describes the fields in a callback notification sent by CSS after a push error occurs.

## Must-Knows

This guide assumes that you understand how to configure callbacks and receive callback notifications from CSS. For details, see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080).

## Push Error Callback Parameters
### Event type

| Event Type | Parameter Value           |
| :------- | :--------------- |
| Push errors | event_type = 321 |

### Common callback parameters

| Parameter       | Type                            | Description  |
| :-------------- | :----- | :------------------------------- |
| appid      | int    | The user’s App ID.                                   |
| stream_id    | string | The stream ID.                  |
| data_time       | int    | The callback time (ms).       |
| report_interval | int    | The reporting interval (ms) when a push error occurs. |
| abnormal_event  | json | The push error details.               |

#### `abnormal_event` parameters

<table>
<tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
<tr>
<td>type</td>
<td>int</td>
<td>The error type.</td>
</tr><tr>
<td>count</td>
<td>int</td>
<td>The number of times the error occurred between two reports (within the reporting interval).</td>
</tr><tr>
<td>detail</td>
<td>json</td>
<td><li>desc: The error description.<li>occur_time: The time when the error occurred.</td>
</tr><tr>
<td>type_desc_cn</td>
<td>string</td>
<td>The error description in Chinese.</td>
</tr><tr>
<td>type_desc_en</td>
<td>string</td>
<td>The error description in English.</td>
</tr></table>
Error types

| Type | Description                             |
| :--- | :------------------------------- |
| 1    | The video timestamp moved backwards.                   |
| 2    | The audio timestamp moved backwards.                   |
| 3    | The video timestamp increased notably (by more than one second).     |
| 4    | The audio timestamp increased notably (by more than one second).     |
| 5    | Chunk size too big (bigger than 8,192).       |
| 6    | Two consecutive video frames arrived late (by longer than three seconds).  |
| 7    | Two consecutive audio frames arrived late (by longer than three seconds).  |
| 8    | The video codec changed.             |
| 9    | The audio codec changed.             |
| 10   | No codec header before a video frame arrived.          |
| 11   | No codec header before an audio frame arrived.          |


>! 
- Currently, you cannot configure callbacks for a specific type of push error. A push error callback includes the information of all push errors that occurred during the reporting interval. If no push errors occur, no callbacks will be sent.
- A push error callback only collects data for push errors in the current reporting cycle. The system will not handle the errors.


### Sample callback

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
            "type_desc_cn":" ",
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
            "type_desc_cn":" ",
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
