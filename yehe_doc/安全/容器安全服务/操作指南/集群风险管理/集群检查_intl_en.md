The security check feature provides the security checklist, cluster risk statistics, security check details, and check item management. It allows installing the scanner for specified clusters, performing risk checks, and viewing cluster risk details.

### Installing the Scanner
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Cluster Risk Management** > **Security Check** on the left sidebar.
2. The **Security Check** page presets a scheduled cluster sync every hour. Click **Sync assets** to manually sync clusters.
>?
>- Currently, the security checklist applies to the sync of TKE managed and self-deployed clusters.
>- During your first use of cluster security, you need to manually "sync the assets" once, and the system will then automatically sync them.

![](https://qcloudimg.tencent-cloud.cn/raw/7031ddb1b8fed22aa11645ce44830894.png)
3. On the **Security Check** page, install the component for a single or multiple clusters.
 - Single: Select the target **Cluster ID** and click **Install scanner** or **Install component**.
![](https://qcloudimg.tencent-cloud.cn/raw/116858e19232e7c1197a87c6d94b9610.png)
 - Multiple: Select the target **Cluster IDs** and click **Install component**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/ff5c95d724983ab6038591713a3b5766.png)
4. In the pop-up window, click **OK**.
5. After the confirmation, the system will deploy the DaemonSet component on all nodes in the cluster. The scanner will be in the **Running** status after the installation.
>?
>- When the scanner is installed, the `cluster-security-defender` DaemonSet workload will be installed in the `kube-system` namespace of the cluster. To execute a cluster security check, make sure that the DaemonSet workload runs normally.
>- DaemonSet doesn't affect cluster running or performance. It is subject to the following resource limits:
>    - CPU: 100–250 MB
>    - MEM: 100–250 MiB
>- To delete the scanner, log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster), click **Workload** on the **Cluster details** page, select **DaemonSet**, select **cluster-security-defender** in the `kube-system` namespace, and click **More** > **Delete** in the **Operation** column.


### Performing a Security Check
On the [**Security Check**](https://console.cloud.tencent.com/tcss/cluster/clusterCheck) page, the system will automatically perform a check after the scanner is installed successfully. You can specify a cluster and click **Check again**, or specify multiple clusters and click **Batch check**.
>? The scanner is not installed by default and needs to be installed before a scan is performed.

![](https://qcloudimg.tencent-cloud.cn/raw/6bcf4fb08f467e1330e2a8bea61ddbda.png)

### Viewing the Security Check Result
1. On the [**Security Check**](https://console.cloud.tencent.com/tcss/cluster/clusterCheck) page, the **Statistics** card displays the total number of clusters and the numbers of clusters involving no risks and those not checked.
![](https://qcloudimg.tencent-cloud.cn/raw/7dba53ecdfc470e3302f7629d3bd9b3a.png)
2. The **Cluster risks** card displays the numbers of risky clusters and clusters involving critical risks, high risks, medium risks, and low risks.
![](https://qcloudimg.tencent-cloud.cn/raw/f65b5d8d09aed1a78126b26e6afb88b7.png)
3. On the **Security Check** page, click **View details** in the **Operation** column of the cluster list to enter the **Cluster risk details** page.
![](https://qcloudimg.tencent-cloud.cn/raw/13f0f6992dc5e8281a1dee4c7ef543f6.png)
4. The **Cluster risk details** page displays all identified cluster risks, cluster details, and risk details of the current cluster.
<img src="https://qcloudimg.tencent-cloud.cn/raw/901a85bb392e83a53315e77116d378dd.png" style="zoom:67%;" />
5. On the risk details list, select the target check item and click **View details** to enter the **Risk check item details** page.
![](https://qcloudimg.tencent-cloud.cn/raw/2d4c7aa97e6cd81f296e46fc1e6a2876.png)
6. The **Risk check item details** page displays the risk details, description, solution, and affected assets in the current cluster.


### Enabling Automatic Check
#### Enabling automatic check for a single cluster
1. On the [**Security Check**](https://console.cloud.tencent.com/tcss/cluster/clusterCheck) page, select the target cluster and toggle on ![](https://qcloudimg.tencent-cloud.cn/raw/a29676450dd11f574cbb0d0b12914d43.png).
![](https://qcloudimg.tencent-cloud.cn/raw/eec4362eeb98a8e628f3a0d6fe4446b0.png)
2. In the pop-up window, click **OK**.
>? After the confirmation, automatic check will be enabled and performed as follows:
>- Nodes newly added to the cluster will be automatically checked.
>- The cluster will be checked across every midnight.

#### Enabling automatic check for multiple clusters
On the [**Security Check**](https://console.cloud.tencent.com/tcss/cluster/clusterCheck) page, select multiple clusters and click **Batch check**.
>? Automatic security check is disabled by default and can be enabled for the following check items:
>- Nodes newly added to the cluster will be automatically checked.
>- The cluster will be checked across every midnight.

### Managing Security Check Items
1. On the [**Security Check**](https://console.cloud.tencent.com/tcss/cluster/clusterCheck) page, click **Check item management** in the top-right corner.
2. On the check item settings page, the list of check items displays all check items of a security check performed by the system. Click **View details** to view the check item details.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8ff009095fd5af7ea27054e476bad29b.png" style="zoom:67%;" />