## Feature Overview
Instance information records the basic information of your EMR cluster. You can view the basic configuration, software information, and hardware information of the cluster on the instance information page.
- The basic configuration section displays basic information of the cluster, such as network information, creation time, security group, and high-availability enablement status.
- The software information section displays the cluster type, software tools installed in the cluster and their version numbers, COS activation status, and Kerberos mode enablement status.
- The hardware configuration section displays the quantity of nodes in each type.

This document describes how to view the cluster instance information in the console.

## Directions
1. After you successfully create a cluster, log in to the [EMR Console](https://console.cloud.tencent.com/emr) and click the **ID/Name** or of the cluster to be managed on the **Cluster List** page.
![](https://main.qcloudimg.com/raw/bb5497a544bf822644e6ee4051c11803.png)
2. If COS has not been activated for a cluster, and you want to activate it now for business needs, you can click **Set** and enter the test verification address, `SecretID`, and `SecretKey` as required.
>To ensure that COS can be properly activated and take effect after authentication, please make sure that the access domain names corresponding to the `SecretID` and `SecretKey` are the same. For detailed directions, please see [Manually Activating COS in Console](https://intl.cloud.tencent.com/document/product/1026/34570).
>
![](https://main.qcloudimg.com/raw/1b2adb3004a6b28e883f342d551d0f4d.png)
