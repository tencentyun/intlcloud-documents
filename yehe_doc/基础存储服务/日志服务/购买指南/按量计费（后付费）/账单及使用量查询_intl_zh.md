日志服务（Cloud Log Service，CLS）支持用户自助查询服务账单及使用量，本文介绍详细的操作方式。

## 查询账单

### 查看日志主题费用

1. 登录**费用中心**，进入 [账单详情](https://console.cloud.tencent.com/expense/bill/summary?type=resource) 页面。
2. 在**全部产品**下拉框中，选择“日志服务CLS”，即可查看日志服务相关账单。

 - 账单数据默认按照费用从高向低排列，可以直观看到哪些日志主题花费最多。
 - 通过顶部账单时间范围选择器，可以切换账单的统计时间。
3. 选择需要查看的日志主题，单击**账单详情**。

4. 进入当前日志主题账单的详细分析。

您可以在此页面查看如下信息：
 - 该日志主题账单的各计费项花费与占比。在做成本优化时，可以根据流量费用与存储费用的占比情况选择不同的策略。如流量费用占据绝大比例，则考虑减少采集端日志的打印量或通过数据加工过滤掉无用日志。如存储费用占据绝大比例，则除上述两种方法外，还可以考虑缩短日志存储的时长。
 - 该日志主题账单的月度花费趋势。可用于同环比分析，定位是否有异常的费用突增。

### 通过分账标签区分不同业务

在各业务部门共用日志服务时，需要将日志服务的费用划分给不同的业务部门。此时可以通过 [分账标签](https://intl.cloud.tencent.com/document/product/555/32276) 功能，实现日志主题费用与业务部门的关联。操作如下：

1. 创建一个业务标签，详情请参见 [创建标签](https://intl.cloud.tencent.com/document/product/651/41684)。

 - 标签键：如“业务”。
 - 标签值：如“业务A”和“业务B”。
2. 绑定日志主题。
<dx-tabs>
::: 通过日志服务控制台绑定
1. 登录日志服务控制台，进入 [日志主题](https://console.cloud.tencent.com/cls/topic) 页面。
2. 勾选已有的日志主题或新建的日志主题，单击**编辑标签**。

3. 在弹出的窗口中，选择刚创建的“业务”标签，单击**确定**。
:::
::: 通过标签控制台绑定
1. 登录标签控制台，进入 [标签列表](https://console.cloud.tencent.com/tag/taglist) 页面。
2. 选择对应的业务标签，单击**绑定资源**。

3. 在弹出的窗口中，将“云服务”选择为“日志服务”，将“资源类型”选择为“日志主题”，并勾选对应的日志主题，单击**确定**。

:::
</dx-tabs>
3. 登录费用中心，进入 [分账标签](https://console.cloud.tencent.com/expense/tag) 页面。
4. 选择刚创建的“业务”标签，单击**设置为分账标签**。

5. 通过“业务”分账标签，查看不同业务的账单统计。
<dx-tabs>
::: 查看各业务的日志主题费用
1.  登录费用中心，进入 [账单详情](https://console.cloud.tencent.com/expense/bill/summary?type=resource) 页面。
2.  在**全部产品**下拉框中选择“日志服务CLS”，在**全部标签**下拉框中选择刚设置的“业务”标签键值即可查看。

:::
::: 查看各业务的总费用概览
1. 登录费用中心，进入 [账单概览](https://console.cloud.tencent.com/expense/bill/overview) 页面。
2. 选择**按标签汇总**页签即可查看。

:::
</dx-tabs>


### 设置日志服务费用预警

>!
>- 费用分析数据延迟2天更新，该数据可供成本分析、规划时参考，不作为结算和对账依据。
>- 费用分析目前正在灰度体验中，如需体验，可以联系腾讯云助手。
>

1. 登录费用中心，进入 [费用分析](https://console.cloud.tencent.com/expense/cost/analysis) 页面。
2. 单击**设置提醒**。

3. 单击**新建提醒**。

4. 在弹出的窗口中，将范围条件设置栏的**产品**选择为“日志服务”，其余配置根据实际需求进行设置。

支持的提醒类型有日数据提醒、月数据提醒。
 - 日数据提醒支持三种方式：环比（与上一天比较）、同比（与上个月同一天）、固定值（每日费用与此固定数值比较）
    日数据提醒公式说明：
    - 同比公式 = ABS（（本月日-上月日）/ 上月日 * 100%）
    - 环比公式 = ABS（（本期数-上期数） / 上期数 * 100%）
    - 固定值公式 = ABS（本期数）与固定值比较
 - 月数据提醒支持三种方式：环比（与上一月比较）、固定值（每月费用与此固定数值比较）
    月数据提醒公式说明：
    - 环比= ABS（（本期数-上期数） /上期数 * 100%）
    如今天是8月18日，则本期数指的是8月1日-16日的费用总和，上期数指的是7月1日-16日的费用总和。
    - 固定值公式 = ABS（本期数）与固定值比较
 - 支持配置产品、计费模式维度的告警推送。
    产品：显示当前用户所有已购产品，计费模式逻辑相同。
5. 单击**保存**，完成新建。


## 查询使用量

### 查看单个日志主题使用量

1. 登录日志服务控制台，进入 [日志主题](https://console.cloud.tencent.com/cls/topic) 页面。
2. 在日志主题列表中，单击 ![img](https://qcloudimg.tencent-cloud.cn/raw/9876ff99b4cb8853fe291ceec5b5b7ea.png)，即可查看该日志主题的使用量。



### 查看多个日志主题使用量

1. 登录云监控控制台，进入 [日志服务监控](https://console.cloud.tencent.com/monitor/product/cls_uin_topic) 页面。
2. 选择顶部的地域，查看该地域下的日志主题用量。（列表中流量数据均为当天累计流量）

3. 在日志主题列表中，单击 ![img](https://qcloudimg.tencent-cloud.cn/raw/9876ff99b4cb8853fe291ceec5b5b7ea.png)，即可查看该日志主题的使用量。


### 自定义分析日志主题使用量

1. 登录云监控控制台，进入 [Dashboard 列表](https://console.cloud.tencent.com/monitor/dashboard2/dashboards) 页面。
2. 单击**新建 Dashboard**，新建一个用于分析日志主题使用量的 Dashboard。

3. 完成配置后，单击右上角**保存**，保存该 Dashboard。
更多 Dashboard 功能使用说明详见云监控的 [Dashboard](https://intl.cloud.tencent.com/document/product/248/38461) 文档。
