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

## Integrating YARN with Ranger
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
<td>description</td>
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
![](https://main.qcloudimg.com/raw/d0b97609dc9d5108a84582eb9fffac70.png)
4. After the policy is added, it will take effect in about 30 seconds, then you can use **user1** to submit, kill, or query jobs in the `root.default` queue of YARN.

>!When configuring Ranger YARN services and policies, make sure that there are no YARN jobs during this period; otherwise, issues about job submission permissions may occur.
