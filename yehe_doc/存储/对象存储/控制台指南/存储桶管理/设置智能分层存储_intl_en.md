## Overview

You can specify COS INTELLIGENT TIERING as the storage class of your objects to reduce storage costs. Objects are automatically moved between two storage tiers (frequent access and infrequent access) when access patterns change.

INTELLIGENT TIERING is ideal for data with unknown or changing access patterns. It offers the same low latency and high throughput as STANDARD while featuring lower costs. Users can change the storage class of objects with uncertain access patterns from STANDARD to INTELLIGENT TIERING as needed to reduce in-cloud storage costs.

For more information about INTELLIGENT TIERING and the supported regions, please see [Overview - INTELLIGENT TIERING](https://intl.cloud.tencent.com/document/product/436/38305).

>!
>
>- Storage usage fees of INTELLIGENT TIERING are described as follows:
 - Storage fees for data in the frequent access tier are consistent with the list price of STANDARD.
 - Storage fees for data in the infrequent access tier are consistent with the list price of STANDARD_IA.
>- The request fees of INTELLIGENT TIERING are consistent with that of STANDARD. The traffic fees, management feature fees, and supported regions are the same as those of other storage classes. INTELLIGENT TIERING involves no data retrieval fees but does involve object monitoring fees. For more information, please see [Product Pricing](https://buy.cloud.tencent.com/price/cos).



## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to go to the bucket list page.
2. Locate the desired bucket you want to set INTELLIGENT TIERING for and click its name to go to its management page.
3. Click **Basic Configurations** > **INTELLIGENT TIERING**. Then click **Edit** and switch on the **Status** toggle. After this, perform configuration by referring to the description below.
   **Conversion days**: specifies the time period to move objects to the infrequent access tier. The valid values are 30, 60, and 90. For example, if this parameter is set to 30, an object that is not accessed for 30 consecutive days will be moved from the frequent access tier to the infrequent access tier.
    ![](https://main.qcloudimg.com/raw/97f9f450c62c3f914235019c08a604fe.png)
4. After confirming the configuration, click **Save**. Note that **INTELLIGENT TIERING** cannot be disabled or suspended after being enabled.
<img src="https://main.qcloudimg.com/raw/77f8f6416d5929025fe2d1e46afcc630.png" width="30%"></img>
5. After enabling INTELLIGENT TIERING, click **File List** > **Upload Files**. Then, select the files to upload.
6. Click **Next** to set the object properties. Set **Storage Class** to **INTELLIGENT TIERING** and then click **Upload** to upload your objects to the INTELLIGENT TIERING storage class. COS will move your objects between the storage tiers automatically. For more information about other configuration items, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).



