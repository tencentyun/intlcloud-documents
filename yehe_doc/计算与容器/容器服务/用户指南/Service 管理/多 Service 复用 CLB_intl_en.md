## Overview
You can use the feature for sharing the same CLB among multiple Services to support the simultaneous opening of TCP and UDP on the same port for the same VIP.
>! This feature is not recommended for other scenarios.
>



## Notes
- **For clusters created before Aug. 17, 2020, the CLBs created by their Services support the sharing of the same CLB by default.**
For a cluster where the CLB sharing feature is enabled, the CLBs created by its Services are configured with the `<serviceUUID>:tke-lb-serviceId` and `<serviceUUID>_<lb_listener_id>:<lb_listener_id>` tags by default. Each CLB has its own key and value, so there are many tags. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20TKE&step=1) to request that we disable the CLB sharing feature for this kind of cluster and clear the tags.
- **For clusters created after Aug. 17, 2020, the feature of multiple Services sharing the same CLB is disabled by default.**
For a cluster where the CLB sharing feature is disabled, the CLBs created by its Services are configured with the `tke-lb-serviceuuid:<serviceUUID>` tag by default. All Services use the same batch of tag keys, and the number of tag keys can be controlled. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20TKE&step=1) to request that we enable the CLB sharing feature.

## Limits
- In a scenario where multiple Services share the same CLB, the number of listeners managed by a single CLB cannot exceed 10.
- In scenarios where a Service is reused, only the user-created Cloud Load Balancer (CLB) can be used. This is because when the CLB created in the TKE cluster is reused, CLB resources may not be released, leading to a resource leak.
- To reuse CLB resources created by the current TKE, you can add `service.kubernetes.io/tke-existed-lbid` annotation to the current Service, and delete the `tke-createdBy-flag = yes` tag of this CLB.
>! After reusing CLB resources created by the current TKE, you need to manually manage the CLB resources, because the CLB's life cycle will not be controlled by the TKE due to the lack of the tag.


## Directions
1. [](id:Step1)Refer to [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149) to create a CLB for the public or private network of the VPC where the cluster is located.
2. Refer to [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662) or [Creating a Service](https://intl.cloud.tencent.com/document/product/457/36833) to create a Service of the Loadbalancer type. Select **Use Existing** for **Load Balancer** and choose the CLB instance created in [Step 1](#Step1), as shown in the following figure.
![](https://main.qcloudimg.com/raw/6e98284605215d156a2c945d2a729652.png)
3. Repeat Step 2 to reuse the same CLB for multiple Services.
