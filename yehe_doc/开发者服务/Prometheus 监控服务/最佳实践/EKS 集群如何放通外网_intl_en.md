## Overview
TMP is integrated with CM. When creating an integration, if you select COS, you need to enable public network access for the EKS cluster of the target CM exporter, as COS doesn't support private network access.


## Directions
1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. Click the target instance to enter the instance management page. Then, click **Integration Center** > **Integration List**.
3. Click **Log** in the **Operation** column of the line where **Type** is **CM**.
![](https://qcloudimg.tencent-cloud.cn/raw/1c9df655c6ed84579aa47d39492ec49a.png)
4. On the topbar, switch to the Pod management page. Click the instance name to enter the cluster page.
5. On the **Basic Info** page, click **Container Network**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/69fe20787ca41b0f5b2520da5e8568c6.png" width="60%">
6. On the topbar of the container network page, switch to the **Routing Policy** tab. Click the route table link (`rtb-xxx` in the list) to enter the route table page.
![](https://qcloudimg.tencent-cloud.cn/raw/e303e2c8860e3f082f6f5a48a2441e2a.png)
7. On the route table page, click **Create Routing Policy**.
 - **Destination**: Enter `0.0.0.0/0`.
 - **Next Hop Type**: Select **NAT Gateway**.
 - **Next Hop**: Select the target gateway. If there is no gateway, create one as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/1015/30251).
![](https://qcloudimg.tencent-cloud.cn/raw/0bd4613874e997ddfa211325a41a674a.png)
8. Click **Create**. After the creation is successful, public network access is enabled for EKS.
