## 操作场景

腾讯云容器服务默认为所有集群提供基础监控功能，您可以通过以下方式查看容器服务的监控数据。
- [查看集群指标](#check1)
- [查看节点指标](#check2)
- [查看节点内 Pod 指标](#check3)
- [查看工作负载指标](#check4)
- [查看工作负载内 Pod 指标](#check5)
- [查看 Pod 内 Container 指标](#check6)

## 前提条件
已登录控制台，并进入【[集群](https://console.cloud.tencent.com/tke2/cluster?rid=1)】的管理页面。

## 操作步骤

<span id="check1"></span>
### 查看集群指标
在需要查看监控数据的集群行中，单击 <img src="https://main.qcloudimg.com/raw/fef90a2f69f50758b30e4c4b5e0bc7de.png" style="margin-bottom: -2px;;"></img>，即可查看该集群监控信息页面。如下图所示：
![](https://main.qcloudimg.com/raw/444d1c462cf681ec7456229b25373c3a.png)

<span id="check2"></span>
### 查看节点指标
您可以通过以下操作查看节点和 Master&Etcd 节点的监控信息。
1. 选择需要查看的集群ID/名称，进入该集群的管理页面。
2. 展开**节点管理**，即可查看节点和 Master&Etcd 节点的监控信息。
 - 选择**节点**>**监控**，即可进入**节点监控**页面，查看监控信息。如下图所示：
![](https://main.qcloudimg.com/raw/c1c1fca1e108f8479b50a895c2d2d0b5.png)
 - 选择**Master&Etcd**>**监控**，即可进入**Master&Etcd 监控**页面，查看监控信息。如下图所示：
![](https://main.qcloudimg.com/raw/b178510aaf43b2907d64835d7384a5b1.png)

<span id="check3"></span>
### 查看节点内 Pod 指标
您可通过以下两种方式查看节点内 Pod 指标。
1. 选择需要查看的集群ID/名称，进入该集群的管理页面。
2. 选择**节点管理**>**节点**，进入节点列表页面。
3. 根据实际需求，选择查看节点内 Pod 指标的方式。
 - 在节点列表中查看 Pod 指标。
    1. 单击**监控**，进入**节点监控**页面。
    2. 单击**Pod**，将**所属节点**选择为您想查看的节点，即可查看到该节点内 Pod 的监控指标对比图。如下图所示：
![](https://main.qcloudimg.com/raw/e58301ce2675d2de018a867c31fcfb69.png)
 - 在节点详情页面中查看 Pod 指标。
    1. 选择需要查看的节点ID/节点名，进入该节点的管理页面。
    2. 选择**Pod 管理**页签，单击**监控**，即可查看到该节点内 Pod 的监控指标对比图。如下图所示：
![](https://main.qcloudimg.com/raw/269631374cbe8ff955de4d691c53772c.png)

<span id="check4"></span>
### 查看工作负载指标
1. 选择需要查看的集群ID/名称，进入该集群的管理页面。
2. 选择**工作负载**>**任意类型工作负载**。例如，选择**Deployment**，进入 Deployment 管理页面。
3. 单击**监控**，即可查看该工作负载的监控信息。如下图所示：
![](https://main.qcloudimg.com/raw/392b8235bb98367b50bc4b20e6ad3118.png)

<span id="target"></span><span id="check5"></span>
### 查看工作负载内 Pod 指标
<span id="first"></span>
1. 选择需要查看的集群ID/名称，进入该集群的管理页面。
2. 选择**工作负载**>**任意类型工作负载**。例如，选择**Deployment**，进入 Deployment 管理页面。
3. 选择需要查看的工作负载名称，进入该工作负载的管理页面。<span id="third"></span>
4. 选择**Pod 管理**页签，单击**监控**，即可查看该工作负载内所有 Pod 的监控指标对比图。如下图所示：
![](https://main.qcloudimg.com/raw/bda91f0b0fb55cf87cf7258cc471ae1f.png)

<span id="check6"></span>
### 查看 Pod 内 Container 指标
1. 参照[查看工作负载内 Pod 指标](#target)的[步骤1](#first)-[步骤3](#third)，进入工作负载详情页。
2. 选择**Pod 管理**页签，单击**监控**，进入**Pod 监控**页面。
3. 单击**Container**，将**所属 Pod**选择为您想查看的 Pod，即可查看该 Pod 内 Container 的监控指标对比图。如下图所示：
![](https://main.qcloudimg.com/raw/28b567cd6eda684fbd0076d89bdadd76.png)


