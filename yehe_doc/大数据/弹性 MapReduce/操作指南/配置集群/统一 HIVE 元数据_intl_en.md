## Feature Overview
If you choose to deploy the optional Hive component when creating an EMR cluster, the system provides two Hive metadata storage methods for unified management of such metadata: you can store the metadata in a MetaDB instance separately purchased for the cluster or associate the metadata with an external Hive metadatabase (EMR-MetaDB or a self-built MySQL database). In the latter case, metadata will be stored in an associated database and will not be terminated when the cluster is terminated.
## Prerequisites
- Default: a MetaDB instance is automatically purchased to store Hive metadata, alongside metadata of other components. The MetaDB instance will be terminated too when the cluster is terminated. If you need to retain the metadata, please go to the TencentDB Console and save it manually in advance.
 - Hive metadata is stored together with metadata of Sqoop, Hue, Ranger, Oozie, and Presto.
 - A MetaDB instance needs to be purchased separately for the cluster as the metadatabase.
 - The MetaDB instance will be terminated when the cluster is terminated, i.e., the metadata stored in it will be deleted.
- Associate EMR-MetaDB: when a cluster is created, the system will pull an MetaDB instance available in the cloud as the Hive metadatabase, so you don't need to purchase a MetaDB instance separately, which helps reduce your storage costs. Moreover, Hive metadata will not be deleted when the cluster is terminated.
 - The ID of the available MetaDB instance is the ID of an existing MetaDB instance in the EMR cluster under the same account.
 - If one or more components among Sqoop, Hue, Ranger, Oozie, and Presto are selected, a MetaDB instance will be automatically purchased to store the metadata of such components other than Hive.
 - If the associated EMR-MetaDB instance needs to be terminated, please go to the TencentDB Console to do so. Hive metadatabases cannot be recovered once terminated.
 - Please make sure that the associated EMR-MetaDB instance is in the same network as the newly created cluster.
- Associate self-built MySQL database: you can associate with your local self-built MySQL database as Hive metadatabase, so you don't need to purchase a MetaDB instance separately, which helps reduce your storage costs. Please enter the address beginning with `jdbc:mysql://`, username, and login password correctly and make sure that the database can be connected with the cluster.
 - Please make sure that the self-built database is in the same network as the EMR cluster.
 - Please enter the username and password of the database correctly.
 - If one or more components among Sqoop, Hue, Ranger, Oozie, and Presto are selected, a MetaDB instance will be automatically purchased to store the metadata of such components other than Hive.
 - Please make sure that the Hive metadata version in the custom database is not below the Hive version in the new cluster.

## Directions
### Creating cluster
1. Log in to your [Tencent Cloud Account](https://console.cloud.tencent.com/emr) and click [Buy Now](https://buy.cloud.tencent.com/emapreduce#/) on the product overview page. Then, in **Optional Components** on the "AZ and Software Configuration" page, select the Hive component.
![](https://main.qcloudimg.com/raw/c68a9ec0f2ead0e71107f22e0a100045.png)
2. Select a Hive metadata storage method (default, EMR-MetaDB, or self-built MySQL database) as needed.
3. Configure according to the selection and the above restrictions.

### Installing Hive component subsequently
1. After you successfully create a cluster, log in to the [EMR Console](https://console.cloud.tencent.com/emr), enter the **Cluster List** page, and click the **ID/Name** of the cluster to be managed.
2. Select **Add Component** in **Cluster Service** and install the Hive component.
![](https://main.qcloudimg.com/raw/eaf98a271d734386d17945f0894f4f76.png)
3. Select a Hive metadata storage method (default, EMR-MetaDB, or self-built MySQL database) as needed.
4. Configure according to the selection and the above restrictions.
