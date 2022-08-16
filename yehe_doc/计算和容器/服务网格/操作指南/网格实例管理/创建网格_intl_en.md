## Overview
Create a service mesh instance before using the service mesh. Mesh instances have regional attributes, but can manage services in multiple regions.

>? Each account is allowed to create 20 meshes by default. If more meshes are required, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

## Directions

The procedure of creating a service mesh instance on the console is as follows:

1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh).
2. Select a region, and click **Create** in the upper left corner of the page.
3. On the **Create service mesh** page, fill in configurations related to mesh creation as required. For the description of the configuration items, see [Configuration Item Description for Mesh Creation](#createMeshPara). Then, click **Next: Confirm information**.
![](https://qcloudimg.tencent-cloud.cn/raw/8b211742df1ad42394ca72c195d41c99.png)
4. On the **Confirm information** page, confirm that the creation configurations are correct and click **Submit** to start the mesh creation process.
![](https://qcloudimg.tencent-cloud.cn/raw/68e2cfc60b20b6616ac2b585b6c9a2a1.png)
5. After the mesh creation process is complete, view the service mesh instance in the list.
![](https://qcloudimg.tencent-cloud.cn/raw/5969bc20db03ce0de661aa8e0b8bdbb2.png)

## Configuration Item Description for Mesh Creation [](id:createMeshPara)

<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td>Mesh name</td>
<td>Name of the service mesh to be created.</td>
<td>Yes</td>
</tr>
<tr>
<td>Region</td>
<td>Region where the service mesh control plane runs. The region where the control plane runs can be different from the region where the service workload (such as a cluster) is located. It is recommended to select a region close to the region where the service workload (cluster) is located.</td>
<td>Yes</td>
</tr>
<tr>
<td>Mesh component version</td>
<td>Control plane and data plane version. Tencent Cloud Mesh is compatible with the latest two major versions of the Istio community.</td>
<td>Yes</td>
</tr>
<tr>
<td>Mesh mode</td>
<td>Deployment mode of components related to the service mesh control plane. For a managed mesh, the control plane components are managed and maintained by Tencent Cloud. For a stand-alone mesh, the control plane components are deployed in a cluster you specified, and you need to manage and maintain the control plane components in the cluster. The **Managed mesh** option is available by default. A stand-alone mesh can be used after being added to an allowlist. To apply for a stand-alone mesh, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
<td>Yes</td>
</tr>
<tr>
<td>Egress traffic mode</td>
<td>Policy for the external access to services in the mesh. Two options are available: **Registry Only** (access to only services automatically discovered by the mesh and manually registered services is allowed) and **Allow Any** (access to any address is allowed).</td>
<td>Yes</td>
</tr>
<tr>
<td>Service discovery</td>
<td>Cluster for implementing automatic service discovery. The cluster must meet constraints such as version, permission, and IP range conflict.</td>
<td>No</td>
</tr>
<tr>
<td>Sidecar auto-injection</td>
<td>Namespace into which sidecars are automatically injected. After this field is enabled, sidecars will be automatically injected into all service workloads in the selected namespace. Auto-injection will take effect only for newly created service workloads. Sidecars will be injected into existing service workloads only after the workloads are restarted. If you need to further customize sidecar injection exceptions, see <a href="https://intl.cloud.tencent.com/document/product/1152/47464">Custom Sidecar Injection</a>.</td>
<td>No</td>
</tr>
<tr>
<td>External request bypasses sidecar</td>
<td>Corresponding to <a href="https://istio.io/latest/zh/docs/tasks/traffic-management/egress/egress-control/#direct-access-to-external-services">excludeIPRanges</a>. By default, sidecars takes over all the traffic in the current pod. If you want the access from a specific IP address not to pass through the sidecar proxy, you can configure this field. After configuration, Istio features such as traffic management and observability will not be performed on the request traffic from the IP range. After the configurations are modified, they take effect only for newly added pods, and for existing pods only after the pods are restarted. </td>
<td>No</td>
</tr>
<tr>  
<td>Sidecar readiness guarantee</td>
<td>Use the <a href="https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/#ProxyConfig">HoldApplicationUntilProxyStarts</a> feature to configure a service container to wait for sidecars to complete the startup before starting. This configuration ensures that a pod in the service container that depends on the sidecars can run normally.</td>
<td>No</td>
</tr> 
<td>Sidecar stop protection</td>
<td>After this field is enabled, a sidecar needs to wait for the process in the service container to be completely terminated before stopping, which increases the pod stop time. It is recommended to enable this field for the service whose service process cannot be shut down at any time. For Istio versions earlier than 1.12, Tencent Cloud Mesh uses the preset container prestop script to check that there is no more service process before allowing the service container to exit. If a user configures other prestop scripts, this feature will be interfered with. For versions later than 1.12, this feature is implemented by the new feature <a href="https://istio.io/latest/news/releases/1.12.x/announcing-1.12/change-notes/">EXIT_ON_ZERO_ACTIVE_CONNECTIONS</a>.</td>
<td>No</td>
</tr>
<tr>  
<td>Custom sidecar resources</td>
<td>By default, Tencent Cloud Mesh configures a resource limit of up to 2 cores and 1 GB for a sidecar container, which are sufficient in most cases. When the scale of your mesh increases or the logic in the sidecar increases, the default resource limit may be insufficient. You can modify the resource limit based on your service requirements.</td>
<td>No</td>
</tr>  
<tr>
<td>Ingress gateway</td>
<td>Ingress gateway to be created for the mesh. If the selected cluster is a TKE/EKS cluster, an ingress gateway of the CLB type is created by default. In this case, CLB-related items need to be configured. If the cluster is a manually registered cluster, only a gateway service of the LoadBalancer type is created because it is not determined whether the cluster supports CLB.</td>
<td>No</td>
</tr>
<tr>
<td>Egress gateway</td>
<td>If you need to manage the outgoing traffic of the mesh in a centralized manner, such as unified egress, unified authentication, and rule configurations, you need to create an egress gateway. After this field is enabled, an egress gateway service of the ClusterIP type will be automatically created for you.</td>
<td>No</td>
</tr>
<tr>
<td>Gateway deployment mode</td>
<td>Two options are available: **Normal mode** and **Exclusive mode**. For details, see <a href="https://intl.cloud.tencent.com/document/product/1152/47471">Gateway Deployment Modes</a>.</td>
<td>No</td>
</tr>
<tr>
<td>Gateway auto-scale policy</td>
<td>HPA policy for the gateway that is deployed in the specified cluster.</td>
<td>No</td>
</tr>
<tr>
<td>Network resource definition</td>
<td>Pod resource limit customized for the ingress/egress gateway.</td>
<td>No</td>
</tr>
<tr>
<td>Consumer end</td>
<td>Monitoring metric backend service of the mesh. Currently, interworking with TMP is supported. After configuration, monitoring metrics will be reported to TMP. The Tencent Cloud Mesh console displays metrics based on the TMP data source. You can also view the metrics independently on the TMP console. If a consumer end is not configured for the monitoring metrics, the mesh cannot use monitoring features such as displaying monitoring metrics and topologies.</td>
<td>No</td>
</tr>
<tr>
<td>Consumer end</td>
<td>Call tracing backend service of the mesh. Currently, interworking with APM is supported. After configuration, tracing data will be reported to APM from sidecars. The Tencent Cloud Mesh console displays tracing data based on the APM data source. You can also view the data independently on the APM console. If a consumer end is not configured for call tracing, the mesh cannot use features such as viewing traces.</td>
<td>No</td>
</tr>
<td>Trace sampling rate</td>
<td>Sampling rate at which the mesh collects data and persists in conducting call tracing. The resources consumed by sidecars during data collection and reporting are positively related to the bandwidth and data volume. Set the sampling rate as required. It is recommended to set the sampling rate to 100% for development and test environments, and 1% for production environments.</td>
<td>No</td>
</tr>
<tr>
<td>Range</td>
<td>To avoid unnecessary overhead, Tencent Cloud Mesh supports enabling sidecar logs for a specific gateway or namespace.</td>
<td>No</td>
</tr>
<tr>
<td>Log format</td>
<td>Tencent Cloud Mesh supports logs in JSON or TXT format.</td>
<td>No</td>
</tr>
<tr>
<td>Output template</td>
<td>Field settings for sidecar logs. There are two formats of predefined templates: default and enhanced. Compared with the fields output in the default format, the fields output in the enhanced format are added with **Trace ID**. If you need to further modify the field settings, customize the log fields by referring to <a href="https://www.envoyproxy.io/docs/envoy/latest/configuration/observability/access_log/usage">Envoy's Standard Specifications</a>.</td>
<td>No</td>
</tr>
<tr>
<td>Consumer end</td>
<td>Sidecar log backend service. Currently, interworking with CLS is supported. After this field is enabled, a log collection component will be deployed on cluster nodes to ensure normal use of the feature.</td>
<td>No</td>
</tr>
</tbody></table>
