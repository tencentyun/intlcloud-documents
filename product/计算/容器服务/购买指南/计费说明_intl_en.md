The TKE service itself is free of charge for the time being, but you need to pay for the actually used Tencent Cloud resources. The use of TKE involves the following products. For more information, see the corresponding product's billing documents.

- [Pay-as-you-go CVM](https://intl.cloud.tencent.com/doc/product/213/2180#2.-.E6.8C.89.E9.87.8F.E8.AE.A1.E8.B4.B9)
- [Pay-as-you-go CBS](https://intl.cloud.tencent.com/document/product/362/2413)
- [CLB billing description](https://intl.cloud.tencent.com/document/product/214/8848)

>TKE is based on Kubernetes and is a declarative service. If you have created IaaS resources such as CLB load balancers or CBS cloud disks in TKE and no longer need to use them, please delete the corresponding Service and PersistentVolumeClaim objects in the TKE Console. If you only delete the load balancers in the CLB Console or the cloud disks in the CBS Console, TKE will recreate them and fees will continue to be incurred.

