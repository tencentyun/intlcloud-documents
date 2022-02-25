## Feature Overview
When there is too much data in a cluster instance, you can store some cold data to a COS bucket and hot data to a Cloud Data Warehouse local disk to save storage costs without compromising the data query performance of Cloud Data Warehouse.

## Terms
- Hot data: frequently accessed or recently created data, which is stored on the cloud or local disk selected at the time of cluster creation for efficient data access.
- Cold data: less frequently accessed data, which can be stored on a cold data disk to save storage costs and meet data access needs.

## Directions
1. Log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch). When creating a cluster, enable cold backup storage on the hot-cold tiered storage page and select a previously created COS bucket (you need to purchase one in the same region).
![](https://qcloudimg.tencent-cloud.cn/raw/3cd14d243d1057c55580ecaf30f70508.png)
According to the cluster policy, when the used storage space reaches 90%, a cold data tiering mechanism will be automatically triggered by default, where cold data configured with a tiering table will be transferred from the local disk to the configured COS bucket in order of data storage until the used space drops below the threshold. You can configure the tiering table with the following command as needed:
```
ALTER TABLE xx MODIFY SETTINGS storage_policy = 'jbod_ha'
```
2. To enable data tiering after a cluster is created, select **Operation > More > Configure Hot-Cold Tiered Storage** in the cluster list.
 ![](https://qcloudimg.tencent-cloud.cn/raw/38196520c02abace07533cb3c8218e0a.png)
3. After tiering is configured, view or adjust the hot data tiering coefficient on the cluster details page. 
 ![](https://qcloudimg.tencent-cloud.cn/raw/c75b8e2161c2eb6e632fd4d8eba124e0.png)
4. If tiering is triggered, you can log in to the [COS console](https://console.cloud.tencent.com/cos5/bucket) and go to the COS bucket details page to query cold data files. 

## Notes
1. Tiered storage is available for v20.1 and later.
2. Due to network restraints, you need to have a COS bucket in the same region as the cluster to perform tiered storage.
3. During tiering, the cluster will be restarted and become inaccessible.
4. After tiering is enabled, a cluster will store newly written data to a hot data disk, with a default data space threshold of 90%, which you can customize.



