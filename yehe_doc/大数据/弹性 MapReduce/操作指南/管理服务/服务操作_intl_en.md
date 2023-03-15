## Overview
Service operation is a collection of convenient Ops and management tools provided for components, including general service restart and command-based Ops operations specific to certain components, such as HDFS NameNode active/standby switch, HDFS data rebalance, YARN ResourceManager active/standby switch, and YARN queue refresh.

>?1. YARN ResourceManager active/standby switch requires you to disable `yarn.resourcemanager.ha.automatic-failover.enabled`. If it is not displayed in the operation drop-down list on the YARN block, you need to find `yarn.resourcemanager.ha.automatic-failover.enabled` in the `yarn-site.xml` configuration file of YARN configuration management and disable it.
>2. Do not delete the queues that have already taken effect in the scheduler's configuration file when refreshing YARN queues.
>3. Ranger metadatabase change is currently supported only for MySQL databases, and only the connections of admin users will be tested.
>
## Specification Items
- **HDFS NameNode active/standby switch**: This operation switches the active NameNode to standby status and the standby NameNode to active status.
- **HDFS data rebalance**: This operation is usually required when a new DataNode is added. It will make the data evenly distributed to avoid hotspotting and make the cluster read/write load more balanced.
- **YARN ResourceManager active/standby switch**: This operation switches the active ResourceManager to the standby status and the standby ResourceManager to active status. It is allowed only when `yarn.resourcemanager.ha.automatic-failover.embedded` is disabled.
- **YARN queue refresh**: This operation enables additions or updates to `capacity-scheduler.xml` or `fair-scheduler.xml` to take effect in the ResourceManager. Do not delete queues defined in them.
- **Ranger metadatabase change**: To change the underlying database of Ranger, you need to modify the `conf/install.properties` file and then run the `setup.sh` script locally. This script can synchronize the database information to the local `ranger-admin-site.xml` configuration file without modifying the content of `ranger-admin-site.xml` in **Configuration Management**. When you modify and deliver `ranger-admin-site.xml` based on your needs, the database information will be overwritten, resulting in an exception. This operation allows you to quickly configure a Ranger metadatabase, so as to avoid exceptions caused by missing configuration items when you change the metadatabase address.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the corresponding cluster in the cluster list to go to the cluster details page.
2. On the cluster details page, select **Cluster Service** and click the target component block.
3. Taking HDFS NameNode active/standby switch as an example, in **Cluster Service**, select **HDFS** > **Operation** > **NN Failover** to perform the active/standby switch operation.
![](https://qcloudimg.tencent-cloud.cn/raw/6d94a2e49227359b32e1f2fe06b156e5.png)
