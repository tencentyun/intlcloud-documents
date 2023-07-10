
## 简介
日志服务可以通过 Ckafka 实例来消费日志主题的数据，下面将为您详细介绍如何开启日志主题 Ckafka 消费功能。

## 前提条件

已开通腾讯云消息队列 （CKafka），并在日志主题同地域下创建 Ckafka 消费实例和消息队列 topic。

>Ckafka 实例的创建操作，请参阅 [创建实例和 Topic](https://intl.cloud.tencent.com/document/product/597/32543) 。

## 操作步骤

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls) 。
2. 在左侧导航栏中，单击【日志集管理】。
3. 单击需要配置 Ckafka 消费的日志集 ID/名称，进入日志集详情页。
4. 找到需要消费的日志主题，在其右侧单击【管理】，进入日志主题管理页面。
![](https://main.qcloudimg.com/raw/04759d7e7f2d6db0b0249c4393b5edd5.png)
5. 单击【Ckafka消费】页签，进入 Ckafka 消费配置页。
6. 单击右侧的【编辑】，开启 Ckafka 消费开关，选择消费的 Ckafka 实例以及对应的消息列队 topic。
![](https://main.qcloudimg.com/raw/43a9878b5bf8f0500c1ba19b668b7766.png)
7. 单击【保存】，启动 Ckafka 消费，Ckafka 消费状态显示为“已开启”则表示开启成功。
![](https://main.qcloudimg.com/raw/f964f0a141123a7926b8fd1a1eb1b5ba.png)




