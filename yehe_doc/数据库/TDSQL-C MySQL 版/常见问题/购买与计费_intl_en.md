
### How do I reduce the costs of TDSQL-C for MySQL?
TDSQL-C for MySQL reduces TCO through pooling, features minimalist software optimizations, and supports common networks and hardware devices to release the hardware dividend. It has an elastic scaling feature and a built-in high availability architecture, where fast scaling capabilities greatly reduce the wastes of computing and storage resources. In addition, it is more cost-effective than traditional commercial databases with the same high performance and reliability.

TDSQL-C for MySQL offers flexible billing modes and specification adjustment capabilities, so you can scale cluster resources largely based on your business conditions and reasonably query the approximate costs of required resources before deploying your business. The computing-storage separation architecture further allows you to adjust the specification on demand with no need to select a certain combination. Instead of upgrading or downgrading both the compute node and storage space specifications within the fixed range, you can easily adjust the compute node and storage space separately as needed. This helps you implement fine-grained cost management to the greatest extent.

### What are the billable items of TDSQL-C for MySQL?
The billable items of TDSQL-C for MySQL include compute node, storage space, backup (free of charge currently), and database audit (optional). For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/1098/40620).

### What types of files will use the storage space?
Such files include data files, index files, log files (redo, undo, slow, and error logs), temporary files, and a small number of system files. For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/1098/40620).

### What billing modes does TDSQL-C for MySQL support?
TDSQL-C for MySQL adopts a computing-storage separation architecture, so the compute nodes and storage space can be billed separately in different billing modes:
- The billing modes of compute nodes include monthly subscription, pay-as-you-go, and serverless.
- The billing modes of the storage space include monthly subscription (available only when the billing mode of compute nodes is monthly subscription) and pay-as-you-go.

