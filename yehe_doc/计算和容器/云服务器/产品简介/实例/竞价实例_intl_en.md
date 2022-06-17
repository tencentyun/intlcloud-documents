## What is a spot instance?
Spot instances are a new mode of CVM instances that feature a discounted price and a system interruption mechanism, which means that you can purchase a spot instance at a discounted price, but the system may automatically repossess it. When you use a spot instance, the operations are almost the same as what you do with a pay-as-you-go CVM instance, including console operations, remote login, service deployment, and association with a VPC.

- Reference: [FAQ > About Instance > Spot Instances](https://intl.cloud.tencent.com/document/product/213/17817)
- Reference: [Spot Instances](https://intl.cloud.tencent.com/document/product/213/17926)

## Special policies for the current stage
- **Fixed discount**: All spot instances are available at a fixed discount, which is 80% off the price of pay-as-you-go instances of the same specification. The discounts for a few types of instances may be slightly adjusted.
- **System interruption due to insufficient supply**: Currently, spot instances will not be interrupted due to the price reason, but may be interrupted if spot instances are in short supply. If the supply is insufficient, Tencent Cloud will randomly repossess allocated spot instances without retaining the instance data.
- **Available in almost all regions**: Spot instances are available in almost all Tencent Cloud regions. The instance types supported by spot instances are the same as those supported by pay-as-you-go instances. For the latest regions and instance types supported, see [Spot Instances](https://intl.cloud.tencent.com/document/product/213/17817#.E5.BD.93.E5.89.8D.E7.AB.9E.E4.BB.B7.E5.AE.9E.E4.BE.8B.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E5.9C.B0.E5.9F.9F.E5.92.8C.E5.AE.9E.E4.BE.8B.E7.B1.BB.E5.9E.8B.E5.8F.8A.E8.A7.84.E6.A0.BC.EF.BC.9F).

## Features
### 1. Cost-effectiveness
![](https://main.qcloudimg.com/raw/8179ef6629ac0a0b4b9c3c9cd6f80ffa.png)
Spot instances are sold at a discount of up to 90% off the prices of pay-as-you-go instances.

- **Discount range**: Spot instances are sold at a discount of up to 90% off the price of pay-as-you-go instances of the same specification.
- **Exclusions**: The discount only applies to CVM CPU and memory. Other CVM-related billing items including system disks, data disks, bandwidth, and paid images are not eligible for the discount.
- **Price fluctuations**: The discount is stable for a period of time. However, if there are bulk purchases in an availability zone, the price may fluctuate. Currently, the discount is fixed at 80% off.

### 2. System interruption mechanism
![](https://main.qcloudimg.com/raw/a4db964d52400b9a00d3c7e96c0b833d.png)
Unlike pay-as-you-go instances which can only be released by users, spot instances may be interrupted by the system due to price or resource availability reasons.
![](https://main.qcloudimg.com/raw/824a585f8dfeb1914f4d72ea1eafdb6c.png)

- **Price**: If the market price is higher than your highest bid, your spot instances will be repossessed. However, at the current stage, the market price will be fixed.
- **Resource Availability**: If spot instances are in short supply, Tencent Cloud will repossess spot instances based on the shortage. Once the supply gets sufficient, you can apply for spot instances again.

## Non-applicable scenarios
As spot instances may be interrupted, their lifecycle is not under your control. Therefore, it is not recommended to run services with high stability requirement on a spot instance. For example:
- Database services
- Online and website services without load balancers
- Core control nodes in a distributed architecture
- Prolonged big data computing job lasting over 10 hours

## Applicable scenarios and industries
### Use cases
- Big data computing
- Online and website services with load balancers
- Web crawler service
- Other computing scenarios with fine granularity or support for checkpoint restart

### Applicable industries
- Gene sequencing and analysis
- Drug crystal form analysis
- Video transcoding and rendering
- Financial and transaction data analysis
- Image and multimedia processing
- Science calculations, such as in geography and hydromechanics

## Restrictions
- **Quota limit**: Currently, the spot instances for each account per availability zone can contain up to 50 vCPU cores in total. To increase the quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- **Operation restriction 1**: You cannot upgrade and degrade the configuration of spot instances.
- **Operation restriction 2**: You cannot witch the billing mode of spot instances to monthly subscription.
- **Operation restriction 3**: **No charges when shut down** is not supported for spot instances.
- **Operation restriction 4**: System reinstallation is not supported for spot instances.
- **Operation restriction 5**: You cannot expand the system disks and data disks of spot instances.

## Best Practices
### 1. Splitting tasks
- Split a prolonged task into fine-grained subtasks for lower possibility of interruption.
- Use a big data suite such as EMR that comes with a splitting mechanism.

### 2. Using load balancers to ensure the stability of online and website services
- Use load balancers, such as CLB, at the access layer.
- Use a combination of some pay-as-you-go instances and many spot instances for backend resources.
- Monitor the interruptions of spot instances and remove instances that are about to be interrupted from the CLB.

### 3. Using a computing scheduling mode that supports checkpoint restart
- Store intermediate computing results on permanent storage products such as COS, CFS, and NAS.
- Be aware of the instance metadata to monitor which instances are about to be interrupted and save the computing results within the retention period of 2 minutes.
- Resume the last computing when a spot instance is started again.
