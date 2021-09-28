## 操作场景

如果当前的实例规格不能满足您的业务需求，可以通过控制台提升您的实例规格。

> ?
> - 通过控制台直接提升实例规格包括峰值带宽、磁盘容量、Topic 个数、Partition 个数，也可以仅提升磁盘容量。实例规格的升配操作为平滑升级，您的服务不会中断。
> - 1个 Topic 支持的 partition 数量限制为24个，如需继续提升 Partition 数量需要 [提交工单](https://console.cloud.tencent.com/workorder/category) 处理，Partition 最高可提升至500个。

## 前提条件

升配前请您进行如下检查：

1. 检查实例是否存在不可用的公网路由、支撑网、VPC 网络等。参考 [添加路由策略](https://intl.cloud.tencent.com/document/product/597/32555)。
2. 检查实例是否存在有未同步的副本。参考 [查看 Topic 详情](https://intl.cloud.tencent.com/document/product/597/32554)。
3. 检查实例是否存在未完成的任务（数据迁移），是否存在创建异常的 Topic、删除异常的 Topic 数据等。

如果存在上述未完成事项及任务，建议等待全部完成后再进行升配，如果其中任务存在执行异常情况，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 处理。

## 操作步骤

### 标准版

1. 登录 [CKafka 控制台](https://console.cloud.tencent.com/ckafka)。
2. 在实例列表页的操作栏，选择**更多** > **升配**进入升配页。
3. 在实例升配页 ，选择目标升配规格。
   ![](https://main.qcloudimg.com/raw/1856e04396a4228368329885bc766e9d.png)
4. 单击**提交**完成实例升配。

### 专业版

1. 登录 [CKafka 控制台](https://console.cloud.tencent.com/ckafka)。
2. 在 实例列表页的操作栏，选择**更多** > **升配**进入升配页。
3. 在实例升配页 ，选择目标升配规格。
   ![](https://main.qcloudimg.com/raw/80704895f876dddeee2fecb6496dcf94.png)
	- 产品规格：根据峰值带宽和磁盘容量选择对应的型号。
	- 实例价格：升配按天补足差价。
	- rebalance 时间：
		- 当识别到升配需要进行数据迁移时，可以选择立即执行或者自定义时间（推荐选择夜晚执行，减少对业务的影响），预计耗时由后台接口经过对变配升配的计算后得出。
			![](https://main.qcloudimg.com/raw/98f3c20193e67fdb65799739b2cc234c.png)
		- 当识别到升配不需要进行数据迁移时，则显示“本次升配不会产生Reblance”。
			![](https://main.qcloudimg.com/raw/e0d6ebe815789cb0827a021c1f40d548.png)
	- 升配模式：当识别到升配需要进行实例迁移时，可以根据实际业务需要选择升配模式；若不需要进行实例迁移，则无需选择升配模式。
		- 稳定模式：CKafka 将限制升配过程中数据迁移速度，最大程度保留实例的带宽属性，适合于不希望干扰业务的场景。
		- 高速模式：CKafka 将不对升配过程中数据迁移的速度进行限制，会影响实例的生产消费带款，适合于业务低峰或者允许停服的场景。
4. 单击**提交**完成实例升配，在状态列可实时查看实例的升配进度。
5. 若设置了定时升配，则在状态栏可修改定时时间。


## 升配失败的可能原因

1. 当前可用区的磁盘资源不满足此次升配的需求，建议联系腾讯云客户确认是否有足够的资源。

2. 实例升配过程中如果选择高速模式，并且集群当中存在占用带宽资源较高的生产任务时，会发生数据迁移延迟时长增大，可通过 [查看监控](https://intl.cloud.tencent.com/document/product/597/12167) 观察升配时间段生产和消费流量是否存在有过高峰值存在。

3. 升配过程中耗时过长，由于迁移的机器配置的接受最大的消息字节数是1MB，而需要迁移的 Broker 配置的是8MB。会导致 Broker 无法接收超大消息迁移，从而产生较长的迁移数据耗时，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 处理。

4. 新旧集群升配或迁移过程中，Broker IP 更新发生异常，导致新集群的 Broker IP 拉取数据失败。通过 [查看监控](https://intl.cloud.tencent.com/document/product/597/12167) 可观察到持续一段时间无监控数据，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 处理。
