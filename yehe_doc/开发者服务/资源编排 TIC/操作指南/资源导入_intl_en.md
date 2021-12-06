## Introduction

You can use the resource import feature of Tencent Infrastructure as Code (TIC) to import Tencent Cloud resources created using the console or Cloud APIs into a TIC stack for unified orchestration without having to delete or re-create Tencent Cloud resources.

>?You can only import existing Tencent Cloud resources into a new stack, not into an existing stack.

The following table lists the Tencent Cloud services that can be imported into TIC.

| Tencent Cloud Service | Resource Type                                                     | Remarks                  |
| ------ | ------------------------------------------------------------ | --------------------- |
| CDN    | [tencentcloud_cdn_domain](https://console.cloud.tencent.com/tic/resource-types/detail/1045) | HTTPS certificates cannot be imported |


## Directions

### Importing resources

1. Log in to the [TIC console](https://console.cloud.tencent.com/tic). In the left sidebar, choose **Orchestration** -> **Stacks** to go to the **Stacks** page.
2. On the [**Stacks**](https://console.cloud.tencent.com/tic/stacks) page, click **New stack**.
3. In the **Select Mode** step, select a region, specify a template for importing resources, and select the resources to be imported.
![image-20200710154557033](https://main.qcloudimg.com/raw/ec82cc68cfb8f353d36a29f1c7e1bc9f.png)
4. Click **Next** to import the selected resources.
5. The more resources you select to import, the longer it will take to import them. After the resources are imported, click **Import Completed** to go to the **Configure the Stack** step.
![](https://main.qcloudimg.com/raw/89cf5c05edef27aaeb93ba42ed4968e5.png)

### Configuring the stack

1. After the resources are imported, the stack configurations will be generated automatically.
	 ![](https://main.qcloudimg.com/raw/dba3ee9b9394fdd3e6196b0eda65b996.png)
2. After you confirm that the stack configurations are correct, click **Next** to go to the **Plan** step.
   >!To ensure that the import operation does not affect resource configurations on the live network, follow these rules when you confirm the stack configurations:
   > 1. Do not modify parameters of the `ForceNew` type. For example, in the configuration parameters of CDN `tencentcloud_cdn_domain`, the `domain` and `service_type` parameters are of the `ForceNew` type. If these 2 parameters are modified, resources on the live network will be destroyed and re-created, which may affect businesses on the live network.
   > 2. You must manually configure parameters that cannot be automatically imported. For example, to import domain name certificates of CDN into TIC, manually configure the certificates and add them into the stack configuration file for resource orchestration and management.
   > 3. If you have any questions about the generated configuration parameters, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact the TIC team before you perform subsequent operations.
3. Check whether the plan results meet your requirements, especially whether any resources have been added, changed, or destroyed. If the plan results meet your requirements, click **Next**.
   ![image-20200710154824278](https://main.qcloudimg.com/raw/33533236d7d1e1d06ccf9aa447d56bfc.png)
   >?TIC supports importing existing resources that have been created on Tencent Cloud. Normally, no resource is added, changed, or destroyed in the import process. If the number of added, changed, or destroyed resources is not 0 in the plan results, do not perform subsequent operations. Instead, check whether you have modified any parameters of the `ForceNew` type. If you have any questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact the TIC team before you perform subsequent operations.
4. Set the stack name and the description and click **Confirm** to create the stack.
![](https://main.qcloudimg.com/raw/7824466b2c40aa13d996a60d95bf6f7d.png)

### Viewing the stack status


1. Go to the [**Stacks**](https://console.cloud.tencent.com/tic/stacks) page. Click the name of the created stack to go to the stack details page.
2. Click the **Events** tab and view the stack status. **APPLY_IN_PROGRESS** indicates that the resource information is being synchronized.
![image-20200710155056811](https://main.qcloudimg.com/raw/7676c44b8f3055e3ec59773adc313ff7.png)
3. Wait 10 seconds or more for the resource information synchronization to complete. Then, the stack status will change to **APPLY_COMPLETED**.
![image-20200710155906888](https://main.qcloudimg.com/raw/49a7e5b553f49ed0d7c0d40c69c0739a.png)
4. Verify that the resources have been imported into the created stack. On the **Resources** tab of the **Stacks** page, you can view the imported Tencent Cloud resources. To manage these resources, you only need to modify the configurations of the stack.
![image-20200710155952490](https://main.qcloudimg.com/raw/60414c7cf720def527bd2112d4dafff7.png)
