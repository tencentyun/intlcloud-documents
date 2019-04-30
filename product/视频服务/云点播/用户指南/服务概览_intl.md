The Tencent Cloud VOD console provides a multi-dimensional data overview of the VOD service. You can log in to the [VOD Console](https://console.cloud.tencent.com/video) and click **Service Overview** in the left navigation pane to go to the **Service Overview** page to view various data.
![](https://main.qcloudimg.com/raw/371fbe78aa98aee65bcdd2c2008f19ba.png)

## Data Overview

The data overview section displays the total amount of console service usage in the current month, divided into four data dimensions: total files stored this month, total storage capacity of files this month, total transcoding duration this month, and total traffic used this month.
- Total files stored this month: This data entry is the total number of files you store in the VOD console in the current month. It is automatically refreshed on the first day of every month.
- Total storage capacity of files this month: This data entry is the total storage capacity in GB occupied by your files in the VOD console in the current month. It is automatically refreshed on the first day of every month.
- Total transcoding duration this month: This data entry is the total duration of the transcoding service in seconds you use in the VOD console in the current month. It is automatically refreshed on the first day of every month.
- Total traffic used this month: This data entry is the total amount of traffic in B consumed by the cache service you use in the VOD console in the current month. It is automatically refreshed on the first day of every month.

## Key Data

The key data section displays the storage capacity, transcoding duration, traffic used, and bandwidth consumed in the past week as well as the weekly trends. You can click a tab for a detailed view. You can also click **Details** in the upper right corner to go to the [Data Center](https://cloud.tencent.com/document/product/266/14060) to view more details.

## Billing
The billing section shows the current billing method of your Tencent Cloud account.
- ** Daily settlement**: You can click [About Billing](https://cloud.tencent.com/document/product/266/14666) to view the billing details, or click [Price Calculator] (https://buy.cloud.tencent.com/price/vod/calculator) to estimate the prices of different resource combinations.
- **Monthly settlement**: Please contact your Tencent Cloud representative.

## Resource Package
The data displayed for resource packages vary slightly by billing method.
### Daily Settlement
The resource package section displays the resource package usage, name, and expiration time under the current account. If the billing method is changed from daily settlement to monthly settlement, the resource packages will be frozen and cannot be used, and the resource package section will no longer display the resource package information.
 - If the current account has no purchased resource packages or all packs have expired, you can click **Buy Now* to go to the [VOD resource package purchase page](https://buy.cloud.tencent.com/vod?from=console-portal-buy-vod) for purchase.
 - If the current account has effective resource packages, only one of each resource package type will be displayed in this section. Resource packages are categorized into video storage resource packages, video transcoding resource packages, and video cache resource packages.
  - Click **Upgrade/Renew** to upgrade or renew a resource package.
  - Click **View All** to go to the **Resource Package Management** page, where you can purchase a new pack, view the type, usage, claim/purchase time, expiration time, and status of an existing pack, or upgrade/renew it.
![Resource Package Management](https://main.qcloudimg.com/raw/9acdf3db9743bc576be9f375f3f33bc0.png)

>?For daily settlement, during the validity period of a resource package, the current storage capacity, transcoding duration, and cache amount will be preferably deducted from the resource package, and after the pack runs out, fees will be deducted from the account balance. For more information, see [Resource Package (Prepaid)](https://cloud.tencent.com/document/product/266/14667).

### Monthly Settlement

Resource packages (prepaid) are not supported for monthly settlement.
If the current monthly settlement method is changed from daily settlement method, and resource packages have been purchased before the change, they will be frozen and cannot be used. When you change back to the daily settlement method, they will be automatically unfrozen and can be used during their validity periods. The frozen status of resource packages can be queried in the [VOD Console](https://console.cloud.tencent.com/video).
