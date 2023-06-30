### What are the differences between a CVM assigned to a CDH and a CVM instance?

A Cloud Virtual Machine (CVM) deployed on a CDH runs in a single-tenant environment, whereas a CVM instance is a physical server resource shared by multiple tenants. The CVM on a CDH supports custom specifications, whereas a CVM instance does not. Beyond that, they provide the same features.

### How is a created CVM instance assigned to multiple selected CDHs?

If you select multiple CDHs when creating a CVM instance, it will be created on any one of these hosts.

### Why does a CVM instance occupy 2 GB more disk space than its specification?

You can customize the sizes of the system disk and data disk when creating a CVM instance. In addition to the planned disk storage, another 2 GB capacity is used to store additional configuration information.
![](https://main.qcloudimg.com/raw/7c99cc1c8ab94bd71ab6a1b8861b3011.png)

### Does CVM on a CDH support migration?
- Yes. Instances can be migrated among different dedicated hosts. For detailed directions, see [Migrating Instances Among CDHs](https://intl.cloud.tencent.com/document/product/416/41222).

### Does CVM on a CDH support configuration adjustment?

Yes. To configure the CVM on a CDH, log in to the [CVM console](https://console.cloud.tencent.com/cvm), locate the target CVM instance in the instance list, and click **More** > **Resource Adjustment** > **Adjust Configuration** in the **Operation** column. For more information, see [CVM Configuration Adjustment](https://intl.cloud.tencent.com/document/product/416/19733).

