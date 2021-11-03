This document describes how to associate SSH keys with CVM instances on the SSM console.

## Prerequisite
- You have created a [CVM SSH key secret](https://intl.cloud.tencent.com/document/product/1078/42683). 
- You have created a CVM instance. For details, see [Guidelines for Creating Instances](https://intl.cloud.tencent.com/document/product/213/36302).

## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **CVM SSH Key** on the left sidebar.
   ![](https://qcloudimg.tencent-cloud.cn/raw/a0d86ff8018e79dabc72bb3daf2f05b1.png)
2. On the **CVM SSH Key** page, click the drop-down list in the top left corner to select a region.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8adaab99046ba923642cbf227547a9a4.png)
3. Click the search box, select a filter (**Tag** or **Secret Name**) from the list, and enter keywords to get results.
![](https://qcloudimg.tencent-cloud.cn/raw/7d1fc5eddcc362b445bedf8af4d564ad.png)
4. Select the secret you want to associate with a CVM instance, and click **Associated Resources** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/39e2c16e032923463dcd41fabe7239c2.png)
5. On the **SSH Key** page of the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1), click **Bind Instance** on the right of the CVM instance you selected.
![](https://qcloudimg.tencent-cloud.cn/raw/8536318fa2edd85cd43720793648d90d.png)
