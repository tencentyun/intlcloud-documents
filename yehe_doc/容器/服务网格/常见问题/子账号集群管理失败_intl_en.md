When you try to operate a service mesh after logging in the Tencent Cloud console as a sub-account, you may encounter permission problems. For example, if you fail to associate a cluster, you will be prompted for insufficient permission. You will also be prompted for insufficient permission when viewing services.

## Cause
The core point is that the currently logged-in sub-account needs to have the permission to operate the clusters associated with the mesh. If the sub-account does not have the permission to operate all or some clusters, you need to authorize the sub-account (authorization on each cluster is required). Refer to the following authorization method.


## Cluster Authorization Method
1. Log in to the Tencent Cloud console as the Tencent Cloud account that creates the cluster (this account will be used to authorize sub-accounts), enter the [TKE console](https://console.cloud.tencent.com/tke2/cluster), and then choose **Authorization management** > **RBAC policy generator**.

2. Select the sub-account to be authorized.

3. Grant the admin permissions.
   
