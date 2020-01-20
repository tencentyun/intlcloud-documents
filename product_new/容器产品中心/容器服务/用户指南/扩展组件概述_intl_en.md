
>The add-on feature is currently under beta. They are slated for official release in December, 2019. Once they are released, you can view them in the [TKE Console](https://console.cloud.tencent.com/tke2). 
>

## Overview
Add-ons are extended feature packages provided by Tencent Cloud TKE. You can deploy the add-ons according to your business requirements. Add-ons can help you manage cluster Kubernetes components, including component deployment, upgrades, and configuration updates.


## Add-on Types

There are two categories of add-ons: basic add-ons and advanced add-ons.

### Basic add-ons

Basic add-ons are software packages that TKE features depend on. For example, the CLB add-on `Service-controller` and `CLB-ingress-controller`, and TKE network add-on `tke-cni-agent`, etc.
>
>- The upgrade and configuration management of basic add-ons are fully managed by TKE. It is recommended that you do not modify basic add-ons.
>- When basic add-ons are updated, you will be notified by email and SMS.



### Advanced add-ons

Advanced add-ons are add-ons provided by TKE that can be deployed optionally. You can deploy advanced add-ons to use advanced features supported by TKE:
- By deploying the `PersistentEvent` add-on, you can persistently store the Kubernetes Events of a TKE cluster to a consumer.
- By deploying the `LogCollector` add-on, you can quickly collect business logs on a TKE cluster, and report them to a log consumer.
- By deploying the `Helm` add-on, you can quickly deploy community software packages in a TKE cluster.
- By deploying the `GPU-Manager` add-on, you can use GPU resources in a TKE cluster in a more fine-grained manner.


