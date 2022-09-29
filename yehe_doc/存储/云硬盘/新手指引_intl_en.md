## 1. Basic of CBS
- [Overview](https://intl.cloud.tencent.com/document/product/362/2345)
- [Product Strengths](https://intl.cloud.tencent.com/document/product/362/3039)
- [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636)
- [Use Cases](https://intl.cloud.tencent.com/document/product/362/3065)
- [Use Limits](https://intl.cloud.tencent.com/document/product/362/32406)

## 2. CBS Billing Modes
Tencent Cloud CBS supports the **monthly subscription** and **pay-as-you-go** billing modes. You need to understand the two billing modes to select an optimal billing solution. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).

## 3. Snapshots
Snapshots are convenient and efficient data protection methods. We recommend that you create snapshots for cloud disks before major business changes. If a business change fails, snapshots can be used to quickly restore the data. For more information, see [Snapshot Overview](https://intl.cloud.tencent.com/document/product/362/31638).


## 4. Getting Started
#### 4.1 Registration and authentication
Before using Tencent Cloud CBS, sign up for a [Tencent Cloud account](https://www.tencentcloud.com/en/account/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

#### 4.2 Creating cloud disks
After registration and identity verification, you can select a cloud disk type, capacity, billing mode, retention period, automatic renewal, and expiration or in arrears protection based on the requirements of the availability zone where your CVM is located to create cloud disks. For more information, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31647).

#### 4.3 Using cloud disks
After you create cloud disks, you need to mount separately purchased cloud disks to CVMs in the same availability zone and initialize the cloud disks. For more information, see the following documents:
- [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/39991)
- [Initializing Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645)

#### 4.4 Creating snapshots (optional)
After you create cloud disks, you can use snapshots to manually or periodically back up important business data to prevent data loss or damage caused by maloperations, attacks, viruses, or others. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) and [Scheduled Snapshot](https://intl.cloud.tencent.com/document/product/362/35238).




## 5. Console
![](https://qcloudimg.tencent-cloud.cn/raw/0911469301e8401592905c3955e067c4.png)

## 6. Overview of Console Features

| Features | Reference |
|---------|---------|
| Create cloud disks using different methods | [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744) |
| Mount a cloud disk to a CVM in the same availability zone and set automatic cloud disk mounting | [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401) |
| Initialize cloud disks based on actual requirements | [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596) |
| Expand cloud disks to add storage space | [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600) |
| Unmount cloud disks and mount them to other CVMs | [Unmounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32400) |
| Terminate or return a cloud disk | [Terminating cloud disks](https://intl.cloud.tencent.com/document/product/362/32399) |
| Create the snapshot of a cloud disk at a specific time point to save the cloud disk data at that time | [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) |
| Use a scheduled snapshot policy to flexibly back up data | [Scheduled Snapshots](https://intl.cloud.tencent.com/document/product/362/35238) |
| Delete unnecessary snapshots | [Deleting Snapshots](https://intl.cloud.tencent.com/document/product/362/5758) |
| Rollback a cloud disk by using a snapshot, so as to restore the data at the snapshot creation time | [Rolling Back by Using Snapshots](https://intl.cloud.tencent.com/document/product/362/5756) |

## 7. FAQs
#### Usage of CBS
- [What are the applicable scenarios for different types of cloud disks?](https://intl.cloud.tencent.com/document/product/362/32409)
- [How can I view cloud disk details?](https://intl.cloud.tencent.com/document/product/362/32409#.E5.A6.82.E4.BD.95.E6.9F.A5.E7.9C.8B.E4.BA.91.E7.A1.AC.E7.9B.98.E8.AF.A6.E7.BB.86.E4.BF.A1.E6.81.AF.EF.BC.9F)
- [Can one cloud disk be accessed by CVMs?](https://intl.cloud.tencent.com/document/product/362/32409#.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81.E5.A4.9A.E4.B8.AA.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8.E8.AE.BF.E9.97.AE.E5.90.8C.E4.B8.80.E5.9D.97.E4.BA.91.E7.A1.AC.E7.9B.98.EF.BC.9F)
- [Why is the separate cloud disk I created released along with my instance?](https://intl.cloud.tencent.com/document/product/362/32409#.E4.B8.BA.E4.BB.80.E4.B9.88.E6.88.91.E5.8D.95.E7.8B.AC.E5.88.9B.E5.BB.BA.E7.9A.84.E4.BA.91.E7.A1.AC.E7.9B.98.E5.92.8C.E6.88.91.E7.9A.84.E5.AE.9E.E4.BE.8B.E4.B8.80.E8.B5.B7.E9.87.8A.E6.94.BE.E4.BA.86.EF.BC.9F)
- [Can I change the type of the cloud disk after purchase?](https://intl.cloud.tencent.com/document/product/362/32409#.E5.9C.A8.E6.88.90.E5.8A.9F.E8.B4.AD.E4.B9.B0.E5.90.8E.EF.BC.8C.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81.E6.9B.B4.E6.8D.A2.E4.BA.91.E7.A1.AC.E7.9B.98.E7.9A.84.E7.B1.BB.E5.9E.8B.EF.BC.9F)
- [Can I partition my system disk?](https://intl.cloud.tencent.com/document/product/362/32409#.E7.B3.BB.E7.BB.9F.E7.9B.98.E8.83.BD.E5.90.A6.E8.BF.9B.E8.A1.8C.E5.88.86.E5.8C.BA.E6.93.8D.E4.BD.9C.EF.BC.9F)


#### Snapshot FAQs
- [What are the differences between snapshots and images?](https://intl.cloud.tencent.com/document/product/362/17820)
- [Why can't I delete a snapshot?](https://intl.cloud.tencent.com/document/product/362/17820)
- [Do I need to shut down the CVM to roll back using a snapshot?](https://intl.cloud.tencent.com/document/product/362/17820)
- [When I terminate a cloud disk, will the associated snapshots be deleted as well?](https://intl.cloud.tencent.com/document/product/362/17820)


## 8. Feedback and Suggestion
If you have any doubts or suggestions when using Tencent Cloud CBS products and services, you can submit your feedback through the following channels. Dedicated personnel will contact you to solve your problems.

- If you have any questions regarding the product documentation, such as links, content, or APIs, click **Send Feedback** on the right of the document page.
- If you encounter any problems when using the product, contact [online support](https://intl.cloud.tencent.com/contact-sales) for assistance.



