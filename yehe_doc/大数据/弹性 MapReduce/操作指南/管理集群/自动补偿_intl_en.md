## Overview
The system continuously monitors task nodes and router nodes in a cluster for any abnormal running status. If any exceptions are detected, the system automatically purchases nodes of the same model to replace the affected nodes. Meanwhile, alarms are sent to notify users of the replacement result.
>! When "Instance Termination Protection" is enabled for nodes, this action cannot be triggered.

## Replacement Principle
1. Only pay-as-you-go and spot instance nodes support automatic replacement.
2. The system purchases only nodes of the same model in the same billing mode as abnormal nodes for automatic replacement.
3. When automatic replacement is not enabled, you can still receive alarms in the event of any node abnormalities.
4. Automatic replacement and exception monitoring are not supported for Pod nodes.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click **Cluster List** in the left sidebar. On the page that appears, click the **ID/Name** of the cluster for which you want to enable automatic replacement.
2. Choose **Instance Information** > **Basic Configuration** and enable **Automatic Replacement**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/k8jv837_%E5%9B%BD%E9%99%8541.png)
