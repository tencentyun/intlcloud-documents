### 删除消息失败时如何处理？ 
删除消息失败可能是因为消息句柄超时了。队列属性 visibilityTimeout 表明了消息的可见时间，如果从消费消息到删除消息超过了这个时间，那么消息句柄就会失效，从而导致无法删除消息。 

### 调用TDMQ CMQ 版时出现 10250 qps throttling 异常如何解决？ 
出现该异常是由于 QPS 达到了上限值。QPS 默认值为5000，表示每秒发送（发布）消息的上限为5000 条，消费的消息条数默认为生产的1.1倍。如果对 QPS 有要求，您可以 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 申请提高 QPS 上限。

### 如果没有需要的 SDK 应该如何操作？
如果没有对应的语言，可以按照官网文档中的规范自己组包调用 TDMQ CMQ 版服务。

### 如何使 API 密钥只对 TDMQ CMQ 版的接口有用？
API 密钥是全局的密钥，目前 TDMQ CMQ 版已经接入 CAM，您将可以使用 CAM 进行权限控制。

