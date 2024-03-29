## 功能介绍
EMR 控制台支持自动监测本地盘换盘事件，换盘后可在控制台自助初始化新磁盘操作。
>! 
>- 用户收到 CVM 坏盘通知并根据 CVM 的通知内容修复物理盘或更换磁盘后，EMR 控制台方可触发‘磁盘修复’操作。
>- 磁盘更换后，该磁盘上的数据会丢失，请确保磁盘上的数据有备份。

## 操作步骤
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在集群列表中单击对应的**集群 ID/名称**进入集群详情页。
2. 在集群详情页中选择**集群资源 > 资源管理**，对其更换完磁盘的节点进行**修复磁盘**操作。
3. 在操作过程中，会对当前节点进行服务重启等操作，重启过程中服务和节点不可用，建议在业务低峰期进行修复操作。

## Kudu 服务恢复
>! 
>- 当存在多块本地盘，且其中1块或多块盘维修后使用EMR磁盘修复功能，所在节点部署了 KuduServer 服务;
>- 受限于 kudu 的 fs_data_dirs 能力，由于某1块或者多块盘被格式化处理，为保证 kuduServer 正常启动只支持 kuduServer 节点上配置的所有数据盘数据目录都是空数据，需客户协助确认这些数据目录，除 kudu 存储数据外，未被其他客户自身业务误用。

- 场景：
具体可在 EMR 控制台集群服务，所更换磁盘节点的 KuduServer 中健康状态为“不可用”状态：
- 确认数据一致性及恢复：
	1. 确认所在目录（具体查看方式如下）数据除 kudu 外，无其他用途；假如有其他用途，请先把相关数据迁移到其他非 fs_data_dirs 配置目录下，再执行以下操作。
	具体目录：查看文件`/usr/local/service/kudu/conf/tserver.gflags`：
	![](https://qcloudimg.tencent-cloud.cn/raw/daf635f30f14fd6c213b562ecdc4c464.png)
	2. 登录本地盘异常节点查看日志：`/data/emr/kudu/log/kudu-tserver.INFO`：
	![](https://qcloudimg.tencent-cloud.cn/raw/059c22c9e94094405a601b6616e1d94a.png)
	使用 root 用户执行以下命令，清理相关不一致数据： 
```
rm -rf /data/emr/kudu/tserver/*
rm -rf /data1/emr/kudu/tserver/*
```
此命令假设 fs_data_dirs 中配置为 `/data/emr/kudu/tserver/`，` /data1/emr/kudu/tserver/`，具体可根据`/usr/local/service/kudu/conf/tserver.gflags`查看
	3. 观察 kuduServer 服务状态。

>? 若您在操作过程中遇到问题，请您及时 [提交工单](https://console.cloud.tencent.com/workorder/category) 反馈，我们将为您核实处理。
