本文档指导您查看 GPM 的指标监控和配置告警。

## 前提条件

- 已完成 [匹配创建](https://intl.cloud.tencent.com/document/product/1072/39203)。
- 您当前的账号需具备**云监控（Cloud Monitor，CM）**的全读写访问权限。云监控的权限配置说明，详情请参见 [管理子账号访问权限](https://intl.cloud.tencent.com/document/product/248/36744)。

## 查看指标监控

### 步骤1：登录云监控控制台

GPM 的指标数据将被上报到您的**云监控（Cloud Monitor，CM）**服务，您需要登录 [云监控控制台](https://console.cloud.tencent.com/monitor/overview) 查看指标数据。

### 步骤2：创建 GPM Dashboard

单击云监控左侧菜单栏**Dashboard**>**Dashboard 列表**进入 Dashboard 列表页，单击**新建 Dashboard**。
![](https://main.qcloudimg.com/raw/4d4547948acfe1c8120227a147740d1b.png)

### 步骤3：创建 GPM 图表

单击**新建图表**，选择需要监控的指标，完成图表信息配置。
![](https://main.qcloudimg.com/raw/56c530e9f929842eee6aae4111c187e4.png)
如图所示：
1. 在1处的**指标**下拉框选择“游戏玩家匹配监控”后，选取一个监控指标（图中以“匹配成功率(%)”为例）。
2. 在2处的**筛选**下拉框选择“实例”后，选择需要监控的 MatchCode。
>!选择需要监控的 MatchCode 对象前，需要确保您选择的“地域”与创建 MatchCode 的“地域”保持一致。您只可选中当前账户有访问权限的 MatchCode。
>![](https://main.qcloudimg.com/raw/f874212cc51539e40b78506277108400.png)
>
3. 在3处的**图表名**自定义您的图表名称。
4. 单击右上角**保存**，在弹出“新的 Dashboard”配置窗口中填写“Dashboard 名称”和“所属文件夹”。
![](https://main.qcloudimg.com/raw/89a9feb2bde8e34e357e87ccb9bf11b0.png)
5. 单击**确定**即可完成指标监控图表创建。

### 步骤4：通过已创建好的图表查看监控数据

通过**[Dashboard列表](https://console.cloud.tencent.com/monitor/dashboard2/dashboards)**菜单，进入您创建完成的**Dashboard**所在的目录。
- 您可通过单击“Dashboard 名称”右侧的**设置**更改 Dashboard 名称。
  ![](https://main.qcloudimg.com/raw/1f8a06e485817aad0e27e49a70511ed4.png)您可通过单击“Dashboard 名称”，即可看到当前 Dashboard 下已配置的所有图表。当您跟进的 MatchCode 有请求记录后，图表即可呈现相应数据。
  ![](https://main.qcloudimg.com/raw/0cdc66c6f5e22468d91ed6477226e0f8.png)




## 配置指标告警

### 步骤1：进入告警策略页面
1. 登录 [云监控控制台](https://console.cloud.tencent.com/monitor/overview) ，单击**告警配置**>**告警策略**进入策略列表页。
2. 单击**新建**进入“新建告警策略”页面。
![](https://main.qcloudimg.com/raw/f0277fefee102dbef36a1fcce62ab802.png)

### 步骤2：新建告警策略

![](https://main.qcloudimg.com/raw/6b13f5f5aa7fb36f04128c9beba52d04.png)
如图所示：
1. 在1处输入告警“策略名称”。
2. 在2处下拉框选择“游戏玩家匹配监控”。
3. 在3处下拉框选择需要告警的 MatchCode。
4. 在4处下拉框选择需要告警的指标。此处可以配置单一指标，也可以组合指标配置告警条件和策略。
5. 在5处选择已有的模版或新建模版，配置告警接收人/接收方式。
6. 单击**完成**，告警策略即可生效。到达您配置的告警条件后，将自动触发告警通知。

