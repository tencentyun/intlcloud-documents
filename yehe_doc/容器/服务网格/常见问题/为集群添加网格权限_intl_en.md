## Problem Description
When you try to operate a service mesh after logging in the Tencent Cloud Mesh console as a sub-account, you are prompted that there is no cluster permission.

![](https://qcloudimg.tencent-cloud.cn/raw/15d059a2f1c8b72642b772c685a66e35.png)



## Solution
The currently logged-in sub-account does not have the admin permissions for the cluster. You can use the following method to authorize permissions for the cluster.


### Authorization by the Admin
If your root account has admin permissions, you can use the **Get cluster admin role** feature directly on the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/cluster) to quickly grant your sub-account admin permissions for the cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/41702de5b18d8c74f80eb848c8df1849.png)

### Authorizing Other Sub-accounts
1. Log in to the Tencent Cloud console as the Tencent Cloud account that creates the cluster (this account will be used to authorize sub-accounts).
2. On the [TKE console](https://console.cloud.tencent.com/tke2/cluster), select the cluster.
3. On the cluster details page, choose **Authorization management** > **RBAC policy generator**.
![](https://qcloudimg.tencent-cloud.cn/raw/ce0c5d4953023a33acfc357701d93d3f.png)
4. In the pop-up window, select the sub-account to be authorized.
![](https://qcloudimg.tencent-cloud.cn/raw/e79c0b85f0e0633df93306d67e57f40e.png)
5. Click **Done** to authorize admin permissions.
![](https://qcloudimg.tencent-cloud.cn/raw/e4e18be7944537eb7fae74c30a20e0b9.png)
