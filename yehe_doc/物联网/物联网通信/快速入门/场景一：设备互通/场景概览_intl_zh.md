## 操作场景
假设一个智能家居的场景（非实际产品，仅用于阐述物联网通信功能），如需实现如下图功能，您可以参考本文档进行操作。
![come_home](https://main.qcloudimg.com/raw/7a705176f8cba804b72d1e4519e93151.png)


## 解决方案
基于腾讯物联网通信，我们可以通过 SDK 创建两类智能设备（Door、AirConditioner），基于设备间的消息和规则引擎实现设备之间的联动，如下图所示：
![rule_engine_for_smart_home](https://main.qcloudimg.com/raw/f4c5186f03f8636eb8f8d80622b49b02.png)


>! airConditioner1 不可以通过直接订阅 door1 的 update 消息来完成消息通信，原因请参考 [功能组件 > 权限管理](https://intl.cloud.tencent.com/document/product/1105/41500) 。
