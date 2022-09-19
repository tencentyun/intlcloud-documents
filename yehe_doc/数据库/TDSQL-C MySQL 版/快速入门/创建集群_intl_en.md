This document describes how to create a cluster in the TDSQL-C for MySQL console.

## Prerequisites
To make a purchase, you need to complete identity verification first. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
1. Log in to the [purchase page](https://buy.intl.cloud.tencent.com/cynosdb#/), complete the **Database Configuration** settings, and click **Next**.
   - **Compute Billing Mode**: Monthly subscription, pay-as-you-go, and serverless billing modes are supported.
   - **Region**: Select a region for database deployment.
   - **Source AZ**: Select an AZ for deployment. Specific AZs in the selected region are shown on the actual purchase page.
   - **Multi-AZ Deployment**: Select whether to enable multi-AZ deployment. If you enable it, the replica AZ option will appear.
   - **Replica AZ**: It is disabled by default and can be selected after multi-AZ deployment is enabled.
   - **Network**: For performance and security considerations, only VPC network is supported currently. CVM instances can communicate with TDSQL-C clusters only in the same [VPC](https://intl.cloud.tencent.com/document/product/215).
   - **Compatible Database**: MySQL 5.7 and 8.0 are supported.
   - **Compute Instance Quantity**: The instance quantity includes one read-write instance and one or more read-only instances. We recommend you select at least two instances to ensure the high availability of the cluster. After the cluster is created, you can expand its read capacity by adding read-only instances.
   - **Instance Specification**: For more information on calculating the instance specification and storage capacity, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1098/40620).
   ![](https://qcloudimg.tencent-cloud.cn/raw/a13ccab2742377785a6aab6098d3b936.png)
>?If your desired instance specification is sold out, you can click **Do you need it?**, and the pop-up window will display instances of the same specification in other AZs. If none of them meet your requirements, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>![](https://qcloudimg.tencent-cloud.cn/raw/13a9d35588668412021ce767fa38866b.png)
>
   - **Storage Billing Mode**:
     - Pay-as-you-go billing is supported, which means you don't need to specify a storage option when you buy. TDSQL-C for MySQL is billed by the actual storage used per hour.
     - Monthly subscription billing is supported, which means you need to purchase monthly-subscribed storage space now (billed in the entirety regardless of whether it is used up).
>?
>- Monthly-subscribed storage space can be purchased only after you select the monthly subscription billing mode.
>- For more information on how to select an appropriate billing mode for storage space, see [Selecting Billing Mode for Storage Space](https://intl.cloud.tencent.com/document/product/1098/47633).
   - **Auto-Renewal**: Auto-renew the device monthly upon expiration if your account has sufficient balance.
2. Complete the **Basic Info** and **Advanced Configuration** settings, select the **Validity Period**, confirm the fees, and click **Buy Now**.
   - **Basic Info**
     - **Cluster Name**: Name the cluster now or later with up to 60 letters, digits, hyphens, underscores, and dots.
     - **Admin Username**: It is **root** by default.
     - **Password**: The password can contain 8–64 characters in at least three of the following character types: uppercase letters, lowercase letters, digits, and special symbols `~!@#$%^&*_-+=|\(){}[]:;'<>,.?/`.
     - **Default Character Set**: UTF8, GBK, LATIN1, and UTF8MB4 are supported.
     - **Custom Port**: It is 3306 by default and can be customized.
   - **Advanced Configuration**
     - **Security Group**: Select or create a security group.
     - **Parameter Template**: Select or create a parameter template.
     - **Table Name Case Sensitivity**: Select **Case-Insensitive** or **Case-Sensitive**.
     - **Project**: Specify a project for the cluster to be created.
     - **Alarm Policy**: Select or create an alarm policy.
     - **Tag**: Add a tag to facilitate resource categorization and management.
     - **Terms and Conditions**: Read and indicate your consent to the terms and conditions.
![](https://qcloudimg.tencent-cloud.cn/raw/f32886901c14b28800113878e0080714.png)
>?
>- When you hover over **Configuration Fees**, the details such as computing fees and storage fees will be displayed.
>![](https://qcloudimg.tencent-cloud.cn/raw/cc18b625268f4271f10d73eb4cb10b7d.png)
>- Cluster quantity
>Pay-as-you-go: You can purchase up to ten TDSQL-C for MySQL clusters in each AZ. If you need more, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>Monthly subscription: You can purchase an unlimited number of clusters.
>- When the amount of data stored in a cluster exceeds its maximum storage space, the cluster can only read but not write data. In this case, you can choose to delete redundant data or upgrade the specification.
>
3. After the purchase is completed, you will be redirected to the cluster list. After the status of the cluster becomes **Running**, it can be used normally.

## Subsequent operations
After purchasing the TDSQL-C for MySQL cluster, you can connect to it through its private or public network address or DMC. For more information, see [Connecting to Cluster](https://intl.cloud.tencent.com/document/product/1098/40627).

