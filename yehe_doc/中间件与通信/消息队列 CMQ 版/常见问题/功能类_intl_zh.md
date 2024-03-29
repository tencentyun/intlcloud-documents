### TDMQ CMQ 版可以使用外网域名吗？
TDMQ CMQ 版可以使用外网域名，具体地址在控制台的 **API请求地址**获取。推荐您使用内网域名，**使用外网会收取流量费用，且外网时延可能费用较高**。 

### 协作者账户可以使用 TDMQ CMQ 版吗？
目前协作者、子账户均可以使用 TDMQ CMQ 版, 需要在 CAM 开通 TDMQ CMQ 版对应的资源操作权限。

### 当前队列的消息数小于当前请求的批量消费数量，请求会阻塞吗？
不会阻塞。

### 目前 SDK 是异步模式吗？
HTTP SDK 所有操作均为同步模式，TCP SDK 接入可选择异步模式。

### 可以在图形管理界面中查看队列的情况吗？
TDMQ CMQ 版提供可视化控制台，您可以很方便地查看当前队列情况。
[进入控制台 >>](https://console.intl.cloud.tencent.com/tdmq)

### TDMQ CMQ 版目前支持 MQTT 协议吗？
TDMQ CMQ 版目前不支持 MQTT 协议。

### TDMQ CMQ 版收发消息大小有限制吗？
TDMQ CMQ 版单条消息大小为1MB，单次请求的大小为1MB（指 HTTP post body 大小上限为1MB）。**当消息体大于1KB时，建议使用 post 请求方式，get 方式会被截断触发异常。**
如果消息超过1MB，您可通过以下两种方法解决：
- 将消息存储在 COS 中，然后把 Object 地址放在 TDMQ CMQ 版消息中，消费的时候从 COS 下载消息进行处理。
- 对消息进行重新拆分。

### TDMQ CMQ 版使用哪种协议访问？
TDMQ CMQ 版使用 HTTP、TCP 协议，TDMQ CMQ 版 SDK 会维护 TCP 长连接。

### TDMQ CMQ 版会进行消息去重吗？
目前 TDMQ CMQ 版不会对消息进行去重。重复消息出现的原因以及去重方案，您可以参考 [消息去重](https://intl.cloud.tencent.com/document/product/1111/43011)。

### TDMQ CMQ 版消费消息时，pull 的长轮询是如何实现的？
队列有 pollingWaitSeconds 属性，表示默认的队列长轮询时间。
消费消息时如果有消息，则直接返回消息；如果当前队列没有消息，则会等待 pollingWaitSeconds 时间，如果在该时间内有消息则返回消息；如果超过了该时间仍然没有消息，则会报没有消息的异常。

这里用户可以根据自己的需求来设置队列的这个属性，而且用户也可以在消费消息的时候指定 pollingWaitSeconds 时间，不用每次消费消息都使用这个默认值。