### How do I choose an appropriate billing mode?
- If your business peak traffic fluctuates greatly, you only use the database infrequently in the development and test environments, or you use SaaS in scenarios such as website building for small and medium-sized enterprises, we recommend you choose the serverless billing mode. In this mode, the database can automatically start, stop, and scale based on the business load in an imperceptible manner without causing disconnections, and the service is billed by the actual computing and storage resource usage.
- If your business has a stable traffic and runs for a long term, we recommend that you choose the monthly subscription billing mode. In this mode, the longer the purchase period, the higher the discount as displayed on the purchase page.
- If your business often fluctuates greatly and instantaneously, we recommend that you choose the pay-as-you-go billing mode. In this mode, instances can be released immediately after use to reduce the costs.
- If you need a large storage space, you can choose the monthly subscription billing mode. In this mode, the storage space is billed in a tiered manner. If the used storage space exceeds 3,000 GB, you can enjoy a even lower unit price.
For more information on storage space pricing, see [Selecting Billing Mode for Storage Space](https://www.tencentcloud.com/document/product/1098/47633).

### Which billing modes does a TDSQL-C for MySQL read-only instance support?
The computing and storage billing modes of a TDSQL-C for MySQL read-only instance must be the same as those of its source instance.
- If both the computing and storage space billing modes of the source instance are monthly subscription, you can only add read-only instances with the monthly subscription billing mode for both computing and storage space.
- If the computing and storage space billing modes of the source instance are monthly subscription and pay-as-you-go respectively, you can only add read-only instances with the monthly subscription billing mode for computing and pay-as-you-go billing mode for storage space.
- If both the computing and storage space billing modes of the source instance are pay-as-you-go, you can only add read-only instances with the pay-as-you-go billing mode for both computing and storage space.
- In serverless billing mode, you cannot add read-only instances.

### Does TDSQL-C for MySQL charge for the backup space?
The backup storage space of TDSQL-C for MySQL is free of charge currently and will be billed on a pay-as-you-go basis as needed in the future. Therefore, plan your backup storage files reasonably.

### Will my pay-as-you-go cluster be eliminated immediately when my account balance becomes negative?
No.
The moment your account balance becomes negative:
- You can continue to use your TDSQL-C for MySQL cluster in 24 hours. We will continue to bill you for this period.
- After 24 hours, your TDSQL-C for MySQL cluster will be automatically isolated and moved into the recycle bin, and the billing will stop.
- If you top up your account within 3 days after the isolation to a positive balance, the billing will continue, and the cluster will be automatically recovered for normal use.
- If your account balance remains negative after 3 days, the isolated cluster will be deactivated and put into the repossession queue. >- After it is repossessed, all data in it will be cleared and cannot be recovered.
![](https://main.qcloudimg.com/raw/2a4084a3304cd60ede9a2675feda9e97.png)

### How do I purchase TDSQL-C for MySQL?
You can purchase TDSQL-C for MySQL in the following two ways:
- Create a cluster in the [console](https://console.cloud.tencent.com/cynosdb).
You can click **Create** in the **Cluster List** to quickly purchase a cluster. This method is suitable for existing TencentDB users.
- Directly purchase the service on the [purchase page](https://buy.cloud.tencent.com/cynosdb?regionId=1#/).
You can purchase a cluster on the purchase page. This method is suitable for new TencentDB users.

Before using either method, you must register a Tencent Cloud account and complete identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
- To complete identity verification:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

You need to set the database configuration, basic information, and advanced configuration in both purchase methods. For more information on the configuration, see [Purchase Methods](https://www.tencentcloud.com/document/product/1098/46013).

### How do I change the billing mode of a pay-as-you-go cluster to monthly subscription?
TDSQL-C for MySQL implements this change by generating a renewal order. You can select **More** > **Pay-as-You-Go to Monthly Subscription** in the **Operation** column in the [Cluster List](https://console.cloud.tencent.com/cynosdb) for change.
Rest assured that access to your business will not be affected during the change from pay-as-you-go billing to monthly subscription billing. However, a monthly subscribed cluster cannot be changed back to a pay-as-you-go cluster.

### How do I change the billing mode of a pay-as-you-go cluster to serverless?
TDSQL-C for MySQL converts the cluster type on the backend to change the billing mode from pay-as-you-go to serverless. After conversion, the billing mode is a postpaid billing mode, where you can set the maximum and minimum computing power values as needed first and will be charged based on the actual usage of computing and storage resources upon settlement.
During the change from pay-as-you-go billing to serverless billing, the database can be accessed normally but will experience a momentary disconnection at the time point of change. Therefore, we recommend you configure an automatic reconnection feature for your application. However, a serverless cluster cannot be changed back to a pay-as-you-go cluster. For detailed directions, see [Change from Pay-as-You-Go to Serverless Billing](https://www.tencentcloud.com/document/product/1098/40624).

### How do I renew a TDSQL-C for MySQL cluster?
You can manually renew or set automatic renewal for one or multiple TDSQL-C for MySQL clusters in the console. If you have many resources under your account, you can configure renewal settings in the [Renewal Management Center](https://console.cloud.tencent.com/account/renewal), such as batch cluster renewal, automatic renewal, and unified expiration date.

### How do I delete a cluster?
If you are sure that you no longer need a cluster, you can find it in the **Cluster List** and select **More** > **Delete** in the **Operation** column to delete it.
>!  
>- After a cluster is deleted, all instances (including read-write and read-only instances) in it will also be automatically deleted.
>- After a pay-as-you-go cluster is deleted, its billing will stop automatically.
>- If a monthly subscribed cluster is deleted before it expires, the fees of all instances in it will be calculated again by the usage duration at the pay-as-you-go price, and your original payment will be refunded after fees incurred are deducted from it.

### How do I restore an instance?
You can restore accidentally deleted, expired, or suspended instances from the [recycle bin](https://console.cloud.tencent.com/cynosdb/mysql/recycle) before they are terminated.

>!
> - Read-only instances can be restored only after the read-write instance is restored.
> - You can only restore an instance before it is terminated.
> - If you click **Terminate** in the **Operation** column, the instance will be eliminated immediately and cannot be restored. Therefore, proceed with caution.

