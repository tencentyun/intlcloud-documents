## Billing Overview

Cloud Storage Gateway (CSG) is **pay-as-you-go** and is billed and settled daily by the actually used traffic.

CSG traffic is divided into **write traffic** and **read traffic**, and the write traffic has a daily capped price for each CSG instance.

In addition, as the storage service of CSG is based on COS, part of the storage fees will be listed in COS bills. For more information, please see [COS Pricing Overview](https://intl.cloud.tencent.com/pricing/cos).

If you deploy CSG on CVM, corresponding CVM fees will be incurred. For more information, please see [CVM Pricing Overview](https://intl.cloud.tencent.com/pricing/cvm).

### Billable items

CSG write traffic is the traffic consumed when your application writes to CSG, while CSG read traffic is the traffic consumed when your application reads from CSG.

### CSG pricing

| Billable Item | Billing Cycle | Unit Price (USD/GB) | Capped Price (USD/Gateway Instance/Day) |
| ---------------------- | ---------------------- | ------------- | ---------------------------------------------------- |
| Write traffic | Daily | 0.00285 | 2 <br>(Each gateway instance has a daily capped price of 2 USD, that is, when a gateway instance's daily write traffic exceeds 750 GB, the traffic will be billed as 750 GB; otherwise, the traffic will be billed as actually consumed) |
| Read traffic           | Daily     | 0.00285         | N/A            |


## Viewing Billing Details

### Directions
1.	 Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/).
2.	 Click **Billing Center** in the top-right corner to enter the Billing Center overview page.
3.	 On the left sidebar, click **Billing**.
4.	 Click **Billing Details** in the drop-down list and then select the CSG product to view CSG's bills by instance and detailed bills online.

## Arrears and Service Suspension

If your account falls into arrears, the CSG service will be suspended after 24 hours. Your data will be retained for 120 days. If you fail to top up your account to a positive balance within this period, your data will be destroyed.

Once you receive the arrears reminder, please go to [Billing Center > Payment](https://console.cloud.tencent.com/account/recharge) to top up your account as soon as possible to prevent your business from being affected.

You can also configure alarms for arrears through the balance alarm feature in the Billing Center. 
