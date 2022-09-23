
## Overview

You need to bind an EIP or configure a NAT Gateway for the container instance and pay additional network fees when the EKSCI needs to connect to a public network, such as deploying a Nginx service, pulling a private image etc. There are two methods for this.


| Method | Description and Use Cases | Cost |
|---------|---------|---------|
| <nobr>Binding an EIP</nobr> | Elastic IP (EIP) is a fixed public IP address under a certain region and can be purchased and held independently.<br>Use cases: a single instance or a few instances need to interconnect with a public network, for example, the Nginx service. | When EIP has not been bound with cloud resource, only IP resource fees are charged. When EIP has been bound with cloud resource, only public network fees are charged. For more information, see [Billing for Elastic Public IP](https://intl.cloud.tencent.com/zh/document/product/213/17156). |
| Binding a NAT Gateway | A NAT Gateway is a IP address translation service. It provides secure and high-performance Internet access service for the resources in a VPC.<br>Use cases: multiple instances under a VPC need to communicate with a public network. For example, multiple instances need to pull images from a third-party image repository. | NAT Gateway service fees consists two parts: gateway fees (bill on an hourly basis) and network fees (bill by traffic). For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1015/30248). |

This document describes how to bind an EIP to a container instance, so as to enable the container instance to interconnect with a public network. The steps are as follows:


## Directions

<dx-alert infotype="explain" title="">
You need to bind an EIP when creating the container instance.
</dx-alert>




1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/eksci) to go to the container instance page.
2. Click **Create Instance**.
3. Configure the parameters of the container instance based on actual needs. For more information, see [Creating a Container Instance](https://cloud-doc.isd.com/document/product/457/57341#step2). Click **Next**.
4. Enable "Binding an EIP". You can use one of the two methods to bind.
<dx-tabs>
::: Auto-creating an EIP
A container instance supports auto-creating an EIP and binding with it. The attributes are as follows:
- Peak bandwidth, which needs to be customized by you. It will affect billing. Please check the details and select appropriate peak bandwidth based on your needs.
- Lifecycle, which is consistent with the container instance. When you delete the container instance, the lifecycle is deleted simultaneously.
:::
::: Using an existing EIP
You can also select an existing EIP. If you choose this method, you need to create an EIP in advance. If there is no appropriate one, please click [Create EIP](https://console.cloud.tencent.com/cvm/eip).
:::
</dx-tabs>
4. Click **Confirm** to complete the process.
