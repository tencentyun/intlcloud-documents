## 操作场景

您可以对云服务器实例对应的维修任务设置告警，在发生异常时将会第一时间通过邮件、短信、电话等渠道通知您采取措施。本文介绍如何通过事件总线控制台，通过 [事件总线](https://intl.cloud.tencent.com/document/product/1108/42267) 设置云服务器实例对应事件告警。

## 操作步骤
1. 登录 [事件总线控制台](https://console.cloud.tencent.com/eb)，参考 [开通事件总线](https://intl.cloud.tencent.com/document/product/1108/42272) 完成服务开通。
2. 选择左侧导航栏中的 **[事件规则](https://console.cloud.tencent.com/eb/rule)** ，在“事件规则”页面上方选择地域及事件集，并单击**新建事件规则**。
3. 进入“新建事件规则”页面：
    1.  在“基础信息”中输入**规则名称**。如下图所示：
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/zHwA899_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421102346.png)
    2. 在“事件模式”中，参考以下信息设置“事件匹配”参数，其余参数请按需设置。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/bQp2060_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421102608.png)
       - **云服务类型**：在下拉列表中选择**云服务器**。
       - **事件类型**：在下拉列表中按需进行勾选。
   3. 单击**下一步**。
   4. 在“事件目标”中，“触发方式”在下拉列表中按需进行勾选，您可按需进行配置。
      - “触发方式”选择**日志服务（CLS）**，则参考 [CLS 目标投递](https://intl.cloud.tencent.com/document/product/1108/46992) 进行配置。
      - “触发方式”选择**消息推送**，则参考 [消息推送目标投递](https://intl.cloud.tencent.com/document/product/1108/46779) 进行配置。
4. 单击**完成**即可完成设置。
