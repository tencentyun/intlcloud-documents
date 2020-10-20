## Operation Scenario
You can use the feature for sharing the same CLB among multiple Services to support the simultaneous opening of TCP and UDP on the same port for the same VIP.
>! This feature is not recommended for other scenarios.



## Descriptions
- **For clusters created before Aug. 17, 2020, the CLBs created by their Services support the sharing of the same CLB by default.**
For a cluster where the CLB sharing feature is enabled, the CLBs created by its Services are configured with the `<serviceUUID>:tke-lb-serviceId` and `<serviceUUID>_<lb_listener_id>:<lb_listener_id>` tags by default. Each CLB has its own key and value, so there are many tags. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20TKE&step=1) to request that we disable the CLB sharing feature for this kind of cluster and clear the tags.
- **For clusters created after Aug. 17, 2020, the feature of multiple Services sharing the same CLB is disabled by default.**
For a cluster where the CLB sharing feature is disabled, the CLBs created by its Services are configured with the `tke-lb-serviceuuid:<serviceUUID>` tag by default. All Services use the same batch of tag keys, and the number of tag keys can be controlled. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20TKE&step=1) to request that we enable the CLB sharing feature.
- **In a scenario where multiple Services share the same CLB, the number of listeners managed by a single CLB cannot exceed 10.**

## Directions
1. Refer to [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662) and create a Service of the Loadbalancer type.
2. Wait until the Service is created, select a type, and go to the CLB details page, as shown in the figure below: 
![](https://main.qcloudimg.com/raw/cf0c44dd72de3b077e809e53b521531f.png)、
<span id="Step3"></span>
3. Record the CLB ID and name generated on the CLB details page, as shown in the figure below: 
![](https://main.qcloudimg.com/raw/4dfb4ead46f5c376be67cdc3f7c2949b.png)
4. Refer to [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662) again and use the existing CLB from [Step 3](#Step3) to create a second Service.
