### What Are the Differences Between the CVM Assigned by a Dedicated Host and a Common CVM?

A Cloud Virtual Machine (CVM) deployed on a dedicated host runs in a single-tenant environment, whereas a common CVM is a physical server resource shared by multiple tenants. The CVM on a dedicated host supports specifications customization, whereas a common CVM does not. Other features of the two CVM types are the same.

### How Is a Created CVM Assigned to Multiple Selected Dedicated Hosts?

If you select multiple dedicated hosts when creating a CVM, the CVM is created on any one of these hosts.

### Why Does a CVM Occupy 2 GB More Disk Space than Its Specifications?

You can customize the sizes of the system disk and data disk when creating a CVM. In addition to planned disk storage, 2 GB of local disk storage is used to store additional configuration information. 
![qcow2](https://main.qcloudimg.com/raw/7c99cc1c8ab94bd71ab6a1b8861b3011.png)

### Is Migration Supported for CVMs on Dedicated Hosts?

Tencent Cloud supports hot migration of CVMs between different dedicated hosts of the same model and configurations. To apply for CVM migration, please [Submit a Ticket](https://console.cloud.tencent.com/workorder/category).
Currently, Tencent Cloud does not support CVM migration between dedicated host resource pools and common CVM instance resource pools.

### Is Configuration Adjustment Supported for CVMs on Dedicated Hosts?

Yes. To configure the CVM on a dedicated host, log in to the [CVM Console](https://console.cloud.tencent.com/cvm), find the target CVM instance in the instance list, and click **More** -> **Resource Adjustment** -> **Adjust Configuration** in the **Operation** column. For more information, see [CVM Configuration Adjustment](/document/product/416/19733).
