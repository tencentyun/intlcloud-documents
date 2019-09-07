## Overview
You can download existing objects in a bucket in the COS Console. Specifically, you can download a single object in the console or download multiple objects in batches using the COSBrowser tool.

## Prerequisites
Before downloading an object, make sure that the object already exists in the bucket. If no objects have been uploaded, upload them first as instructed in [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/13321).

## Downloading a Single Object
#### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and enter the bucket list page. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
   ![](https://main.qcloudimg.com/raw/46f3f6bcf85a1ca8f16a2f47479d0ef8.jpg)
2. On the "Objects" tab, find the object you want to download. You can download it in three ways:
 1. Click **Download** to the right of the selected object to download it.
![](https://main.qcloudimg.com/raw/45e44cdc6495cd33a477bbcf83fe6649.jpg)
 2. Select the object and click **Download** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/6265db98be71116a293b929875d98365.jpg)
 3. Click **Details** to the right of the object to enter the file details page. Click **Download Object** to download the object. Or, click **Copy Temporary Link**, paste the link into a browser address bar, and press Enter to download the object.
![](https://main.qcloudimg.com/raw/88e128e95c375e971ea5995aae7a9206.jpg)

>- If the bucket where the object is stored is Private Read/Write, a signature will be automatically calculated and added at the end of the address copied here. For more information on how to generate a signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- The temporary link with a signature is valid for one hour from the moment you click to view the **Details**. You can refresh the validity period of the signature by clicking **Refresh**.

## Downloading Objects/Folders in Batches
> You can only download individual objects in the COS Console. To download multiple objects or folders in batches, it is recommended that you install the [COSBrowser client](https://intl.cloud.tencent.com/document/product/436/11366). Here is how to download objects or folders in batches in the console in conjunction with the **COSBrowser client**.
#### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and enter the bucket list page. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
![](https://main.qcloudimg.com/raw/46f3f6bcf85a1ca8f16a2f47479d0ef8.jpg)
2. Select multiple objects and click **Download** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/a947ce302b4b81495da5d1de0ea7f71e.jpg)
3. Follow the on-screen prompts to install or launch the COSBrowser client and log in.
![](https://main.qcloudimg.com/raw/8139647ac37a73deed1de5a7cc235966.png)
4. After COSBrowser is launched, the selected files will be automatically added to the download queue and start to download. You can click **Download List** to view them.
![](https://main.qcloudimg.com/raw/ab3c5cd10121b5d149bc97622bf11a0a.png)
