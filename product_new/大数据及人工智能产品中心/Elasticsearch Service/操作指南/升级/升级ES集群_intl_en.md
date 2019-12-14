Tencent Cloud ES offers an upgrade feature that allows you to upgrade ES and Elastic Stack. You can upgrade your cluster based on your business needs to achieve seamless business transition.
> The upgrade feature is currently made available through a whitelist. If you need to enable it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

## Supported upgrade types
ES supports the following two upgrade types.
1. Upgrade of the Elasticsearch version
<table style="width:350px !important;">
  <tr>
    <th>Source Elasticsearch Version</th>
    <th>Target Elasticsearch Version</th>
  </tr>
  <tr>
    <td>5.6.4</td>
    <td>6.4.3</td>
  </tr>
</table>
2. Upgrade of Elastic Stack
<table style="width:350px !important;">
  <tr>
    <th>Source Elastic Stack Edition</th>
    <th>Target Elastic Stack Edition</th>
  </tr>
  <tr>
    <td>Open Source Edition</td>
    <td>Basic or Platinum Edition</td>
  </tr>
	 <tr>
    <td>Basic Edition</td>
    <td>Platinum Edition</td>
  </tr>
</table>
<b>Descriptions of Elastic Stack editions:</b>
The Basic Edition and Platinum Edition integrate Elasticsearch's official Elastic Stack (formerly X-Pack) features such as security, SQL, machine learning, and monitoring. The former only comes with certain SQL features and monitoring, while the latter has all Elastic Stack features. For more information, see [Elastic Stack (X-Pack)](https://intl.cloud.tencent.com/document/product/845/30943).
 
>
 >1. You can perform only one of the two types of upgrade above at a time. Particularly, when you upgrade from version 5.6.4 to version 6.4.3, you can also choose to upgrade to the Basic Edition, which comes with the features provided by the Elasticsearch's official Elastic Stack (formerly X-Pack) such as monitoring and SQL. This practice is highly recommended.
 >2. Version 5.6.4 only supports the Open Source Edition for the time being and cannot be upgraded to the Basic or Platinum Edition.

## Notes on upgrade

### Compatibility and use of Elasticsearch 5.6.4 and 6.4.3
1. Multi-type index
  Starting from 6.x, Elasticsearch no longer supports multiple types within a single index. After you upgrade from version 5.6.4 to version 6.4.3, creating a multi-type index will cause an error. Multi-type indices previously created on version 5.6.4 will not be affected, and data can be written to them normally.
2. Accessing a cluster using curl    
  When accessing a cluster using curl, you need to add the `header -H 'Content-Type: application/json'` request.
```
	curl -XPUT http://10.0.0.2:9200/china/city/beijing -H 'Content-Type: application/json' -d'
	{
		"name":"Beijing",
		"province":"Beijing",
		"lat":39.9031324643,
		"lon":116.4010433787,
		"x":6763,
		"level.range":4,
		"level.level":1,
		"level.name":"Tier-1 city",
		"y":6381,
		"cityNo":1
	}
```  
3. Compatibility of configuration items   
 Different versions of Elasticsearch have certain incompatible configuration items, and if you have set such items, an upgrade may affect the use of your cluster. The upgrade feature of ES comes with a process to check configuration items as well as instructions for adjustment, as described below in <a href="#update_check">Upgrade check</a>.
4. For more information, see [ES 6.4.3 Release Notes](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/release-notes-6.4.3.html).

