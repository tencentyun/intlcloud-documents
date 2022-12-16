SCF supports pay-as-you-go billing, and offers prepaid subscription packages.
Subscription packages offer a relatively lower unit price than pay-as-you-go. Furthermore, they provide free tiers of [concurrent function quota](https://intl.cloud.tencent.com/document/product/583/37040) and [function burst](https://intl.cloud.tencent.com/document/product/583/37040). 

## Pricing of Subscription Packages

SCF offers seven types of packages, including Personal General, Personal Premium, Team, Enterprise Basic, Enterprise General, Enterprise Premium and Enterprise Ultimate. Each type contains different quota of function resource usage, invocations, outbound traffic, concurrent functions and function burst. 


Detailed specs of different package types



| Type | Specification                                                   |Special offer| List price |
| ---------- | ------------------------------------------------------------ | -------------------- | ------------ |
| Personal General | Resource usage: 100K GBs <br>Function invocations: 500K for event-triggered functions and 500K for HTTP-triggered functions<br>Outbound traffic: 2 GB <br>Concurrent function: 128 GB <br>Function burst: 500 functions/minute| **1.48 USD/month**         | 1.9 USD/month      |
| Personal Premium | Resource usage: 1M GBs <br>Function invocations: 1M for event-triggered functions and 1M for HTTP-triggered functions<br>Outbound traffic: 2 GB <br>Concurrent function: 256 GB <br>Function burst: 500 functions/minute| **13.58 USD/month**         | 17 USD/month      |
| Team | Resource usage: 10M GBs <br>Function invocations: 10M for event-triggered functions and 10M for HTTP-triggered functions<br>Outbound traffic: 20 GB <br>Concurrent function: 512 GB <br>Function burst: 1000 functions/minute| **139.56 USD/month**         | 172 USD/month      |
| Enterprise Basic | Resource usage: 100M GBs <br>Function invocations: 100M for event-triggered functions and 100M for HTTP-triggered functions<br>Outbound traffic: 200 GB <br>Concurrent function: 1280 GB <br>Function burst: 2000 functions/minute| **1362.60 USD/month**         | 1721.5 USD/month      |
| Enterprise General | Resource usage: 300M GBs <br>Function invocations: 300M for event-triggered functions and 300M for HTTP-triggered functions<br>Outbound traffic: 600 GB <br>Concurrent function: 2560 GB <br>Function burst: 2500 functions/minute| **5165 USD/month**         | 5165 USD/month      |
| Enterprise Premium | Resource usage: 1 billion GBs <br>Function invocations: 1 billion for event-triggered functions and 1 billion for HTTP-triggered functions<br>Outbound traffic: 2000 GB <br>Concurrent function: 12,800 GB <br>Function burst: 5000 functions/minute| **13,330.38 USD/month**         | 17,215 USD/month      |
| Enterprise Ultimate | Resource usage: 10 billion GBs <br>Function invocations: 10 billion for event-triggered functions and 10 billion for HTTP-triggered functions<br>Outbound traffic: 20K GB <br>Concurrent function: 25,600 GB <br>Function burst: 10K functions/minute| **130,156.76 USD/month**         | 172,150 USD/month      |

## Deduction of Subscription Quota

- Sequence: Free quota (if any) > Namespace-specific package > Region-specific package > Pay-as-you-go. SCF offers a free tier for new SCF users for the first three months. Resource usage exceeding the free quota is first deducted from the package. If there is not available package quota, pay-as-you-go is adopted. 
- For each region and namespace, you can only subscribe to one package type for once. 

>? The function MEM size is not counted into consideration for package deduction.



## Purchasing Subscriptions 

You can purchase a subscription package for a specific region or namespace. This attribute cannot be changed after purchase. 
- Purchase only a region-specific package: The package quota is taken as the upper limit of the region, and it can be shared by all functions in this region. 
- Purchase only a namespace-specific package: The package quota is taken as the upper limit of the namespace, and it’s shared by all functions in this namespace. 
- Purchase both packages for a region and a namespace in this region: The regional quota is taken as the upper limit of the region. The quota of the namespace-specific package is the upper limit for the namespace, which means that when the quota of the namespace is used up, functions in this namespace DO NOT share the quota of the region. The regional quota is shared by functions in other namespaces without specific subscription packages. 
- The function reserved quota set for the current region/namespace cannot exceed the function concurrency quota of the package. You can upgrade the package or lower the reserved quota.

## Upgrading/Degrading Packages

You can upgrade or degrade a package within its validity period. The adjustment does not affect the expiration time of the package.

**Paying for the upgrade**


- You need to pay for the price difference brought by the upgrade. The amount is calculated by days. 
  - Upgrade fee = Monthly price of the new spec X Remaining subscription period (in months) X Eligible discount for the new spec - Monthly price of the original spec X Remaining subscription period (in months) X Eligible discount for the original spec
  Remaining subscription period = (Subscription expiration date - Current date)/(365/12)
- All the eligible discounts mentioned above refer to the discount stated in the SCF purchase page. 
- Check the latest price and eligible discount in the [subscription purchase page](https://console.cloud.tencent.com/scf/buy?rid=19&ns=default).   

**Getting refund for degrade**

- When you submit a degrading request, the purchased package is returned and place an order for the new package. 
 Refund for degrading = Refund of the original package - Price of the new package 
- If the price of the new package is higher than the refund amount of the original package, there is no refund.
Degrading is not supported in the following cases: 
- The ratio of used/total quota is larger than the ratio of elapsed validity/total validity. 
- The function reserved quota set for the current region/namespace cannot exceed the function concurrency quota of the package. You can upgrade the package or lower the reserved quota.


## Renewing Subscription
You can renew the package if necessary. For details, see [Renewal Management](https://intl.cloud.tencent.com/document/product/555/7454).

## Returning a Package
You can return a package and get the refund automatically.
Note the refunding is not supported in the following cases: 

- The ratio of used/total quota is larger than the ratio of elapsed validity/total validity. 
- The function reserved quota set for the current region/namespace cannot exceed the function concurrency quota of the package. You can upgrade the package or lower the reserved quota.


**Refund amount and method**

Refund amount = Paid order amount - Consumed resource amount

The consumed resource amount is calculated based on the usage duration.
Consumed resource amount = (usage duration / total amount) * original order price * current discount
>?A usage duration less than one day will be rounded up to one day, and the current system discount matching the usage duration applies.

## Invalidation of Packages

The quota of a package goes invalid upon its expiration time. After then, pay-as-you-go is automatically adopted for the SCF service under your account. 

**Policies after subscription expiration**


- The quota of resource usage, function invocations and outbound traffic: All are adjusted to the default free quota.
- Function concurrency and function burst: If the reserved concurrency is set and the concurrency quota exceeds the default quota, you need to remove the exceeding part. They will be adjusted to the default concurrency quota and function burst of the related region.
- If the exceeding function concurrency quota and function burst are not removed in time, they will be removed by the system automatically.

## How to Purchase

The following describes how to purchase subscriptions.
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/) and click **Subscriptions** on the left sidebar.
2. Click **Monthly subscriptions** to enter the purchase page. 
If you have not subscribed to any packages, the pay-as-you-go free tier is displayed in **Basic configurations**. After purchasing of a subscription package, the package quota is displayed.

### Purchase Subscriptions[](id:new)

1. In the subscription purchase page, select the region or namespace.  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/JSfA652_1.png)
2. Select the package you want, such as “Personal General”, and click “Purchase”.
3. In the “Purchase package” pop-up, specify the duration, read and agree to the reminders and click **Purchase**.  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ByvS790_2.png)
4. Confirm the information and click **Submit order**. 
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/yBbb400_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16711773007399.png" alt="image-20220324175806474" style="zoom:67%;" />
5. Complete the payment. You can then check details of the package in **Subscriptions** page. 

