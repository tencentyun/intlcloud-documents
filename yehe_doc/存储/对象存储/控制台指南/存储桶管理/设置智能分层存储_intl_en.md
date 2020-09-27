## Overview

Once you specify INTELLIGENT TIERING as the storage class for your objects, it will reduce your storage costs by moving your data automatically between two storage tiers — frequent access and infrequent access — when access patterns change.

INTELLIGENT TIERING is ideal for data with unknown or changing access patterns. It offers the same low latency and high throughput performance as COS STANDARD, and even lower storage costs. You can reduce your in-cloud storage costs by transitioning proper data as needed from STANDARD to INTELLIGENT TIERING.

For more information, see [Overview - INTELLIGENT TIERING](https://intl.cloud.tencent.com/document/product/436/38305).

>!
>
>- INTELLIGENT TIERING is currently available only in Beijing, Shanghai, and Guangzhou Public Cloud regions.
>- INTELLIGENT TIERING is billed for storage usage in the frequent access tier at the same published prices as STANDARD storage class, and in the infrequent access tier at the same published prices as STANDARD_IA storage class. INTELLIGENT TIERING requests are billed the same as STANDARD requests. The INTELLIGENT TIERING fees for traffic and management features are charged depending on the region, the same as in the other storage classes. There are no data retrieval fees, but additional charges apply for monitoring INTELLIGENT TIERING objects. For more information, please see [Product Pricing](https://buy.cloud.tencent.com/price/cos).

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Locate the bucket for which you want to set intelligent tiering configuration, and click its name to enter the bucket management page.
3. Click **Basic Configurations** > **Intelligent Tiering**, click **Edit**, and configure the required information.
4. Once completed, click **OK**. Please note that **once enabled, the intelligent tiering configuration cannot be disabled**, but only allow modifying the days for transition.
5. Once the configuration is enabled, you can upload objects to the INTELLIGENT TIERING storage class by using the COS console, APIs, SDKs or tools, and COS will automatically move your data between two access tiers. For directions on uploading objects through the console, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).

**Days for Transition**: specifies the number of days for moving objects to the infrequent access tier. For example, when it is set to 30, COS will move objects that have not been accessed for 30 consecutive days in the frequent access tier to the infrequent access tier.
