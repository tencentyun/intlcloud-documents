推流异常事件回调主要用于回调推流异常情况的具体信息，您需要在推流异常事件回调中配置回调地址，腾讯云直播后台会将类型结果回调到您设置的接收服务器中。
本文主要讲解触发推流异常事件回调后，腾讯云直播发送给用户的回调消息通知字段。

## 注意事项

阅读本文之前，希望您已经了解腾讯云直播是如何配置回调功能、您是如何接收回调消息的，具体请参见 [如何接收事件通知](https://intl.cloud.tencent.com/document/product/267/38080)。

## 推流异常事件参数说明
### 事件类型参数

| 事件类型 | 字段取值说明     |
| :------- | :--------------- |
| 推流异常事件 | event_type = 321 |

### 回调公共参数

| 参数            | 类型   | 含义                             |
| :-------------- | :----- | :------------------------------- |
| appid           | int    | 用户 APPID                       |
| stream_id       | string | 直播流名称                       |
| data_time       | int    | 推流事件回调时间（单位ms）       |
| report_interval | int    | 有异常事件时，上报间隔（单位ms） |
| abnormal_event  | json | 详细异常事件事件组               |

#### abnormal_event 内参数说明

<table>
<tr><th>参数</th><th>类型</th><th>含义</th></tr>
<tr>
<td>type</td>
<td>int</td>
<td>异常事件类型</td>
</tr><tr>
<td>count</td>
<td>int</td>
<td>对应异常事件单位时间（上报间隔内）发生次数</td>
</tr><tr>
<td>detail</td>
<td>json</td>
<td><li>desc：异常事件描述<li>occur_time：异常事件发生时间</td>
</tr><tr>
<td>type_desc_cn</td>
<td>string</td>
<td>异常事件中文描述</td>
</tr><tr>
<td>type_desc_en</td>
<td>string</td>
<td>异常事件英文描述</td>
</tr></table>
异常事件类型

| 类型 | 含义                             |
| :--- | :------------------------------- |
| 1    | 视频时间戳回退                   |
| 2    | 音频时间戳回退                   |
| 3    | 视频时间戳突然变大（大于1s）     |
| 4    | 音频时间戳突然变大（大于1s）     |
| 5    | chunk size 太大（大于8192）       |
| 6    | 两帧视频帧到达时间太长（大于3s） |
| 7    | 两帧音频帧到达时间太长（大于3s） |
| 8    | 视频编码类型发生变化             |
| 9    | 音频编码类型发生变化             |
| 10   | 视频帧到来前没有 codec 头          |
| 11   | 音频帧到来前没有 codec 头          |


>! 
- 当前推流异常事件回调不支持对单独事件进行配置，在每个上报间隔，对发生的异常事件进行回调；如果没有异常事件，则不进行回调。
- 推流异常事件回调仅对当前的推流异常进行统计，系统不会进行其他处理。


### 回调消息示例

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
            "type_desc_cn":"视频帧到达时间差值大于1000ms",
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
            "type_desc_cn":"音频帧到达时间差值大于1000ms",
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
