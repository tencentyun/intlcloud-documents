## Billable Items
The billing of SCF contains the following four parts. The fees are accurate to two decimal places in USD for Tencent Cloud International.

### Pay-as-you-go billable items
The basic fees of SCF are billed based on the actual usage.

| Billable Item | Description |
| :----------------------------------------------------------- | :--------------- |
| Resource usage fee | Resource usage is calculated in GBs by multiplying the configured function memory size by the function execution duration. |
| Invocation fee | Each function triggering and execution is calculated as an invocation. HTTP-triggered functions are billed by the **number of invocations** in the same way. |
| Public network outbound traffic fee | The outbound traffic consumed when the function code accesses the public network is counted as the public network outbound traffic in GB. |
| Idle provisioned concurrency fee | The number of idle instances is calculated by subtracting the number of actually running concurrent instances from the number of launched provisioned instances, and the idle resource usage is calculated in GBs by multiplying the number of idle instances by the configured memory size. |
| Basic package fee | A basic package tier is automatically granted, and the fee is automatically deducted on a monthly basis (0.06 USD/day). This fee will be charged in the following cases: 1) You are a three-month new user. 2) You have valid subscription packages. 3) No resource usage, function invocation, and outbound traffic were incurred in the last month. |
| HTTP-triggered function response traffic fee | It is counted only for HTTP-triggered functions configured with default triggers. For more information, see [HTTP-Triggered Function Billing](https://intl.cloud.tencent.com/document/product/583/45902). |


For the unit price of each billable item, see [Product Pricing](https://intl.cloud.tencent.com/document/product/583/12281). 

>? For HTTP-triggered functions using the default trigger, HTTP-triggered function response traffic will be additionally generated, which is not included in the free tier. For more information, see [HTTP-Triggered Function Billing](https://intl.cloud.tencent.com/document/product/583/45902).
>

### Prepaid billable items
After a subscription package is purchased, it can be used to deduct the above **pay-as-you-go billable items**.

| Billable Item | Description |
| :--------------------- | :--------------- |
| [Subscription package](https://www.tencentcloud.com/document/product/583/52230) | It is purchased in the form of monthly subscription and can be used to deduct the fees of **function resource usage**, **function invocation**, **public network outbound traffic**, **function concurrency quota**, and **function burst** in the **specified region/namespace**. The resources in the subscription package will be deducted based on the expiration time. If the actual usage is less than or equal to the package quota, no additional function execution fees will be incurred. Excessive usage will be automatically billed in a pay-as-you-go manner. |


### Fees of other products
Other paid products may be used when you use the SCF service as listed below:

| Billable Item of Associated Service | Description |
| :--------------------- | :--------------- |
| CLS fee | The log query function of SCF is provided by CLS. Operation logs are shipped to CLS by default. For more details, see [Log Shipping Configuration](https://intl.cloud.tencent.com/document/product/583/39778). Starting September 5, 2022, CLS offers a limited [free tier](https://intl.cloud.tencent.com/document/product/614/37889) to new users within three months of activation, after which they will be charged a volume-based log service fee. See [Log Service Pricing](https://intl.cloud.tencent.com/document/product/614/37510). |
| API Gateway, COS, CKafka, and other fees | If you use other products such as CMQ, CKafka, API Gateway, and COS when using SCF, fees will be calculated according to the billing rules of the actually used products. |


## Resource Usage Fee

**Resource usage fees** = **(resource usage - free tier)** * **resource usage unit price**

### Resource Usage (GBs)

**Resource usage** = **memory configured for function** * **execution duration**

Memory configured for the function is calculated in GB, and charged duration is calculated in seconds (converted from milliseconds). So resource usage is calculated in **GBs** (GB-second).

For example, if a function with 256 MB memory configured is executed for 1760 ms, then the billable duration is 1760 ms, and the resource usage of this function execution will be (256/1024) * (1760/1000) = 0.44 GBs.

Resources used in each run are calculated on an hourly basis.

>!
>- SCF resource usage is calculated by multiplying the configured function memory size by the actually triggered execution duration of the function. Compared with the billing method of 100-ms upward aggregation, this billing method calculates lower overall resource usage and incurs fewer fees. For more information, see [Billing Example](https://intl.cloud.tencent.com/document/product/583/12285).
>- Due to issues such as the uncertainty of computing resources where SCF runs, specific actions in the code, and relevant network communications, the execution duration of the same function code may vary slightly when the code is triggered at different times.

## Fee for Number of Calls

**Invocation volume fees = (number of function invocations - free tier)** * **invocation unit price**

Each function triggering and execution will be calculated as an invocation and aggregated in each hour as the hourly invocation volume. Fees will be charged per invocation.


## Fee for Public Network Outbound Traffic

**Public network outbound traffic fees = public outbound traffic** * **traffic unit price**

Outbound traffic will be generated when resources are accessed over the public network in a function, such as uploading a file to an external storage space:

- When the code writes files to the storage space provided on the public network, outbound traffic will be generated by sending files. When the code reads data or files from the storage space provided on the public network, outbound traffic will be generated only by sending requests but not by reading or downloading files.
- If a function is configured with a VPC and writes data to a database in the VPC in its code, no outbound traffic will be generated by data writes.
- For a function that uses an API Gateway trigger, **no function outbound traffic will be generated** by the data returned after the function is executed. The traffic generated by the data returned by API Gateway to the client will be calculated as the outbound traffic of and billed by API Gateway. For the billing rules of API Gateway traffic, see [Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/628/11771).



## Idle Provisioned Concurrency Fees

**Idle provisioned concurrency fees = number of idle instances** * **configured memory size** * **idle duration** * **idle provisioned concurrency unit price**

- **Number of idle instances**: SCF counts the maximum concurrency of a version at a 10-second granularity. The number of idle instances is calculated by subtracting the maximum concurrency from the number of currently started provisioned instances. The calculation formula is as follows: number of idle instances = max(number of started provisioned instances - number of concurrent instances, 0).
- **Configured memory size**: The memory size configured for the provisioned concurrency of the function.
- **Idle duration**: The idle duration of the provisioned concurrency.
- **Idle provisioned concurrency price**: See [Pricing](https://intl.cloud.tencent.com/document/product/583/12281).

>? Idle provisioned concurrency is calculated in GBs (GB-second).

The provisioned concurrency feature only charges small idle fees for the instances that have been configured and started but are not in use, **while no additional fees are charged for the instances that have been configured and are in use**. In other words, only when the number of provisioned instances is greater than the number of concurrent instances for the current version will idle fees be incurred. For examples, see [Billing Example](https://intl.cloud.tencent.com/document/product/583/44256).

## Basic Package Fees
- **Monthly basic package fees = number of days in the month (for example, 31 days in May or 30 days in April)** * **basic package price**
- **Daily basic package fees = 1 (day)** * **basic package price**
- **Days**: **1 day** by default.
- **Basic package fee**: See [Pricing](https://intl.cloud.tencent.com/document/product/583/12281).

>? 
>- If you have used SCF for three months or shorter after the activation, the platform will grant a free tier by default without deducting the basic package fees.
>- If you have used SCF for more than three months after the activation, and you have valid subscription packages, the basic package fees will not be charged.
>- The function invocations in a calendar month is counted on the first day of the next month. If there is no any function-related usage incurred, including the function resource usage, function invocations, and public network outbound traffic, the basic package fees will not be charged in the current month. If any function usage is generated in the current month, the basic package fees will be charged next month.
