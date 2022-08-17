## Traffic Management Model of Tencent Cloud Mesh

Tencent Cloud Mesh is fully compatible with Istio's native traffic management CRDs Gateway, VirtualService, and DestinationRule, and presents the native traffic management syntax as a product. The following figure shows the traffic management model of Tencent Cloud Mesh:

![](https://qcloudimg.tencent-cloud.cn/raw/629939a71bc86e64f73df1d5036a3f41.png)

Tencent Cloud Mesh uses Gateway, VirtualService, and DestinationRule to manage traffic.

- Gateway: defines the port, listening rule, and certificate configurations of a gateway. Gateways and gateway configurations are in a one-to-many relationship. The Gateway specifies a gateway to which the configurations are to be delivered through the selector field.
- VirtualService: defines routing rules and traffic operation rules for a specified host. The VirtualService specifies a bound domain name through the hosts field. It can specify that traffic comes from a gateway or an internal component of a mesh.
- DestinationRule: defines versions and traffic policies of a service. The traffic policies include load balancing, health check, and connection pools. Services and DestinationRules are in a one-to-one binding relationship.

## Traffic Management Configuration Methods

At present, Tencent Cloud Mesh provides the following two methods of configuring Gateways, VirtualServices, and DestinationRules：


<dx-tabs>
::: Console UI Configuration
You can use the console UI to create, delete, update, and view Gateways, VirtualServices, and DestinationRules.

- Creating a Gateway
![](https://qcloudimg.tencent-cloud.cn/raw/425f12e06765f2e912e85234692a7042.png)
- Creating a VirtualService
![](https://qcloudimg.tencent-cloud.cn/raw/a244f690e1d666f871d6d9531caa2129.png)
- Creating a DestinationRule: As DestinationRules and services are in a one-to-one binding relationship, operations of creating and managing DestinationRules are performed on the service details page.
![](https://qcloudimg.tencent-cloud.cn/raw/4c51598a9c2d3162dab10e6e85be0c43.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c902d405dbf4cce7fe146f5efad2e2a5.png)
:::
::: Resource Creation via YAML
You can create Istio or Kubernetes resources by clicking **Create via YAML** in the upper right corner of the mesh management window. If the YAML to be submitted contains a Kubernetes resource and the current mesh manages multiple clusters, you need to select a destination cluster to which the YAML-created resource is submitted.

![](https://qcloudimg.tencent-cloud.cn/raw/507b0c8c8d8888a877788744f66a4819.png)
:::
</dx-tabs>

