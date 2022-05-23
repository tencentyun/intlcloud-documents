

TDMQ CMQ 版目前支持 Java、Python、PHP 及 C++ SDK，后续会支持更多语言。欢迎广大开发者根据 API 说明开发更多语言版本的 SDK。


为保证消息队列 CMQ 用户迁移至 TDMQ CMQ 版无需修改业务代码，以下接口协议与以前版本保持一致。

 | 接口功能                                                     | Action ID           | 功能描述                         |
 | :----------------------------------------------------------- | :------------------ | :------------------------------- |
 | [发送消息](https://intl.cloud.tencent.com/document/product/1111/46415) | SendMessage         | 用于发送一条消息到指定的队列。   |
 | [批量发送消息](https://intl.cloud.tencent.com/document/product/1111/46416) | BatchSendMessage    | 用于发送批量消息到指定的队列。   |
 | [消费消息](https://intl.cloud.tencent.com/document/product/1111/46417) | ReceiveMessage      | 用于消费队列中的一条消息。       |
 | [批量消费消息](https://intl.cloud.tencent.com/document/product/1111/46418) | BatchReceiveMessage | 用于消费队列中的多条消息。       |
 | [删除消息](https://intl.cloud.tencent.com/document/product/1111/46419) | DeleteMessage       | 用于删除已经被消费过的消息。     |
 | [批量删除消息](https://intl.cloud.tencent.com/document/product/1111/46420) | BatchDeleteMessage  | 用于批量删除已经被消费过的消息。 |
 | [发布消息](https://intl.cloud.tencent.com/document/product/1111/46421) | PublishMessage      | 用于发布一条消息到指定主题。     |
 | [批量发布消息](https://intl.cloud.tencent.com/document/product/1111/46422) | BatchPublishMessage | 用于发布批量消息到指定主题。     |

 除此之外的其他接口，需要按照 [HTTP 控制流 SDK](https://intl.cloud.tencent.com/document/product/1111/46413) 的引导进行开发。

