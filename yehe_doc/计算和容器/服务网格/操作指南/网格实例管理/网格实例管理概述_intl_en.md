A mesh instance is a logically isolated space for managing services, and services within the same mesh can communicate with each other.
![](https://qcloudimg.tencent-cloud.cn/raw/0839f6b1448c611cc18ee547b8b2367a.png)

Lifecycle statuses of a mesh are described as follows:

 

<table>
<thead>
  <tr>
    <th width="20%">Status</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Creating</td>
    <td>The mesh is being created, and its details cannot be viewed.</td>
  </tr>
  <tr>
    <td>Running</td>
    <td>The mesh is running normally.</td>v
  </tr>
  <tr>
    <td>Upgrading</td>
    <td>The mesh is being upgraded, and some features are unavailable.</td>
  </tr>
  <tr>
    <td>Idle</td>
    <td>When all service discovery clusters managed by the mesh are deleted or disassociated, the mesh will enter an idle state. The mesh in the idle state can be viewed normally, but some features are unavailable due to no service entity. You can add a new service discovery cluster for the mesh to restore it to a normal state.</td>
  </tr>
  <tr>
    <td>Invalid</td>
    <td>When the mesh remains idle for more than 30 days, or the primary cluster of a stand-alone mesh is deleted, the mesh will enter an invalid state and you will no longer be able to perform operations on the mesh other than deletion.</td>
  </tr>
  <tr>
    <td>Abnormal</td>
    <td>Some components in the mesh are abnormal, which have adverse impact on the mesh features.</td>
  </tr>
</tbody>
</table>

The following configurations are required during mesh creation:
- **Adding a service discovery cluster**
This can be implemented by adding a Kubernetes service discovery cluster to automatically discover a service in the cluster or by manually registering a service. The discovered service in the mesh will be displayed in the list on **Mesh details** > **Service** on the Tencent Cloud Mesh console. After the service is discovered, it can be accessed by other services in the mesh. For detailed instructions, see [Service Discovery Management](https://intl.cloud.tencent.com/document/product/1152/47467).
- **Creating a gateway**
Gateways are divided into two types: ingress and egress, which are the entrance and exit of mesh traffic. Ingress gateways must be created to ensure that traffic can enter the mesh. Egress gateways are optional. For detailed instructions, see [Gateway Management](https://intl.cloud.tencent.com/document/product/1152/47471).
- **Injecting sidecars for a service**
Sidecar containers are responsible for mesh governance such as data plane traffic management, rule validation, monitoring and reporting. They are the basis for mesh traffic governance and observation. Therefore, for services that require traffic management and observation, sidecars need to be injected into them. For detailed instructions, see [Mesh Configuration](https://intl.cloud.tencent.com/document/product/1152/47464).  
- **Configuring an observability backend service**
Observability includes three parts: monitoring metric viewing, call tracing, and log management. Tencent Cloud Mesh supports integration with Managed Service for Prometheus (TMP), Application Performance Management (APM), and Cloud Log Service (CLS) to provide richer and integrated observability capabilities. In addition, Tencent Cloud Mesh also supports interworking with third-party Prometheus, Jaeger/Zpkin services to provide you with greater component scalability. For detailed instructions, see [Observability](https://intl.cloud.tencent.com/document/product/1152/47478). 

After the mesh is created, you can schedule traffic rules of the mesh, or create traffic governance rules for the mesh through the console or by submitting a YAML file. Currently, Tencent Cloud Mesh is fully compatible with Istio's native syntax. For detailed instructions, see [Traffic Management](https://intl.cloud.tencent.com/document/product/1152/47474).
