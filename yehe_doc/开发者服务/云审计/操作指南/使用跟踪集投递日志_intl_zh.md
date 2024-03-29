## 操作场景
本文介绍了如何通过云审计控制台创建跟踪集，并投递日志。

## 操作步骤

1. 登录云审计控制台，选择左侧导航栏中的**[跟踪集](https://console.cloud.tencent.com/cloudaudit/audit)**。
2. 在“跟踪集”页面中，单击**创建**。如下图所示：
![](https://main.qcloudimg.com/raw/af55c793d8045210b777fde74bb3b486.png)
3. 在“创建跟踪集”页面中，根据以下主要信息进行填写。如下图所示：
![](https://main.qcloudimg.com/raw/1355e3ac456af9f5d63218ee454fa605.png)
 - **基础信息**：自定义填写跟踪集名称。
 - **管理事件**：可根据“事件类型”、“资源类型”进行筛选，还可进一步选择“全部事件”或“部分事件”来进行筛选投递。
 - **投递位置**：
    - 将事件投递到日志服务CLS：可以直接创建新的日志主题并投递，也可选择投递到已有的日志主题。使用日志服务更多信息请参见 [日志服务](https://intl.cloud.tencent.com/document/product/614/31592)。
    - 将事件投递到存储桶COS：可以直接创建存储桶并投递，也可投递到已有存储桶中。使用存储桶更多信息请参见 [存储桶概览](https://intl.cloud.tencent.com/document/product/436/38493)。
4. 单击**完成新建**即可创建跟踪集。约10分钟后， 开始正常投递日志。


