Relay callbacks are used to call back status information of relay tasks. You need to configure the callback address in a relay task and then Tencent Cloud CSS backend will call back different results to the specified server.

This document describes the parameters in callback message notifications sent by Tencent Cloud CSS after a stream push/interruption callback event is triggered.

 

## Notes

You need to understand how to configure callbacks and how will you receive messages via Tencent Cloud CSS before reading this document. For more information, see [How to Receive Event Notifications](https://intl.cloud.tencent.com/document/product/267/38080).

 

## Relay Event Parameters

### Event type parameters

| Event Type | Parameter Value |
| :------- | :--------------- |
| Relay | event_type = 314 |


### Common callback parameters

| Parameter    | Type   | Description                                                                                                                    |
| ---------------  | ----------- | ----------- |
| appId      | int    | User `APPID`                                   |
| callback_event  | string     | Callback event type           |
| source_urls     | string     | Pull source URLs            |
| to_url          | string     | Push destination URL           |
| stream_id    | string | Live stream name                  |
| task_id | string | Task ID |
| [msg](#msg)     | string           | Callback details of different types of events |

[](id:msg)
#### Parameters in `msg`

| Parameter    | Type   | Description        |
| ---------------  | ----------- | ----------- |
| task_start_time  | int        | Task start timestamp, in milliseconds   |
| url              | string     | Source URL of the current pull task      |
| index            | string     | Index of the list for on-demand files     |
| duration         | int        | Duration of an on-demand file, in seconds        |
| task_exit_time   | int       | Task stop timestamp, in milliseconds |
| code             | string       | Task stop error code |
| message          | string     | Task stop error message         |

### Sample callback message

#### `TaskStart` - Callback of the task start event
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

#### `VodSourceFileStart` - Callback of the on-demand file’s start
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


#### `VodSourceFileFinish` - Callback of the on-demand file’s end
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

#### `TaskExit` - Callback of the task stop event
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
>- Sequence of callbacks for relay tasks with “Video on-demand” as the source content: `TaskStart` - Callback of the task start event > `VodSourceFileStart` - Callback of the on-demand file’s start > `VodSourceFileFinish` - Callback of the on-demand file’s end.
>- There is an interval of **up to 2s** between `TaskStart` and `VodSourceFileStart` callbacks.
>- Callback settings are included in the relay task configuration. For detailed directions, see [Relay](https://intl.cloud.tencent.com/zh/document/product/267/2818).


