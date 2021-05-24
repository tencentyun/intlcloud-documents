## Preparations
Ranger is available only when it is selected in **Optional Components** when you purchase a cluster. If you add the Ranger component after purchasing the cluster, the Web UI may be inaccessible. By default, when Ranger is installed, Ranger Admin and Ranger UserSync are deployed on the master node, and Ranger Plugin is deployed on the main daemon node of the embedded component.

When creating a cluster of the Hadoop type, you can select Ranger in **Optional Components**. The Ranger version varies depending on the EMR version you choose.
>?When the cluster type is Hadoop and the Ranger optional component is selected, EMR-Ranger will create services for HDFS and YARN by default and set default policies.
>
![](https://main.qcloudimg.com/raw/9f647836f1ef58b473f9e1481655034c.png)

## Ranger Web UI
Before accessing the Ranger Web UI, make sure that the current cluster is configured with a public IP and click the Ranger Web UI URL on the **Cluster Service** page.
![](https://main.qcloudimg.com/raw/185a66ab82272bdec3b6db97071d0af3.png)
After you are redirected, enter the username and password that you set when you purchased the cluster.
![](https://main.qcloudimg.com/raw/a0b4159c09c674773b2f3705abbd7d38.png)

## Component Integration
### Integrating HDFS with Ranger
>!Make sure that HDFS related services are running normally and Ranger has been installed in the current cluster.
>
1. Add an EMR Ranger HDFS service on the EMR Ranger Web UI.
![](https://main.qcloudimg.com/raw/74f103c458aa2327cd3eb8c7ad2009ef.png)
2. Configure EMR Ranger HDFS service parameters.
![](https://main.qcloudimg.com/raw/c73a4fa6907df6be4bc1f2b6fac87106.png)
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
<td>Service name, which is displayed on the main HDFS component on the Ranger Web UI</td>
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
<td>NameNode URL</td>
<td>Yes</td>
<td>HDFS URL</td>
</tr>
<tr>
<td>Authorization Enabled</td>
<td>Default</td>
<td>Select **No** for standard clusters and **Yes** for high-security clusters.</td>
</tr>
<tr>
<td>Authorization Type</td>
<td>Yes</td>
<td>**Simple**: standard cluster; **Kerberos**: high-security cluster</td>
</tr>
</tbody></table>
3. Configure EMR Ranger HDFS resource permissions.
 - Click the configured EMR Ranger HDFS service. 
![](https://main.qcloudimg.com/raw/3c2d2defa092584909a3d1b2a2021eff.png)
 - Configure a policy. 
![](https://main.qcloudimg.com/raw/4e103c65e9de153c4c1cd8d77dcaf33c.png)
![](https://main.qcloudimg.com/raw/af3820edcbeccfb95ef757e262b1eb12.png)
4. After the policy is added, it will take effect in about 30 seconds, then you can use **user1** to read and write the **/user** of the HDFS file system.

### Integrating YARN with Ranger
>!Make sure that YARN related services are running normally and Ranger has been installed in the current cluster.
>
Currently, EMR Ranger YARN only supports ACLs for Capacity Scheduler queues, not for Fair Scheduler queues. Ranger YARN's queue ACLs take effect together with YARN's built-in Capacity Scheduler configuration, but with lower priority. Ranger YARN permissions will be verified only when YARN's built-in Capacity Scheduler configuration denies verification. **You are advised to set ACLs via Ranger, instead of in the configuration files.**

1. Add an EMR Ranger YARN service on the EMR Ranger Web UI.
![](https://main.qcloudimg.com/raw/b574991466eb89ebb990c4c9dc56a236.png)
2. Configure EMR Ranger YARN service parameters.
![](https://main.qcloudimg.com/raw/40ee44b63186f88216f0c657b7a9f018.png)
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
<td>Service name, which is displayed on the main YARN component on the Ranger Web UI</td>
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
<td>NameNode URL</td>
<td>Yes</td>
<td>YARN URL</td>
</tr>
<tr>
<td>Authorization Enabled</td>
<td>Default</td>
<td>Select **No** for standard clusters and **Yes** for high-security clusters.</td>
</tr>
<tr>
<td>Authorization Type</td>
<td>Yes</td>
<td>**Simple**: standard cluster; **Kerberos**: high-security cluster</td>
</tr>
</tbody></table>
3. Configure EMR Ranger YARN resource permissions.
 - Click the configured EMR Ranger YARN service. 
![](https://main.qcloudimg.com/raw/57b34f9adde606c40f52bf76f1e43c36.png)
 - Configure a policy. 
![](https://main.qcloudimg.com/raw/68cceaed942cea8da21222b3d6903a19.png)
![](https://main.qcloudimg.com/raw/f83dfe20e6cecbb6f5bf1901dd4ffabf.png)
4. After the policy is added, it will take effect in about 30 seconds, then you can use **user1** to submit, kill, or query jobs in the `root.default` queue of YARN.

>!When configuring Ranger YARN services and policies, make sure that there are no YARN jobs during this period; otherwise, issues about job submission permissions may occur.

### Integrating HBase with Ranger
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
![](https://main.qcloudimg.com/raw/83ee03d59671dd641d155a8c36cdaefa.png)
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

### Integrating Presto with Ranger
>!Make sure that Presto related services are running normally and Ranger has been installed in the current cluster.
>
1. Add an EMR Ranger Presto service on the EMR Ranger Web UI.
![](https://main.qcloudimg.com/raw/53202d00bdc86897c076caf1fdb139b8.png)
2. Configure EMR Ranger Presto service parameters.
![](https://main.qcloudimg.com/raw/6f096bcccb58a5c52e7e0a4b258d6c9a.png)
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
<td>Service name, which is displayed on the main Presto component on the Ranger Web UI</td>
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
<td>JDBC.driverClassName</td>
<td>Yes</td>
<td>Full path of the drive class name</td>
</tr>
<tr>
<td>jdbc.url</td>
<td>Yes</td>
<td>Presto JDBC connection URL, for example, jdbc:presto://ip/hostname:port</td>
</tr>
</tbody></table>
3. Configure EMR Ranger Presto resource permissions.
 - Click the configured EMR Ranger Presto service.
![](https://main.qcloudimg.com/raw/c47fa2c22c26241a855fa07aaec53e7c.png)
 - Configure a policy. 
![](https://main.qcloudimg.com/raw/4e7f4d64de70f3dc20a8dd266156d490.png)
![](https://main.qcloudimg.com/raw/d424df462aa8263ecb3fa12dce16e7b0.png)
4. After the policy is added, it will take effect in about 30 seconds, then you can use **user1** to view and use the catalog of Presto.
