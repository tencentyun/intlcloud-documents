腾讯云可观测平台为负载均衡和后端实例提供数据收集和数据展示功能。使用腾讯云可观测平台，您可以查看负载均衡的统计数据，验证系统是否正常运行并创建相应告警。有关腾讯云可观测平台的更多信息，请参见 [腾讯云可观测平台](https://intl.cloud.tencent.com/doc/product/248) 产品文档。

腾讯云默认为所有用户提供腾讯云可观测平台功能，您无需手动开通，只要您使用了负载均衡，腾讯云可观测平台即可帮助您收集相关监控数据。您可以通过以下几种方式查看负载均衡的监控数据：

## 负载均衡控制台
1. 登录 [负载均衡控制台](https://console.cloud.tencent.com/clb)，单击负载均衡实例 ID 旁的监控图标，即可通过监控浮窗，快速浏览各个实例的性能数据。
![](https://main.qcloudimg.com/raw/6580c81d6fd1eee2234fcb5262a976bb.png)
2. 单击负载均衡实例 ID，进入负载均衡详情页，单击【监控】选项卡，即可查看当前负载均衡实例的监控数据。
![](https://main.qcloudimg.com/raw/3eb231b336c9325ae16bfe2937e41b39.png)

## 腾讯云可观测平台控制台
登录 [腾讯云可观测平台控制台](https://console.cloud.tencent.com/monitor/overview)，单击左侧导航栏中“云产品监控”模块下的[【负载均衡-CLB】](https://console.cloud.tencent.com/monitor/clb)，单击负载均衡实例 ID 进入监控详情页，即可查看该负载均衡实例的监控数据，展开实例即可查看监听器、后端服务器等监控信息。

## API 方式
您可以使用 GetMonitorData 接口获取所有产品的监控数据，具体内容请参见 [拉取指标监控数据](https://intl.cloud.tencent.com/document/product/248/33881)，负载均衡的命名空间请参见 [公网负载均衡监控指标](https://intl.cloud.tencent.com/document/product/248/10997)、[内网负载均衡监控指标](https://intl.cloud.tencent.com/document/product/248/39529) 。
