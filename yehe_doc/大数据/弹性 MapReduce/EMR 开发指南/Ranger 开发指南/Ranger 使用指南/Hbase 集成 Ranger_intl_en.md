## Preparations
Ranger is available only when it is selected in **Optional Components** when you purchase a cluster. If you add the Ranger component after purchasing the cluster, the Web UI may be inaccessible. By default, when Ranger is installed, Ranger Admin and Ranger UserSync are deployed on the master node, and Ranger Plugin is deployed on the main daemon node of the embedded component.

When creating a cluster of the Hadoop type, you can select Ranger in **Optional Components**. The Ranger version varies depending on the EMR version you choose.
>?When the cluster type is Hadoop and the Ranger optional component is selected, EMR-Ranger will create services for HDFS and YARN by default and set default policies.
>
![](https://main.qcloudimg.com/raw/b27a043dda3df6f2cfa3ae7081dd4c0e.png)

## Ranger Web UI
Before accessing the Ranger Web UI, make sure that the current cluster is configured with a public IP and click the Ranger Web UI URL on the **Cluster Service** page.
![](https://main.qcloudimg.com/raw/75190f3ea2817fd96e8fa13801dc08a9.png)
After you are redirected, enter the username and password that you set when you purchased the cluster.
![](https://main.qcloudimg.com/raw/a0b4159c09c674773b2f3705abbd7d38.png)


## Integrating HBase with Ranger
>!Make sure that HBase related services are running normally and Ranger has been installed in the current cluster.
>
1. Add an EMR Ranger HBase service on the EMR Ranger Web UI.
![](https://main.qcloudimg.com/raw/acc3b5af5f1c4b7186427cb8cc7a837f.png)
2. Configure EMR Ranger HBase service parameters.
![](https://main.qcloudimg.com/raw/bf5058d18d9865a9421821a6dc46fac5.png)
<table>
<thead>
<tr>
<th><strong>Parameter</strong></th>
<th><strong>Required</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody><tr>
<td>Service Name</td>
<td>Yes</td>
<td>Service name, which is displayed on the main HBase component on the Ranger Web UI</td>
</tr>
<tr>
<td>Description</td>
<td>No</td>
<td>Service description</td>
</tr>
<tr>
<td>Active Status</td>
<td>Default</td>
<td>Service status, which is **Enabled** by default</td>
</tr>
<tr>
<td>Username</td>
<td>Yes</td>
<td>Username of the resource</td>
</tr>
<tr>
<td>Password</td>
<td>Yes</td>
<td>User password</td>
</tr>
<tr>
<td>Hbase.zookeeper.property.clientPort</td>
<td>Yes</td>
<td>Request port of the ZooKeeper client</td>
</tr>
<tr>
<td>Hbase.zookeeper.quorum</td>
<td>Yes</td>
<td>ZooKeeper cluster IP</td>
</tr>
<tr>
<td>Zookeeper.znode.parent</td>
<td>Yes</td>
<td>ZooKeeper node information</td>
</tr>
</tbody></table>
3. Configure EMR Ranger HBase resource permissions.
 - Click the configured EMR Ranger HBase service. 
![](https://main.qcloudimg.com/raw/d235d5dff25704fa68e634d268cd7c72.png)
 - Configure a policy. 
![](https://main.qcloudimg.com/raw/9b84df03567605e44664fda64473aae0.png)
In the above figure, the **Users** is **hadoop** and **Policy Name** is **all-table, column-family, column**, meaning HBase users have Region Balance, MemeStore Flush, Compaction, and Split permissions. **Make sure that the created service has these permissions.**
![](https://main.qcloudimg.com/raw/29c52f250c5d5152b6ba73f4e1ad593e.png)
<table>
<thead>
<tr>
<th><strong>Parameter</strong></th>
<th><strong>Required</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody><tr>
<td>HBase Table</td>
<td>Yes</td>
<td>HBase table name</td>
</tr>
<tr>
<td>HBase Column-family</td>
<td>Yes</td>
<td>Column family of the HBase table</td>
</tr>
<tr>
<td>HBase Column</td>
<td>Yes</td>
<td>Qualifiers of the column family</td>
</tr>
</tbody></table>
4. After the policy is added, it will take effect in about 30 seconds, then you can use **user1** to perform operations on the column family and qualifiers of the **order** table.
