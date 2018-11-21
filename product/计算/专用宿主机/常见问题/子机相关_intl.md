###  What is the difference between a dedicated CVM instance assigned on CDH and an ordinary CVM?

A dedicated CVM instance on CDH is deployed on your CDH in a single-tenant environment, while an ordinary CVM is a physical server whose resources are shared by multiple tenants. CDH supports the customization of the specifications of the dedicated CVM instances on it, which is not possible for an ordinary CVM. In terms of other functions, CDH are the same as ordinary CVM.

### How is a dedicated CVM instance assigned during creation if multiple CDHs are selected?

If you select multiple CDHs when creating an instance, it will be randomly created on one of them.

### Why is the disk resource actually used by the dedicated CVM instance is 2 GB larger that the selected disk resource?

You can customize the size of the system disk and data disk when creating an instance. When the instance is created, 2 GB of local disk resources will be deducted in addition to the disk size you specify for storage of additional configuration information.

![qcow2](https://main.qcloudimg.com/raw/7c99cc1c8ab94bd71ab6a1b8861b3011.png)

### Can the CVM instance on CDH be migrated?

The dedicated CVM instance can be hot migrated between different CDHs of the same model and configuration. If you need this service, you can apply by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
Currently, migration of the instance on CDH between a CDH resource pool and an ordinary CVM instance resource pool is not supported.

### Does the dedicated CVM instance on CDH support configuration adjustment?

Yes. You can log in to the [CVM Console](https://console.cloud.tencent.com/cvm), select the instance on the CVM instance list page, and click **More** > **CVM Configuration** > **Adjust configuration** to make adjustments. For details, see [Adjusting Dedicated CVM Instance Configuration](/document/product/416/19733).
