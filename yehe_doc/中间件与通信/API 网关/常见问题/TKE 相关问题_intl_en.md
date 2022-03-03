## How to enable private network access for a TKE cluster?

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Cluster** in the left sidebar.
2. Click the ID or name of the desired cluster to go to the cluster details page.
3. Click **Basic Information** in the left sidebar. You can view information such as the access address, public network/private network access status, and kubeconfig access credential of the cluster in the "Cluster APIServer information" section of the **Basic information** page. See the figure below.
4. Enable the **Private network access**. You need to configure a subnet. IP addresses are assigned from the configured subnet after private network access is successfully enabled.
>! Do not disable the private network access after you enable it. Otherwise, the API Gateway cannot access the APIServer of the cluster.


## How to obtain the TKE cluster admin role?

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Cluster** in the left sidebar.
2. Click the ID or name of the desired cluster to go to the cluster details page.
3. Click **Authorization Management** > **ClusterRole** in the left sidebar. Click **Get cluster admin role** on the page.
4. Failure to obtain the cluster admin role is generally caused by the sub-account not having the Cam permission of the TKE cluster. If this is the case, proceed according to the prompts.