### Changing Specification
1. In the subscription purchase page, select the region or namespace. 
2. Select the target package, such as **Personal Premium**, and click **Purchase**.
>? Note that the region/namespace and expiration time cannot be changed.
>
3. In the **Adjust configuration** pop-up, confirm the information, read and agree to the reminder, and click “**Adjust now**.  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nba3994_3.png)
4. Confirm the information and click **Submit order**.
5. Complete the payment. You can then check details of the package in **Subscriptions** page. 

### Renewing Packages

**Manual Renewal**

 1. In **Basic configurations**, select **Operations - Renew**.  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TSid719_4.png)
 2. In the **Renew** page, confirm the information and click **OK**. 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jdTU857_5.png)
 3. Check the order information, and click **Submit order*. You can then check it in the **Monthly subscriptions** page. 

**Auto-Renewal**
- Method 1: Select **Auto-renewal** in the purchase page. 
- Method 2:
	1. In **Basic configurations**, select **Operations > Enable auto-renewal**. 
	2. You will be redirected to **Renewal management**. For details, see [Managing Auto-Renewal](https://intl.cloud.tencent.com/document/product/555/7454).


**Managing Renewal**
1. Click **Fess** in the top right corner and click **My Orders** to enter **Order Management**.
2. You will be redirected to **Renewal management**. For details, see [Managing Auto-Renewal](https://intl.cloud.tencent.com/document/product/555/7454).


### Refund
1. In **Basic configurations**, select **Operations - Get a refund**.  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/evFa928_6.png)
2. In the pop-up, check the information, read and agree to the reminder, and click **OK**. 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3U6n063_7.png)

### Managing Orders

You can manage purchased subscription packages in [Order Management](https://console.cloud.tencent.com/deal).
