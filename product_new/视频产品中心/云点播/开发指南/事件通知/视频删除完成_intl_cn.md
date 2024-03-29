>!
>- 本文档为3.0版本的格式回调，2.0版本的历史格式回调请参见 [历史格式回调](https://intl.cloud.tencent.com/document/product/266/33962#.E8.A7.86.E9.A2.91.E5.88.A0.E9.99.A4.E5.AE.8C.E6.88.90) 文档。
>- 建议您将回调版本逐步迁移到3.0格式，2.0格式回调的文档将不再维护。

## 事件名称
FileDeleted

## 事件说明
当 App 配置了事件通知，并且在视频删除后，App 后台即可通过“普通回调”或“可靠回调”的方式获取该事件通知。事件通知内容为 [FileDeleteTask 结构](https://intl.cloud.tencent.com/document/product/266/34187#FileDeleteTask)。


## 示例
### 普通回调
如果选择普通回调模式，则回调 URL 会接收到来自云点播的 HTTP 请求。请求采用 POST 方法，请求内容在 BODY 中，如下所示（省略了值为 null 的字段）。

```json
{
    "EventType":"FileDeleted",
    "FileDeleteEvent":{
        "FileIdSet":[
            "24961954183381008"
        ],
        "FileDeleteResultInfo":[
            {
                "FileId":"24961954183381008",
                "DeleteParts":[
                    {
                        "Type":"TranscodeFiles",
                        "Definition":0
                    }
                ]
            }
        ]
    }
}
```


### 可靠回调
如果选择可靠回调模式，调用 [拉取事件通知](https://intl.cloud.tencent.com/document/product/266/34187) API 会接收到如下形式的 HTTP 应答（省略了值为 null 的字段）。


```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "EventType":"FileDeleted",
                "FileDeleteEvent":{
                    "FileIdSet":[
                        "24961954183381008"
                    ],
                    "FileDeleteResultInfo":[
                        {
                            "FileId":"24961954183381008",
                            "DeleteParts":[
                                {
                                    "Type":"TranscodeFiles",
                                    "Definition":0
                                }
                            ]
                        }
                    ]
                }
            }
        ],
        "RequestId":"335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
