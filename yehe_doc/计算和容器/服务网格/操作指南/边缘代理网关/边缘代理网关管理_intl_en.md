A gateway is a special data plane responsible for load balancing between ingress and egress traffic of a mesh. It is deployed as an independent pod but not a sidecar in your cluster. It is classified into two types: ingress gateway and egress gateway. An ingress gateway instance contains an Envoy pod on the data plane and its associated CLB instance (public network or private network). Tencent Cloud Mesh provides a managed [gateway controller](#gatewayController), which has implemented automatic integration of ingress gateway configurations and CL. You can configure the ingress gateway by using Istio CRDs. Tencent Cloud Mesh automatically synchronizes the related configurations to the associated CLB instance. The synchronized configurations include port configurations and enhanced port listening rule configurations. In other words, the Envoy container and associated CLB feature are used as a whole to provide you with ingress gateway capabilities.

If you need the capability to balance the ingress and egress traffic of the mesh, you need to create an ingress gateway or egress gateway instance, and then configure listening rules and traffic management (routing) rules of the gateway by using Istio CRDs such as Gateway, VirtualService, and DestinationRule. The listening rules are configured by using the Gateway CRD, and the traffic management rules are configured by using the VirtualService and DestinationRule CRDs (consistent with the east-west traffic management syntax). The following figure is a schematic diagram of the relationship between gateway instances and Istio CRD configurations.

![](https://qcloudimg.tencent-cloud.cn/raw/4ff31308ce78b47e93a0bdc8f0a4ab39.png)

## Creating a Gateway

1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh).
2. On the mesh creation page, add a service discovery cluster and then create a gateway.
![](https://qcloudimg.tencent-cloud.cn/raw/fd517f22c2aea129e9662128f2ff20c7.png)
Alternatively, on the **Edge gateway** tab page of the mesh details page, click **Create** to create a gateway.
![](https://qcloudimg.tencent-cloud.cn/raw/0b8fea6b80a0b153fc5f8530f4c916c2.png)

Major configuration items for creating a gateway are described as follows.

| Configuration Item | Description |
| ----- | ----- |
| Type | Whether an ingress gateway or an egress gateway is to be created. |
| Access Cluster | Kubernetes cluster in which the gateway is to be created. |
| Namespace | Namespace in which the gateway is to be created. |
| Access type | Ingress gateway parameter. Select a CLB access type. **Public network** and **Private network** are supported.  |
| Load Balancer | Ingress gateway parameter. Select **Automatic creation** or **Use existing**. For more information about using existing CLBs, see [Using Existing CLBs](https://intl.cloud.tencent.com/document/product/457/36835). |
| Billing mode | Ingress gateway parameter. Select a CLB billing mode. **Bill-by-traffic** and **Bill by bandwidth** are supported. For more information about CLB billing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/214/36999). |
| Bandwidth cap | Ingress gateway parameter. Select a CLB bandwidth cap, which ranges from 0 to 2048 Mbps. |
| CLB-to-Pod direct access | Ingress gateway parameter. For example, when the network mode for the gateway to access the cluster is VPC-CNI, **CLB-to-Pod direct access** can be enabled. In this case, traffic is not forwarded through NodePort, so as to improve the performance. Preservation of client source IP, and pod-level session persistence and health check are supported. For more details, see [Using Services with CLB-to-Pod Direct Access Mode](https://intl.cloud.tencent.com/document/product/457/36837). |
| Preserve client source IP | Ingress gateway parameter. Set ExternalTrafficPolicy to **Local** in the ingress gateway service to preserve the client source IP, and enable Local binding and Local weighted balancing. This parameter becomes invalid if **CLB-to-Pod direct access** is enabled. For more details, see [Service Backend Selection](https://intl.cloud.tencent.com/document/product/457/36836). |
| Component Configurations | Configurations about CPU and memory resources and HPA policies of the gateway. |

## Gateway Deployment Modes

Two gateway deployment modes are available: **Normal mode** and **Exclusive mode**.
- **Normal mode**：A gateway service is deployed in a selected service cluster and is deployed indistinguishably from other service pods.
- **Exclusive mode**：In some scenarios, a gateway is deployed on an exclusive node to improve service stability. In the exclusive mode, you need to add some cluster nodes to an exclusive resource pool, and then the mesh sets taints for the selected nodes to ensure exclusive use. After settings, all ingress/egress gateways will be deployed only on the selected nodes. You can further specify nodes for a specific gateway in the advanced settings.

You can adjust the gateway deployment mode on the mesh creation page or the component management page.
>? Adjusting the deployment mode will trigger gateway service scheduling, which may adversely affect service traffic.
>
![](https://qcloudimg.tencent-cloud.cn/raw/95242718623ea1eafbfbdbf5ce2f8f61.png)


## Updating Gateway Configurations

After a gateway is created, you can modify the associated CLB bandwidth (supported only for an ingress gateway), the number of instances, HPA policies, and resource definitions of the gateway.

### Modifying the CLB Bandwidth

You can modify the bandwidth of the CLB instance associated with an ingress gateway. In the gateway area on the **Basic information** tab page on the mesh details page, you can edit configurations of the CLB associated with the ingress gateway. 
![](https://qcloudimg.tencent-cloud.cn/raw/ae3d478889654c9db7beac6cefca47e0.png)


### Modifying the Number of Component Instances

You can adjust the number of component instances by choosing **Mesh details** > **Component management**.

![](https://qcloudimg.tencent-cloud.cn/raw/4432668506a10c90d0e0edf1a45778b9.png)

### Modifying HPA Policies of Components

You can edit HPA policies of components by choosing **Mesh details** > **Component management**. Scaling policies can be configured based on CPU, memory, mesh, and hard disk metrics.

![](https://qcloudimg.tencent-cloud.cn/raw/3a84abdd67d3b7ff92d81173ab29a88c.png)

### Modifying Component Resource Definitions

You can edit component resource definitions, including CPU request, CPU limit, memory request, and memory limit, by choosing **Mesh details** > **Component management**.
![](https://qcloudimg.tencent-cloud.cn/raw/40dbc9fec706d2f2f33d3729105f0861.png)

## Deleting a Gateway

You can delete a specified gateway by choosing **Mesh details** > **Component management** > **Edge gateway**. The procedure is as follows:

1. Access the mesh details page, click **Component management**, click **Edge gateway**, and choose **More** > **Delete** in the **Operation** column where the gateway to be deleted resides.
![](https://qcloudimg.tencent-cloud.cn/raw/0ede45c26792ea8c88d8e4b12a3fb188.png)
2. In the **Delete edge node** dialog box, confirm the name of the gateway to be deleted and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/ba2d32f4b8ad0c5ea97fd7ad02c42834.png)

## Automatic Interworking of the Gateway Controller of Tencent Cloud Mesh with CLB [](id:gatewayController)

Tencent Cloud Mesh implements the managed gateway controller. The controller monitors the gateway configurations delivered to an ingress gateway in real time, parses the current port configurations, and synchronizes the current port configurations to CLB, so that you no longer need to manually configure CLB ports. CLB ports, ingress gateway service ports, and ingress gateway container ports are in one-to-one mapping. To be specific, if the `80` port is defined in the Gateway CRD, the gateway controller of Tencent Cloud Mesh will configure the container port as `80` and the service port as `80` for the ingress gateway instance and enables the `80` port of the associated CLB synchronously.

The gateway controller of Tencent Cloud Mesh also implements the feature of enabling SSL certificate offloading to take place at CLB. In this way, after certificate offloading takes place at CLB, the ingress gateway provides traffic management capabilities. After this feature is configured on the gateway, the gateway controller will resolve the port, domain name, and certificate that are involved in feature configurations, and synchronize the configurations to the CLB instance bound to the ingress gateway.

![](https://qcloudimg.tencent-cloud.cn/raw/3726322a202d61f002c6e102ca5b0d54.png)
