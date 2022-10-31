## 简介
您可以在腾讯云控制台的**费用中心**，查看您的账户使用对象存储服务所产生的费用情况。


>!
>- 在 COS 账单结算时，系统将按照**免费额度 > 按量计费**的顺序进行结算。
> - 默认情况下系统采用按量计费方式进行结算。对于享受免费额度的账户，先抵扣免费额度，再按量计费。
>- 如需了解免费额度、计费项说明以及注意事项，请分别参见 [免费额度](https://intl.cloud.tencent.com/document/product/436/6240) 和 [计费概述](https://intl.cloud.tencent.com/document/product/436/16871) 文档。



## 查看资源 ID 账单/明细账单


您可在 [费用中心](https://console.cloud.tencent.com/expense/overview) 控制台查看费用账单，可在线查看的账单类型有资源 ID 账单和明细账单。

- 资源 ID 账单：根据资源 ID 维度汇总展示账单金额，和 L2-资源账单文件一致。更多详情请参见 [资源账单](https://www.tencentcloud.com/document/product/555/7430)。
- 明细账单：不做聚合，每笔费用均为一条明细记录，和 L3-明细账单文件一致。更多详情请参见 [明细账单](https://www.tencentcloud.com/document/product/555/7430)。





<span id="XBZD"></span>



#### 查询步骤
1. 登录 [腾讯云控制台](https://console.cloud.tencent.com)。
2. 在右上方导航栏**费用**中，单击**费用中心**，进入费用中心总览页面。
3. 在左侧菜单栏中，单击**费用账单 > 账单详情**，即可在线查看当前账号下的资源 ID 账单和明细账单。
>? 选择**账单概览**可查看账单费用趋势和账单汇总。
>
4. 单击“资源 ID 账单”选项卡页面，下拉列表中选择 **COS 对象存储**，可按照地域、计费模式和交易类型等维度查看您的 COS 消费情况。勾选不显示0元费用，账单中心将自动隐藏0元的消费明细账单。
![](https://qcloudimg.tencent-cloud.cn/raw/d57e860dc2e1c482c6ba421c84cffb05.png)
单击“明细账单”选项卡页面，下拉列表中选择 **COS 对象存储**，可展示您的每笔消费明细，费用不做聚合。
![](https://qcloudimg.tencent-cloud.cn/raw/0e158dd0cf06ac91b4bbe30dfee2ca58.png)
>? 
>- 如需按照**存储桶**维度查询每个计量项的用量明细、每个存储桶或地域的费用分摊情况，可单击左侧的 [用量明细下载](https://console.cloud.tencent.com/expense/bill/dosageDownload)，将 COS 用量明细报表下载至本地进行查询。
>- 目前对象存储 COS 支持存储桶分账功能，该功能通过白名单开放，若您的账号已加白，则在资源 ID 账单和明细账单中可看到以**存储桶名称**为资源 ID 展示费用情况。
>
相关选项说明如下：
 - **地域：**在地域的下拉列表中选中不同地域，可以分地域查询消费明细。
 - **计费模式：**在计费模式的下拉列表中选中不同计费模式，可以查询按量计费模式下的消费明细。
 - **交易类型：**在交易类型的下拉列表中选中不同交易类型，可以查询按量计费交易类型的消费记录。





<span id="download"></span>

## 下载账单

您可在 [账单下载中心](https://console.cloud.tencent.com/expense/overview) 下载您所需的费用账单，目前可下载的账单类型有L0-PDF账单、L1-多维度汇总账单、L2-资源账单、L3-明细账单。

>?
>- 关于账单介绍、账单字段说明请参见 [账单介绍](https://www.tencentcloud.com/document/product/555/7430)、[账单字段说明](https://intl.cloud.tencent.com/document/product/555/37506)。
>- 关于账单下载操作指引，请参见 [账单下载中心](https://intl.cloud.tencent.com/document/product/555/44357)。

