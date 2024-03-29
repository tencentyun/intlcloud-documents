## 注意事项

该文档仅适用于 [DescribeStatisticData](https://intl.cloud.tencent.com/document/product/248/39481) 接口，下列所有指标必入参 `tke_cluster_instance_id` 维度，其余为非必选维度，可不入参。

## 命名空间

Namespace = QCE/TKE2

## 监控指标

| 指标英文名                             | 指标中文名                           | 指标单位 | 维度                                                         | 统计粒度                             |
| -------------------------------------- | ------------------------------------ | -------- | ------------------------------------------------------------ | ------------------------------------ |
| K8sWorkloadAbnormal                    | 工作负载异常                         | -        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadFsWriteTimes                | 块设备写入次数                       | 次       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadNetworkReceiveBytesBw       | 网络入带宽                           | MB       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadNetworkTransmitBytesBw      | 网络出带宽                           | MB       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadRateCpuCoreUsedCluster      | CPU利用率                            | %        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadCpuCoreUsed                 | CPU使用量                            | 核       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadMemNoCacheBytes             | 内存使用量（不包含cache）            | MB       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadNetworkReceivePackets       | 网络入包量                           | 个/秒    | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadNetworkTransmitPackets      | 网络出包量                           | 个/秒    | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadRateMemNoCacheCluster       | 内存利用率（不含cache）              | %        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadFsReadBytes                 | 块设备读取大小                       | MB       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadMemUsageBytes               | 内存使用量                           | MB       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadNetworkTransmitBytes        | 网络出流量                           | MB       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadPodRestartTotal             | Pod重启次数                          | 次       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadRateMemUsageBytesCluster    | 内存利用率                           | %        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadFsReadTimes             | 块设备读取次数                       | 次       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadNetworkReceiveBytes         | 网络入流量                           | MB       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadFsWriteBytes                | 块设备写入大小                       | B        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadGpuMemoryUsedBytes          | GPU内存使用量                        | MB       | tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadGpuUsed                     | GPU使用量                            | 卡       | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadRateGpuMemoryUsedCluster    | GPU内存利用率                        | %        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadRateGpuUsedCluster          | GPU利用率                            | %        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadRateCpuCoreUsedResource     | CPU利用率（占Pod规格）               | %        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadRateMemUsageBytesResource   | 内存利用率（占Pod规格）              | %        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |
| K8sWorkloadRateMemNoCacheBytesResource | 内存利用率（占Pod规格，不包含cache） | %        | 必填维度：tke_cluster_instance_id、<br/>非必选：namespace、workload_kind、workload_name | 60s、<br>300s、<br>3600s、<br>86400s |

## 统计粒度与时间跨度

不同统计粒度支持的时间跨度不一致，拉取监控数据时需注意时间跨度限制，具体说明如下：

| 统计粒度 | 支持最大时间跨度（结束时间-起始时间） |
| -------- | ------------------------------------- |
| 60s      | 12小时                                |
| 300s     | 3天                                   |
| 3600s    | 30天                                  |
| 86400s   | 186天                                 |

## 各维度对应参数总览

<table>
    <thead>
        <tr>
            <th><span>参数名称</span></th>
            <th><span>类型</span></th>
            <th><span>维度名称</span></th>
            <th><span>维度解释</span></th>
            <th><span>格式</span></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td rowspan="2"><span>必选</span></td>
            <td><span>tke_cluster_instance_id</span></td>
            <td><span>集群的维度名称</span></td>
            <td><span>输入 String 类型维度名称：tke_cluster_instance_id</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>tke_cluster_instance_id</span></td>
            <td><span>具体集群 ID</span></td>
            <td><span>输入具体集群 ID，例如：cls-fvkxp123</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
             <td rowspan="6"><span>非必选（可不选，也可选择一项或多项）</span></td>
            <td><span>namespace</span></td>
            <td><span>命名空间的维度名称</span></td>
            <td><span>输入 String 类型维度名称：namespace</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>namespace</span></td>
            <td><span>具体命名空间</span></td>
            <td><span>输入具体命名空间，例如：kube-system</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td><span>workload_kind</span></td>
            <td><span>工作负载类型的维度名称</span></td>
            <td><span>输入 String 类型维度名称：workload_kind</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>workload_kind</span></td>
            <td><span>具体工作负载类型</span></td>
            <td><span>输入具体工作负载名称，例如：Deployment</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td><span>workload_name</span></td>
            <td><span>工作负载名称的维度名称</span></td>
            <td><span>输入 String 类型维度名称：workload_name</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>workload_name</span></td>
            <td><span>具体工作负载名称</span></td>
            <td><span>输入具体工作负载名称，例如：coredns</span></td>
        </tr>
    </tbody>
</table>




## 入参说明

**集群（必填参数）入参取值如下：**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123

**根据命名空间入参取值如下：**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=namespace
&Conditions.N.Dimensions.1.Value=kube-system

**根据工作负载入参取值如下：**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_kind
&Conditions.N.Dimensions.1.Value=Deployment

**根据工作负载名称入参取值如下：**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
