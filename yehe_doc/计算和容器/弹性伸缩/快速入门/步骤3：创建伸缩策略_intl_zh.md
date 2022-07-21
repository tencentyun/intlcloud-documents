## 操作场景

弹性伸缩组根据伸缩策略进行云服务器数量的增减：
- 创建**定时任务**，用于定时执行伸缩活动，您还可设置是否周期性执行。
- 创建**告警触发策略**，根据云监控指标（例如 CPU、内存使用率等）情况执行伸缩活动。


## 操作步骤

### 创建定时任务

如果您的负载变化情况是可以预知的，那么您可通过设置定时任务，对您的设备扩展活动进行规划。此功能可定时及周期性地自动增加或减少 CVM 实例，从而灵活应对业务负载变化，提高设备利用率，节省部署和实例成本。
1. 在 “[伸缩组](https://console.cloud.tencent.com/autoscaling/group?rid=1)” 页面，选择伸缩组 ID 进入该伸缩组详情页。
2. 选择**定时任务**页签，并单击**新建**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/8157fcd7ee03c86af5042b357ce5c4f8.png)
3. 在弹出的“新建定时任务”窗口中，指定定时任务名称、伸缩组活动和重复周期等信息。
4. 完成设置后单击**确定**，即可查看该定时任务。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/27bb342e8aef8100fa9e3e23377af78a.png)


### 创建告警触发策略

如果您希望根据 CVM 指标情况调整业务部署，那么您可通过自定义告警触发策略，对您的设备扩展活动进行规划。当业务负载使得指标到达阈值时，该策略将帮助您自动增加或减少 CVM 实例数量，从而灵活应对业务负载变化，提高设备利用率，节省部署和实例成本。


<dx-alert infotype="explain" title="">
 - 伸缩组建立时均会默认建立一条 ping 不可达告警触发策略，以替换不健康子机。
 - 在使用告警触发策略之前，需要在 CVM 的镜像里安装新版本的云监控 Agent。详情请参见 [安装监控组件](https://intl.cloud.tencent.com/document/product/248/6211)。
</dx-alert>


1. 在 “[伸缩组](https://console.cloud.tencent.com/autoscaling/group?rid=1)” 页面，选择伸缩组 ID 进入该伸缩组详情页。
2. 选择**告警触发策略**页签，并单击**新建**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/c11b3994d5f1eafb0ca80a167ed3e41f.png)
3. 在弹出的“新建告警触发策略”窗口中，设置基于云监控性能指标（例如 CPU、内存、带宽等），自动为伸缩组增加或减少指定台数或指定百分比的 CVM 实例。
您还可通过“复制策略（选填）”，直接复制已有伸缩组的已有策略到当前伸缩组。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/a1d45712cfae19d74cd7236c3814961d.png)
4. 完成设置后单击**确定**，即可查看该告警触发策略。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ddadd2956437ddb3abecffb9759411a3.png)
