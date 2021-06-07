## Preparations
Ranger is available only when it is selected in **Optional Components** when you purchase a cluster. If you add the Ranger component after purchasing the cluster, the Web UI may be inaccessible. By default, when Ranger is installed, Ranger Admin and Ranger UserSync are deployed on the master node, and Ranger Plugin is deployed on the main daemon node of the embedded component.

When creating a cluster of the Hadoop type, you can select Ranger in **Optional Components**. The Ranger version varies depending on the EMR version you choose.
>?When the cluster type is Hadoop and the Ranger optional component is selected, EMR-Ranger will create services for HDFS and YARN by default and set default policies.
>
![](https://main.qcloudimg.com/raw/e744dc5ce95b1a2dc17f2765b4abe721.png)

## Ranger Web UI
Before accessing the Ranger Web UI, make sure that the current cluster is configured with a public IP and click the Ranger Web UI URL on the **Cluster Service** page.
![](https://main.qcloudimg.com/raw/002d2aeeb1349f12b3c811b1bbae7ea4.png)
After you are redirected, enter the username and password that you set when you purchased the cluster.
![](https://main.qcloudimg.com/raw/a0b4159c09c674773b2f3705abbd7d38.png)

## Integrating Presto with Ranger
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
![](https://main.qcloudimg.com/raw/785d9e5a8985da3284c01de709b15661.png)
4. After the policy is added, it will take effect in about 30 seconds, then you can use **user1** to view and use the catalog of Presto.
