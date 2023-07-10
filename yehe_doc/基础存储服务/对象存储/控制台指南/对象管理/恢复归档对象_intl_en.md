## Overview

You can restore an object from the ARCHIVE or DEEP ARCHIVE storage class through the COS console. The restoration operation will create a copy of the object in the STANDARD storage class. You can read, download, or perform other operations on the copy within its validity period. The copy will be deleted automatically after expiration. For more information about storage classes, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

>! If you restore objects from ARCHIVE, the object copy will be billed at STANDARD rates. If you restore objects from DEEP ARCHIVE, the object copy will be charged request fees at the marked unit price, and traffic fees at STANDARD rates. For more information, see [Product Pricing](https://www.tencentcloud.com/pricing/cos?lang=en&pg=).
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Locate the object to restore and click **Restore** in the **Operation** column. To restore multiple archived objects at a time, select them all in the object list, and click **Restore** from the **More Actions** drop-down list at the top.
6. In the pop-up window, configure the restoration mode and the validity period (in days) of the copy.
![](https://main.qcloudimg.com/raw/3d3163c09213423aa959b179237ab137.png)
The parameters are described as follows:
 - **Restoration Mode**: Expedited, standard, or bulk retrieval.
    - Expedited retrieval: This is the fastest mode. Archived files can be restored within 1-5 minutes. If you need to access your archival data urgently, you can use this mode to greatly reduce the restoration time. **Please note that the expedited retrieval mode is not available for DEEP ARCHIVE**.
    - Standard retrieval: Files can be restored from ARCHIVE within 3-5 hours, and from DEEP ARCHIVE within 12 hours.
    - Bulk retrieval: This is the lowest-cost mode. If your need for the archival data is not urgent, this mode can usually restore massive amounts of data from ARCHIVE within 5-12 hours, and from DEEP ARCHIVE within 48 hours, both with an ultra-low cost.
>? The QPS of data restoration requests is limited to 100.
>
 - **Validity**: The number of days after which the copy will automatically expire and be deleted. The value range is 1 to 365 days. After the object is successfully restored, you can click **Restore** again to change the validity period of the copy in the pop-up window.
7. Click **OK**. The object enters the restoration process.
During this process, you can click **Details** to go to the object details page to check the restoration progress.
![](https://main.qcloudimg.com/raw/4686bc71f95d7178a8690f3eb49721e6.png)
8. After confirming that the object has been successfully restored, you can go to the object details page to perform access, download, and other operations on the object.
![](https://main.qcloudimg.com/raw/e794f58d2593df1ecb675fc7ffa5019c.png)
To modify the validity period of the copy, follow step 5 to click **Restore** again and modify the validity period in the pop-up window.
![](https://main.qcloudimg.com/raw/c464c9fa3e83213f7cf8692f32fa72ab.png)

