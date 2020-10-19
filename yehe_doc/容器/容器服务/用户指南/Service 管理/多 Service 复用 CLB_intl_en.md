## Overview
You can use the feature of sharing the same CLB among multiple services to support the simultaneous exposure of TCP and UDP over the same port for the same VIP.
>! This feature is not recommended for other scenarios.



## Notes
- **For clusters created before August 17, 2020, the CLBs created by their services support the sharing of the same CLB by default.**
For a cluster with CLB sharing enabled, the CLBs created by its services are configured with the `tke-lb-serviceId:` and `<lb_listener_id>:<lb_listener_id>` tags by default. Each CLB has its own key and value, resulting in many tags. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20TKE&step=1) to request us to disable the CLB sharing feature for this cluster and clear the tags.
- **For clusters created after August 17, 2020, the feature of sharing the same CLB among multiple services is disabled by default.**
For a cluster with CLB sharing disabled, the CLBs created by its services are configured with the `tke-lb-serviceId:` and `<lb_listener_id>:<lb_listener_id>` tags by default. All service-managing CLBs use the same set of tag keys, resulting in a controllable number of keys. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20TKE&step=1) to request us to enable the feature of sharing the same CLB among multiple services.
- **In a scenario where multiple services share the same CLB, the number of listeners managed by a single CLB cannot exceed 10.**

   

## Directions
1. Create a service of the Loadbalancer type by referring to [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).
2. After the service is created, select a type and go to the CLB details page, as shown in the figure below: 
![](https://main.qcloudimg.com/raw/cf0c44dd72de3b077e809e53b521531f.png)
<span id="Step3"></span>
3. Record the CLB ID and name on the CLB details page, as shown in the figure below: 
![](https://main.qcloudimg.com/raw/4dfb4ead46f5c376be67cdc3f7c2949b.png)
4. Use the existing CLB in [step 3](#Step3) to create another service by referring to [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662) again.
