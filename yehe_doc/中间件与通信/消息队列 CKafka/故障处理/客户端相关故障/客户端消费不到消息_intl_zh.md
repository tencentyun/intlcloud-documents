## 问题概述
消费端拉取不到消息。

## 可能原因
确认消费者组是否有堆积。如果没有堆积则会在 fetch.max.wait 时间后，返回空消息。该参数是消费者客户端配置的参数，默认是500ms，配置项如下：
```
# Fetch 请求等待时间
fetch.max.wait.ms=500
```

![](https://qcloudimg.tencent-cloud.cn/raw/eb6f5565a35eff67ee44e7b64104be98.png)

## 解决方法
- 如果消息有堆积，拉取到的消息却为空，建议检查客户端 SDK 的版本，如果 SDK 版本较老，建议升级 SDK 版本，参考 [SDK 文档](https://intl.cloud.tencent.com/document/product/597/41028)。
- 您也可以联系 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 处理。





