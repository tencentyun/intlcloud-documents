## 成本分析概念

成本分析是成本管理体系的基础功能，协助您灵活高效的分析账单数据，清晰透明的了解您的上云成本。

您可以登录腾讯云[费用中心](https://console.cloud.tencent.com/expense/overview)在左侧菜单栏单击**成本管理 > 成本分析**进入成本分析页面。

## 成本分析功能介绍

### 分类维度

分类维度主要用于对指定范围内的成本进行分类聚合，体现成本在该维度下的分布情况。

目前成本分析支持一维分类（即视图中体现为分类维度和日期的二维图表）。

目前支持维度：产品、计费模式、子产品、项目、地域、可用区、交易类型、标签键。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/2BpC587_%E5%88%86%E7%B1%BB%E7%BB%B4%E5%BA%A6.png)

>? 可视化图形中，若某维度下分类项超过10个，则剩余部分汇总为“其他”。在下方表格中则会全量显示，支持翻页查询与下载。

### 费用类型与账单口径

费用类型与账单口径的不同组合对应不同的分析视角。

费用类型：包括原价，总费用（折后价），现金支付，优惠券支付，赠送金支付，分成金支付。

账单口径：包括费用账单和消耗账单（消耗账单需先开通，详情参见[消耗账单介绍](https://www.tencentcloud.com/document/product/555/44227)）。

默认组合是总费用+费用账单，适用于常规的成本分析场景。有摊销视角诉求时可切换为消耗账单，希望只分析现金流的支出情况时可切换为现金支付，以及其他特殊诉求。

### 时间窗
- 时间窗支持固定时间窗与可变时间窗两种模式，在颗粒度上支持日级和月级；

- **固定时间窗：**可在日历中直接点击开始与结束日期
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZeGW196_%E5%9B%BA%E5%AE%9A%E6%97%B6%E9%97%B4%E7%AA%97.png)

- **可变时间窗：**在日历上方点击浮动时间范围，该功能主要用于成本报告，以实现报告的自动更新。日级支持近7、30、60天；月级支持近1、3、6个月。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QHUV227_%E5%8F%AF%E5%8F%98%E6%97%B6%E9%97%B4%E7%AA%97_16777521165341.png)

>? 日时间粒度，日级最多支持历史180天，月级最多支持历史12个月。

### 图表类型

成本分析图表支持堆积图、折线图、条形图三种类型可视化方式。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4Cr7184_%E5%9B%BE%E8%A1%A8%E7%B1%BB%E5%9E%8B_1.png)

![](https://staticintl.cloudcachetci.com/yehe/backend-news/35Yg144_%E5%9B%BE%E8%A1%A8%E7%B1%BB%E5%9E%8B_2.png)

![](https://staticintl.cloudcachetci.com/yehe/backend-news/aeuG219_%E5%9B%BE%E8%A1%A8%E7%B1%BB%E5%9E%8B-3.png)

### 高级筛选

高级筛选用作进一步圈定目标成本范围，锁定关键成本。

支持多个维度复合多选，支持排除选择。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5Yc6459_%E9%AB%98%E7%BA%A7%E7%AD%9B%E9%80%89.png)

### 表格数据

成本明细数据支持翻页查询与下载，在成本明细页面，单击**下载**即可。

可视化图形中，若某维度下分类项超过10个，则剩余部分汇总为“其他”。在下载表格中则会全量显示。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CQmn409_%E8%A1%A8%E6%A0%BC%E6%95%B0%E6%8D%AE.png)

## 成本报告概述

成本报告功能，可以将成本分析的结果保存为报告，方便后续查阅与分享。报告可在成本分析界面中保存，也支持二次编辑或删除。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/r3Ay409_%E6%88%90%E6%9C%AC%E6%8A%A5%E5%91%8A_1.png)

![](https://staticintl.cloudcachetci.com/yehe/backend-news/cLbJ456_%E6%88%90%E6%9C%AC%E6%8A%A5%E5%91%8A_2.png)

- 报告将保存分析路径中设置的所有参数，若时间参数为可变时间窗，则成本报告将自动更新。

- 腾讯云为客户预设三个默认报告，可在[成本报告](https://console.cloud.tencent.com/expense/cost/report)页面查看，不支持修改删除。分别为：日度产品级成本趋势、日度总成本趋势、月度产品级成本趋势。
