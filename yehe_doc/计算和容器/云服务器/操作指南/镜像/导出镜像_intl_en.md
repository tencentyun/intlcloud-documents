## Overview
Tencent Cloud allows you to export created custom images to [COS](https://intl.cloud.tencent.com/document/product/436/6222) buckets.

## Prerequisites
- [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to activate this feature.
- Activate the COS service in the [COS console](https://console.cloud.tencent.com/cos).
- Create a bucket in the same region as of the custom image to export. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).


## Limits
- Windows custom images cannot be exported.
- For a custom image, the capacity of a system disk or data disk cannot be greater than 500 GB.
- When the image of an entire CVM instance is exported, the CVM instance cannot contain more than 5 data disks.


## Billing Description[](id:feeDescription)
If you use other services such as COS when using CVM, fees will be calculated according to the billing rules of the actually used services.
- Fees involved for exporting images to COS buckets:
 - **[Storage usage fee](https://intl.cloud.tencent.com/document/product/436/40099)**: Storing images in COS buckets will incur a storage usage fee, which is calculated according to the object size, storage class and region.
 - **[Request fee](https://intl.cloud.tencent.com/document/product/436/40100)**: Exporting images to COS buckets will incur a write request fee, which is calculated according to the number of write requests.
 - **[Traffic fee](https://intl.cloud.tencent.com/document/product/436/33776)**: Exporting images to COS buckets will generate upstream traffic. Upstream traffic over both the public and private networks are free of charge.
- Fees involved for downloading images from COS buckets
 - **[Request fee](https://intl.cloud.tencent.com/document/product/436/40100)**: Downloading images from COS buckets will incur a write request fee, which is calculated according to the number of write requests.
 - **[Traffic fees](https://intl.cloud.tencent.com/document/product/436/33776)**: Downloading images from COS buckets will generate downstream traffic. COS will calculate the traffic volume. Downstream traffic over the private network is free of charge, but that over the public network is charged.

## Directions
1. Log in to the CVM console and select **[Images](https://console.cloud.tencent.com/cvm/image)** on the left sidebar.
2. In the upper part of the **Images** page, select the region where the custom image to export resides and click the **Custom Image** tab.
3. Find the target image and select **More** > **Export image**.
![](https://qcloudimg.tencent-cloud.cn/raw/67a493d7ae96d92b514f5c124619821c.png)
4. In the **Export image** pop-up window, set parameters as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/4cf1d41610772605ac5867be12353b5a.png)
 - **COS Bucket**: Select the bucket to store the image. Note that the bucket and the image must be in the same region.
 - **Prefix of the files to export**: Customize the prefix of the file to export.
 Select **Agree to authorize CVM to access my COS bucket**.
5. Click **OK** to start exporting the image.
6. In the pop-up window, click **OK**.
The export duration depends on the size of the image file and the length of the export task queue. Once exported, the image file is stored in the destination bucket with the name similar to `Custom prefix_xvda.raw`. To check the image, go to the [Bucket List](https://console.cloud.tencent.com/cos/bucket) page, and click the ID of the destination bucket to go to the bucket details page. 
