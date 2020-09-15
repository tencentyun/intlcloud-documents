
## TKE Billing Description
The TKE service itself is currently free of charge, but fees are collected for the use of related Tencent Cloud products. Use of TKE may require the use of the following products. For more information, see the billing documents of corresponding products.

- [CVM pricing modes](https://intl.cloud.tencent.com/document/product/213/2180)
- [CBS price overview](https://intl.cloud.tencent.com/document/product/213/2255).
- [Cloud Load Balancer Billing Description](https://intl.cloud.tencent.com/zh/document/product/214/8848)

>! TKE is based on Kubernetes and is a declarative service. If you have created IaaS resources such as CLBs or CBS disks in TKE and no longer need to use them, delete the corresponding Service and PersistentVolumeClaim objects in the TKE Console. If you only delete the CLBs in the CLB Console or the CBS disks in the CBS Console, TKE will recreate them and fees will continue to be incurred.

## EKS Billing Description
EKS is pay-as-you-go and billed based on the configured resources and usage duration. For more information, see [Elastic Cluster Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054).

