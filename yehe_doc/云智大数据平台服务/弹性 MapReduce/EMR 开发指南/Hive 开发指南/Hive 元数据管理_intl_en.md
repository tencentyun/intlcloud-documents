When you choose to deploy the Hive component, there are two storage methods for Hive metadata: you can store the metadata in a MetaDB instance separately purchased for the cluster or associate the metadata with EMR-MetaDB or a self-built MySQL database. In the latter case, metadata will be stored in an associated database and will not be terminated when the cluster is terminated.
In the former case, a MetaDB instance is automatically purchased to store Hive metadata, alongside metadata of other components. The MetaDB instance will be terminated too when the cluster is terminated. If you need to retain the metadata, please go to the TencentDB Console and save it manually in advance.

>
>1. Hive metadata is stored together with metadata of Sqoop, Hue, Ranger, Oozie, and Presto.
>2. A MetaDB instance needs to be purchased separately for the cluster as the metadatabase.
>3. The MetaDB instance will be terminated when the cluster is terminated, i.e., the metadata stored in it will be deleted.

## Associating with EMR-MetaDB for Hive Metadata Sharing
When a cluster is created, the system will pull an MetaDB instance available in the cloud as the Hive metadatabase, so you don't need to purchase a MetaDB instance separately, which helps reduce your storage costs. Moreover, Hive metadata will not be deleted when the cluster is terminated.
>
>1. The ID of the available MetaDB instance is the ID of an existing MetaDB instance in the EMR cluster under the same account.
>2. If one or more components among Sqoop, Hue, Ranger, Oozie, and Presto are selected, a MetaDB instance will be automatically purchased to store the metadata of such components other than Hive.
>3. If the associated EMR-MetaDB instance needs to be terminated, please go to the TencentDB Console to do so. Hive metadatabases cannot be recovered once terminated.
>4. Please make sure that the associated EMR-MetaDB instance is in the same network as the newly created cluster.
>

## Associating with Self-Built MySQL Database for Hive Metadata Sharing
You can associate with your local self-built MySQL database as Hive metadatabase, so you don't need to purchase a MetaDB instance separately, which helps reduce your storage costs. Please enter the address beginning with `jdbc:mysql://`, username, and login password correctly and make sure that the database can be connected with the cluster.
>
>1. Please make sure that the self-built database is in the same network as the EMR cluster.
>2. Please enter the username and password of the database correctly.
>3. If one or more components among Sqoop, Hue, Ranger, Oozie, and Presto are selected, a MetaDB instance will be automatically purchased to store the metadata of such components other than Hive.
>4. Please make sure that the Hive metadata version in the custom database is not below the Hive version in the new cluster.
>


