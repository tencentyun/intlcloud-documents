## Overview
In actual use, you may find that the configurations of the nodes in your cluster need to be upgraded, especially when the CPU or memory resources of the master nodes are insufficient. This document describes how to change the instance configuration in the [EMR console](https://console.cloud.tencent.com/emr).

>! 
>- The node will be shut down during the change. Note that the shutdown may affect the normal use of the cluster and even interrupt your business. Proceed with caution.
>- The size of data disks and system disks cannot be changed.

## Notes
1. If the configurations of pay-as-you-go nodes are changed, the billing will start over again from the first tier.
2. The configurations of local disk models, Pod resources, and spot instance models cannot be changed.
3. If you batch adjust configurations, the system will automatically deduct fees one by one. Make sure your account has sufficient balance.
4. The refund will be credited to your Tencent Cloud account at the ratio of cash to trial credit paid upon purchase, but the discount amount or voucher (if any) will not be refunded.


## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list.
2. Select **Cluster resources** on the cluster details page to enter the **Resources** page. Click **Change configuration** of the target node. Batch change is supported, but you can only change the configurations of nodes in the same billing mode to the same configurations.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ivAb492_%E5%9B%BD%E9%99%8523.png)
3. On the configuration adjustment page, confirm the relevant information, read carefully the notes, and select **I have read and understood the notes and agree to the operation**.
4. On the **Select target configuration** tab, select the model, instance type, spec, and other configuration items. After confirming the cost, click **Confirm**.
5. The fees to be paid for adjusting the configurations of different nodes to the same configurations will be displayed on the billing details page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4Q8C914_%E5%9B%BD%E9%99%8524.png)
6. (Optional) To adjust the resources of the component after configuration adjustment, you need to deliver the configurations again in **Configurations** and restart the service.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4Q8C914_%E5%9B%BD%E9%99%8524.png)

>! 
>- The YARN resources will be automatically adjusted according to the model and specification by default. After configuration adjustment, the size of the resources will change as the specification changes and does not need to be adjusted manually.
>- If you have manually adjusted the configurations of YARN resources, then after configuration adjustment, you need to modify the values of the `yarn.nodemanager.resource.cpu-vcores` and `yarn.nodemanager.resource.memory-mb` configuration items in **Configurations**, click **Save configuration** to deliver the configurations, and restart the NodeManager service to update the configurations of YARN resources.
