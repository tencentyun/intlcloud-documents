## Overview

You can specify INTELLIGENT TIERING as the storage class of your objects to reduce storage costs. Then, COS automatically moves objects between two storage tiers (frequent access and infrequent access) when the data access pattern changes.

INTELLIGENT TIERING is ideal for data with unknown or changing access patterns. It offers the same low latency and high throughput as STANDARD while featuring lower costs. You can change the storage class of objects with uncertain access patterns from STANDARD to INTELLIGENT TIERING as needed to reduce your cloud storage costs.

For more information on INTELLIGENT TIERING and the supported regions, see [INTELLIGENT TIERING Overview](https://intl.cloud.tencent.com/document/product/436/38305).

>!
> - Storage usage fees of INTELLIGENT TIERING are described as follows:
> - Storage fees for data in the frequent access tier are consistent with the published prices of STANDARD.
> - Storage fees for data in the infrequent access tier are consistent with the published prices of STANDARD_IA.
>- The request fees of INTELLIGENT TIERING are consistent with the published prices of STANDARD. The traffic fees, management feature fees, and supported regions are the same as those of other storage classes. INTELLIGENT TIERING also charges for object monitoring rather than data retrieval. For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
> 

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
2. Find the target bucket and click the bucket name to enter the bucket details page.
3. Click **Basic Configurations** > **INTELLIGENT TIERING**, find the **INTELLIGENT TIERING** configuration item, click **Edit** to toggle it on, and set the configuration items as follows.

**Conversion days**: Specifies the time period to move objects to the infrequent access tier. The valid values are 30, 60, and 90. For example, if this parameter is set to 30, an object not accessed in 30 consecutive days will be moved from the frequent access tier to the infrequent access tier.
4. After confirming that everything is correct, click **Save**.
>! INTELLIGENT TIERING cannot be disabled or suspended once configured.
>

5. After enabling INTELLIGENT TIERING, click **File List** on the left sidebar.
6. On the **File List** page, click **Upload Files**.
7. In the pop-up window, select the file to be uploaded, click **Configure Parameters** to configure **Object Properties**, and set **Storage Class** to **INTELLIGENT TIERING**.
8. Click **Upload** to upload the object to the INTELLIGENT TIERING storage class. COS will move the object between storage tiers automatically. For more information on other configuration items, see [Uploading Object](https://intl.cloud.tencent.com/document/product/436/13321).