## Upgrade process
To upgrade the Elasticsearch version, you need to complete upgrade check and data backup first. The upgrade process can be started only after those two steps are successfully finished.
1. <a id="update_check">Upgrade check</a>
>  This applies only when you upgrade the Elasticsearch version.
>
 Check whether the two versions have any incompatible configuration items. If the check fails, the process will terminate, and you can view the specific check items and corresponding solutions. For more information, see [Upgrade Check](https://intl.cloud.tencent.com/document/product/845/32599). You can also choose to only perform an upgrade check before upgrade so as to see whether your cluster meets the conditions for upgrade.
2. Snapshot backup
  > This applies only when you upgrade the Elasticsearch version.
  >
 Before the upgrade, ES will perform snapshot backup of your cluster, so that you can restore it using the snapshot in case of an upgrade failure. Therefore, if this step fails, the upgrade process will also terminate. **The time it takes to complete the snapshot backup depends on the amount of data in your cluster. If automatic snapshot backup is not enabled for your cluster, and the data volume is high, it will take longer to create a snapshot for the first time.**
3. Upgrade process and cluster restart  
  For a cluster on version 6.4.3, you can upgrade Elastic Stack from the Open Source Edition to the Basic or Platinum Edition. During the upgrade, the service needs to be restarted as follows:
  - To upgrade from the Open Source Edition to the Basic Edition, your cluster must be restarted on a rolling basis, its health status must be green, and there can be no single-replica or closed indices in it. During the upgrade, the service is accessible, but its performance will be partially affected. As a result, you are recommended to perform the upgrade when the number of access requests is small.
  - To upgrade from the Basic Edition to the Platinum Edition, your cluster must have security authentication enabled and be fully restarted. During the full restart process, your cluster will be inaccessible until the upgrade is completed.

## How to upgrade a cluster
1. Log in to the [ES Console](https://console.cloud.tencent.com/es), enter the cluster details page, and click **Upgrade** in the top-right corner.
![](https://main.qcloudimg.com/raw/95246fbe2add949a6a31275074d35be5.png)
2. Choose to upgrade Elasticsearch or Elastic Stack in the upgrade dialog box.

### Upgrading the Elasticsearch version
1. Select **Upgrade the Elasticsearch version** as the **Upgrade Type** in the upgrade dialog box.
2. Select the version that you want to upgrade to in the **Elasticsearch Version** drop-down list.
  > When you upgrade from Elasticsearch 5.6.4 to 6.4.3, you can upgrade Elastic Stack from the Open Source Edition to the Basic Edition at the same time. You are recommended to select Elastic Stack **Basic Edition**, which contains features such as monitoring and SQL. If you deselect **Basic Edition**, Elasticsearch will be upgraded to version 6.4.3 in the Open Source Edition.
3. Before the upgrade, the cluster status and configuration will be checked first to determine whether your cluster can be upgraded. You can select **Upgrade Check Only**. After you click **OK**, only an upgrade check will be performed, and the upgrade command will not be executed. You can view the check result in the **Cluster Change History** on the details page.
> If you want to upgrade from Elasticsearch 5.6.4 to 6.4.3, as some configuration items at the cluster or index level are not compatible, you need to perform an **upgrade check** to determine whether your cluster can be upgraded. Incorrect configuration items that trigger alarms need to be adjusted as appropriate. For more information, see relevant documents.
4. Read and indicate your consent to the upgrade notice and click **OK** to start the upgrade (if you select **Upgrade Check Only**, an upgrade check will be started).
 ![](https://main.qcloudimg.com/raw/c2718fdcc4cd41ca1ed5fca1c1a773ca.png)
 
### Upgrading Elastic Stack
 1. Select **Upgrade Type** > **Upgrade Elastic Stack Edition** in the upgrade dialog box.
 2. Select the Elastic Stack edition that you want to upgrade to in **Elastic Stack**.
 3. Click **OK** to start the upgrade. 
  > Elastic Stack upgrade notice:  
  Currently, you can only upgrade version 6.4.3 from the Open Source Edition to the Basic Edition or Platinum Edition or from the Basic Edition to the Platinum Edition, which is not supported for version 5.6.4.    
  The upgrade process varies by edition. Please note the following:
  >- Basic Edition: To upgrade to the Basic Edition, your cluster needs to be restarted on a rolling basis, during which the service will be affected momentarily; therefore, you are recommended to perform the upgrade when the number of access requests is small. Once started, the upgrade process cannot be canceled. 
  >- Platinum Edition: To upgrade to the Platinum Edition, your cluster needs to be fully restarted and will become inaccessible. Please do so with caution. Once started, the upgrade process cannot be canceled.
  >
![](https://main.qcloudimg.com/raw/7e8741074ae7aa577a1179c7a74de812.png) 

4. After the upgrade starts, you can check the upgrade progress in the **Cluster Change History** on the cluster details page.
  ![](https://main.qcloudimg.com/raw/86f472f442922c5743aa5296020a4d8c.png)
