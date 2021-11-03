This document describes how to delete a CVM SSH key pair on the SSM console.

## Prerequisite
You have created [a CVM SSH key secret](https://intl.cloud.tencent.com/document/product/1078/42683). 
- Before deleting a secret, you need to disable it first.
- The secret that is to be deleted does not bound to an instance.
>? If the secret you want to delete is bound to a CVM instance, unbind them first.

## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **CVM SSH Key** on the left sidebar.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6dc101c473746a93db5e8484906f7649.png)
2. On the **CVM SSH Key** page, click the drop-down list in the top left corner to select a region.
   ![](https://qcloudimg.tencent-cloud.cn/raw/2cf5ca140fb4b47aae8bbc8fc5f227be.png)
3. Click the search box, select a filter (**Tag** or **Secret Name**) from the list, and enter keywords to get results.
![](https://qcloudimg.tencent-cloud.cn/raw/2683c5fec852e996db5f26a2f8bd3f13.png)
4. Locate the secret you want to remove, and click **Delete** on the right of the secret.
![](https://qcloudimg.tencent-cloud.cn/raw/eb5f3828f2ea838dad5a6d949b3e3b21.png)
5. On the deletion page, choose an option as needed, and then click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/d55efe86b592e95d417ffb1b70ce08fd.png)
