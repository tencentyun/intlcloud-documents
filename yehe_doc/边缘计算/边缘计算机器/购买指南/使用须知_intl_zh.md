您在购买并使用腾讯云边缘计算器 ECM 前，请阅读本章节的使用须知。

##  边缘节点网络

- 单一边缘节点到同一运营商的同省或邻省监测节点的平均 Ping 丢包率 ⩽ 1%。
- 运营商的网络存在异常中断或抖动可能性，边缘计算器会7 \* 24实时监控并上报至云监控平台，用户通过云监控配置可以同步报警信息，实时获知节点网络状态。

##  边缘节点资源

- 边缘节点存储使用本地盘，不同节点存在差异。
- 本地盘来自单台宿主机，数据可靠性取决于宿主机的可靠性，存在单点故障风险和数据丢失风险。如果您对数据可靠性要求高，建议在应用层做数据冗余保证数据的可靠性。

##  边缘节点 SLA

- 腾讯云边缘计算机器的服务可用性（SLA）不低于99.9%。 
由以下原因导致的服务不可用，相应服务不可用时间不属于服务不可用的计算范畴和腾讯云的赔偿范畴：
任何腾讯云所属设备以外的网络和设备异常、腾讯云预先通知用户后进行的系统维护升级、客户原因引起的异常、不可抗力因素引起的不可用等。 
- 本地盘实例可靠性取决于宿主机的可靠性，当发生单点故障或单个边缘节点无法连通时，边缘计算机器会帮助实例尽快恢复连通，但不保证数据可靠性。

##  计费提示 

腾讯云边缘计算机器包括计算存储和网络带宽两部分计费。
- 计算存储服务取每日用量峰值，日结计费。
>! 每日用量峰值指当天0点 - 24点，CPU、内存、存储等各资源使用量的最大值，即您在当天24点前增加的资源，均会统计在当天使用的资源最高峰值内，从而增加当天的总体费用。
> 例如，当天 23:59:58 创建资源或创建资源后立即销毁等操作，均会导致当天费用的增加。
> **请您留意创建资源的时间点，避免因过晚创建资源和误操作造成您的损失。**
> 
- 网络带宽服务取每个边缘节点运营商统计的月95带宽峰值，按月结算。

更多详情请参见 [计费概述](https://intl.cloud.tencent.com/document/product/1119/43404)。

