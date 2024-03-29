本篇文档将为您指导，如何创建 Ckafka 触发器并完成函数的调用。

### 步骤1：创建函数
1. 登录 [Serverless 控制台](https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default)。
2. 在新建函数页面，选择使用**模板创建**来新建函数，在搜索框里筛选`Ckafka`，选择“	
Ckafka 消息转储至 COS”。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/d89b622a7b1ceecb4ed32811404f3940.png)
2. 单击**下一步**。



### 步骤2：配置触发器
在函数配置页面，填写函数基础配置。
1. 在“触发器配置”中，选择使用**自定义创建**来新建触发器。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ebce10b5fa8aa354cff54970c65b3c5d.png)
选择 **Ckafka 触发器**后，按照指引，配置消息来源的 Ckafka 实例的名称、主题等信息。您也可以选择 [新建Ckafka](https://console.cloud.tencent.com/ckafka/index?rid=1)。
>! 请保证您的函数与 Ckafka 在相同 VPC 下。
>
2. 单击**完成**。

### 步骤3：管理触发器
函数创建完成后，前往函数详情页，您可以在“触发管理”中查看已创建的触发器信息。您还可以开启或关闭触发器。
