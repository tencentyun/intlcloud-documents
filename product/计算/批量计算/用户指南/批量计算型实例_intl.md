## Summary

Batch-type instance is a resource pools built by Tencent Cloud for large-scale batch computing scenarios. It is designed for users with high requirements for cost performance and scale. Currently, it is during trials by selected corporate users. (Relevant information can be provided when applying for inclusion in the Batch Console whitelist)

## Instance Benefits
* High cost performance: Starting from CNY0.09/CPU core/hour after discount
* Elasticity: Billed in a postpaid manner for easy scaling
* Large scale: Up to 10,000 concurrent vCPUs supported

## Is It Different from Other CVM Instance Types?
No. After purchase, it is the same as other CVM instance types such as standard-type and compute-type and can be managed in the CVM Console. However, it is currently only available to corporate users with large-scale batch computing needs.

## Instance Configuration

| Model | Specifications | vCPU | Memory | Price |
|---------|---------|---------|---------|---------|
| Universal Batch BS1 | BS1.LARGE8 | 4 cores | 8 GB | Starting from CNY0.36/hour |
| Universal Batch BS1 | BS1.LARGE24 | 12 cores | 24 GB | Starting from CNY1.08/hour |
| Universal Batch BS1 | BS1.LARGE48 | 24 cores | 48 GB | Starting from CNY2.16/hour |

**Currently only available in Guangzhou Zone 2 and Shanghai Zone 1**

## Purchase Guide
### 1. Open Batch - Compute Environment Console

![](https://main.qcloudimg.com/raw/9c05439bd29829925fde120b402ec167)
[Batch - Compute Environment Console >>](https://console.cloud.tencent.com/batch/env). Please select Shanghai or Guangzhou region. If the system prompts for denied access, please click the application link and Tencent Cloud technical support team will approve and activate the service for you as soon as possible.

### 2. Select the Universal Batch BS1 instance
 ![](https://main.qcloudimg.com/raw/ded6fd4bf772292adf12d0f6cf82d8cd)

### 3. Enter the image ID and the number of instances to be created
![](https://main.qcloudimg.com/raw/967bcbeb35b3ea143dcbcfad7dac9c5d)

* Image ID: An image that supports Cloud-Init is required. Common public images can be used. For details, see [How to Make an Image for Batch >>](/document/product/599/16917)
* Desired quantity: You can enter the number of instances you need or keep it as 0 and modify later (subject to the CVM instance and resource quotas in corresponding availability zone, and the entered number may not be fully satisfied)

### 4. Set other configuration items of the instance (optional)
![](https://main.qcloudimg.com/raw/3cb69c184a3877d12e2f480981a4dd0b)

* Name: Enter as needed
* CVM detailed configuration: Disk, bandwidth, password and other options are configured here
* Remote storage mapping: Remote storage such as CFS, COS and NFS can be mounted to a local directory. If not needed, you can click Delete to remove it

### 5. View the created instance in the instance list
![](https://main.qcloudimg.com/raw/32cff4046ba48ac19d233190e6732610)

* You can also view in the [CVM Console](https://console.cloud.tencent.com/cvm/index)
* **If you need to terminate an instance, you can do so in the Batch Console**

### 6. Change quantity and terminate
![](https://main.qcloudimg.com/raw/208ed5a0fc0e4ac0960ad3268ffc94d5)

* You can adjust the desired quantity (subject to instance and resource quotas too) which can be down to 0


