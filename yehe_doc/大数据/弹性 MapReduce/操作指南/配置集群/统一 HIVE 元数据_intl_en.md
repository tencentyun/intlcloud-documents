## Overview
When you choose to deploy the Hive component, the system provides two storage methods for Hive metadata: you can store the metadata in a MetaDB instance separately purchased for the cluster (default method) or associate the metadata with EMR-MetaDB or a self-built MySQL database. In the latter case, metadata will be stored in the associated database and will not be deleted when the cluster is terminated. This way, Hive metadata can be managed in a unified manner.
## Prerequisites
- **Cluster default**: A MetaDB instance is automatically purchased to store Hive metadata, alongside metadata of other components. The MetaDB instance will also be terminated when the cluster is terminated. If you need to retain the metadata, please go to the TencentDB console and save it manually in advance.
 - Hive metadata is stored together with the metadata of Hue, Ranger, Oozie, Presto, Druid, and Superset.
 - A MetaDB instance needs to be purchased separately for the cluster as the metadatabase.
 - The MetaDB instance will be terminated when the cluster is terminated, i.e., the metadata stored in it will be deleted.
- **Associate EMR-MetaDB**: When a cluster is created, the system will pull a MetaDB instance available in the cloud as the Hive metadatabase, so you don't need to purchase a MetaDB instance separately, which helps reduce your storage costs. Moreover, Hive metadata will not be deleted when the cluster is terminated.
 - The ID of the available MetaDB instance is the ID of an existing MetaDB instance in the EMR cluster under the same account.
 - If one or more components among Hue, Ranger, Oozie, Druid, and Superset are selected, a MetaDB instance will be automatically purchased to store the metadata of such components other than Hive.
 - To terminate the associated EMR-MetaDB instance, you need to go to the TencentDB console to do so. Hive metadatabases cannot be recovered once terminated.
 - Make sure that the associated EMR-MetaDB instance is in the same network as the newly created cluster.
- **Associate self-built MySQL**: You can associate with your local self-built MySQL database to store Hive metadata, so you don't need to purchase a MetaDB instance separately, which helps reduce your storage costs. Please enter the address beginning with "jdbc:mysql://", username, and login password of the database correctly and make sure that the database can be connected with the cluster.
 - Make sure that the self-built database is in the same network as the EMR cluster.
 - Enter the username and password of the database correctly. 
 - If one or more components among Hue, Ranger, Oozie, Druid, and Superset are selected, a MetaDB instance will be automatically purchased to store the metadata of such components other than Hive.
 - Make sure that the Hive metadata version in the self-built database is not below the Hive version in the new cluster.

## Directions
### Installing Hive when creating a cluster
1. Log in with your [Tencent Cloud account](https://console.cloud.tencent.com/emr) and click [Buy Now](https://buy.cloud.tencent.com/emr). Select the Hive component in **Components to Deploy** on the **Software Configuration** page.
![](https://main.qcloudimg.com/raw/c68a9ec0f2ead0e71107f22e0a100045.png)
2. Select one of the following values for **Hive metadatabase** as needed: **Cluster default**, **Associate EMR-MetaDB**, and **Associate self-built MySQL**.
3. Restrictions vary depending on the selected value. For more information, see **Prerequisites**.

### Installing Hive after a cluster is created
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click **Cluster List** on the left sidebar. On the page that appears, click the **ID/Name** of the target cluster.
2. Choose **Cluster Service** > **Add Component** and select the Hive component.
![](https://main.qcloudimg.com/raw/eaf98a271d734386d17945f0894f4f76.png)
3. Select one of the following values for **Hive metadatabase** as needed: **Cluster default**, **Associate EMR-MetaDB**, and **Associate self-built MySQL**.
4. Restrictions vary depending on the selected value. For more information, see **Prerequisites**.
