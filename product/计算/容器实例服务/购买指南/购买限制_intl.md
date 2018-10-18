## Preparations Before Purchase
You need to sign up for a Tencent Cloud account and complete identity verification before purchasing a container instance. For more information, see [Sign up for Tencent Cloud](https://cloud.tencent.com/document/product/378/9603).

 ## Available Region
Container instances are available in "Guangzhou" region. More regions are coming soon.

## Instance Quota
| Resource | Limit | Notes |
| ---------------------------------- | ---------- | ---------------------------- |
| Maximum number of instances supported in a region | 30 | Including those that are being created and running |

If the number of instances you need to purchase exceeds the quota limit in the corresponding region, you can submit an application for increasing the quota. Tencent Cloud will assess your actual needs and increase your quota as appropriate.

#### How to apply for quota increase:
You need to [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&source=0). Select **Apply for increasing CIS quota**, enter the target region, the target quota, the application reason and problem description based on the actual situation, and your valid phone number, and then click **Submit**.
>**Note:**
> - To apply for a quota in one availability zone or apply for the same quota in multiple availability zones, you can just select the availability zone(s) and enter the target quota.
> - You need to apply for different quotas in multiple availability zones separately. 

## Supported Configuration
During the internal trial:
- The maximum configuration supported for a CIS instance is 6 cores and 14 GB.
- The number of containers in a CIS instance is limited to 5.

The following configuration is supported for a container in a CIS instance:

| CPU/core | Memory/GB |
| ------ | ------------------------------------ |
| 0.25   | 0.25, 0.5, 0.75, 1                   |
| 0.5    | 0.5, 1, 1.5, 2                       |
| 1      | 1, 2, 3, 4                           |
| 2      | 2, 3, 4, 5, 6, 7, 8                  |
| 4      | 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14 |

