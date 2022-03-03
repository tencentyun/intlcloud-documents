CLB allows real servers to bind EKS container instances.

## EKS Container Instance
[EKS Container Instance (EKSCI)]() is a container service provided by Tencent Cloud Elastic Kubernetes Service (EKS). EKSCI makes it easy to deploy containers without servers and K8S clusters, and provides VM-level security and resource isolation. Meanwhile, its startup and release are faster than VMs.

Compared to pods in Kubernetes clusters, EKSCI offers a simpler and more underlying containerization solution. It can meet your demand that you only need scheduling and managing container resources without considering management capabilities such as orchestration and scheduling of upper-layer workloads. EKSCI also helps increase efficiency and reduce costs. It frees you from O&M work at the underlying server layer, allowing you to focus on the application layer.
>? EKSCI is in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=2028&source=0&data_title=%E5%BC%B9%E6%80%A7%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20EKS&step=1).

## Restrictions
- Container instance binding is only available to CLB instances (not Classic CLB instances).
- VPC network can be used for container instance binding. Classic network is not supported.
- Binding container instances is supported in [cross-region binding 2.0](https://intl.cloud.tencent.com/document/product/214/38441) and [hybrid cloud deployment](https://intl.cloud.tencent.com/document/product/214/38442) scenarios.
- Layer-4 and layer-7 listeners allows to bind container instances.

## Prerequisites
- You have [submitted a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=2028&source=0&data_title=%E5%BC%B9%E6%80%A7%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20EKS&step=1) to apply for EKSCI service.
- You have created a CLB listener. The following takes a TCP listener as an example. For more details, see [Configuring TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517).

## Directions
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar.
2. On the **Instance Management** page, click **Configure Listener** on the right of an instance.
3. Select a TCP listener on the list and click **Bind** on the right.
4. In the **Bind Real Server** dialog, choose **Container Instance**, select a container instance to bind, set the port and weight, and then click **OK**.
>? To bind to other VPC container instances, you need to associate other VPCs and the VPC you use with the same CCN instance. For more information, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
>
![]()


