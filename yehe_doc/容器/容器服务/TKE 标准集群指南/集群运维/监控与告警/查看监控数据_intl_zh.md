## 操作场景

腾讯云容器服务默认为所有集群提供基础监控功能，您可以通过以下方式查看容器服务的监控数据。
- [查看集群指标](#check1)
- [查看节点指标](#check2)
- [查看节点内 Pod 指标](#check3)
- [查看工作负载指标](#check4)
- [查看工作负载内 Pod 指标](#check5)
- [查看 Pod 内 Container 指标](#check6)

## 前提条件
已登录容器服务控制台，并进入 **[集群](https://console.cloud.tencent.com/tke2/cluster?rid=1)** 的管理页面。

## 操作步骤

[](id:check1)
### 查看集群指标
在需要查看监控数据的集群行中，单击 <img src="https://main.qcloudimg.com/raw/fef90a2f69f50758b30e4c4b5e0bc7de.png" style="margin-bottom: -2px;;"></img>，即可查看该集群监控信息页面。如下图所示：
![](https://main.qcloudimg.com/raw/444d1c462cf681ec7456229b25373c3a.png)

[](id:check2)
### 查看节点指标
您可以通过以下操作查看节点和 Master&Etcd 节点的监控信息。
1. 选择集群ID/名称，进入该集群的管理页面。
2. 展开**节点管理**，即可查看节点和 Master&Etcd 节点的监控信息。
 - 选择**节点** > **监控**，即可进入**节点监控**页面，查看监控信息。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EPbK891_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206162908.png)
 - 选择 **Master&Etcd** > **监控**，即可进入 **Master&Etcd 监控**页面，查看监控信息。如下图所示：
![](https://main.qcloudimg.com/raw/b178510aaf43b2907d64835d7384a5b1.png)

[](id:check3)
### 查看节点内 Pod 指标
1. 选择集群ID/名称，进入该集群的管理页面。
2. 选择**节点管理** > **节点**，进入节点列表页面。
3. 选择节点名称，在 “Pod 管理”页签中单击**监控**，即可查看到该节点内 Pod 的监控指标曲线图。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WeGI357_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206163502.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Rfbs680_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206163616.png)

[](id:check4)
### 查看工作负载指标
1. 选择集群ID/名称，进入该集群的管理页面。
2. 选择**工作负载** > **任意类型工作负载**。例如，选择**Deployment**，进入 Deployment 管理页面。
3. 单击**监控**，即可查看该工作负载的监控信息。如下图所示：
![](https://main.qcloudimg.com/raw/392b8235bb98367b50bc4b20e6ad3118.png)

[](id:check5)
### 查看工作负载内 Pod 指标
1. 选择需要查看的集群ID/名称，进入该集群的管理页面。
2. 选择**工作负载** > **任意类型工作负载**。例如，选择**Deployment**，进入 Deployment 管理页面。
3. 选择工作负载名称，在该工作负载的 “Pod 管理”页签中单击**监控**，即可查看该工作负载内所有 Pod 的监控指标对比图。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nhMM324_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206164052.png)


[](id:check6)
### 查看 Pod 内 Container 指标

1. 选择集群ID/名称，进入该集群的管理页面。
2. 选择**工作负载** > **任意类型工作负载**。例如，选择**Deployment**，进入 Deployment 管理页面。
3. 选择工作负载名称，在该工作负载的 “Pod 管理”页签中，单击实例名称前的![](https://qcloudimg.tencent-cloud.cn/raw/73074e1d0fd941c5dcdfa52ed415195a.png)，即可查看该 Pod 的 Container 信息。
4. 单击![](https://qcloudimg.tencent-cloud.cn/raw/1655cff483b7ec789d487e17dd54b12c.png)，即可查看该 Pod 内 Container 的监控指标对比图。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/whLQ650_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206164130.png)

 
