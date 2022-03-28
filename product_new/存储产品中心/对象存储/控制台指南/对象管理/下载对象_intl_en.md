## Overview
You can download existing objects in a bucket in the COS console. Specifically, you can download a single object in the console or download multiple objects in batches using the COSBrowser tool.

## Prerequisites
Before downloading an object, make sure that the object already exists in the bucket. If no objects have been uploaded, upload them first as instructed in [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/13321).

## Downloading a Single Object
#### Directions
1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click Bucket List on the left sidebar to enter the bucket list page.
2. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
   ![](https://main.qcloudimg.com/raw/46307132ac1ef1e8422667abd896f878.png)
3. Under **File List**, select the object you want to download. To download only one object, you can use one of the following ways:
  1. Click **Download** under the **Operation** column, or select a single object and click **Download** in the **More Actions** drop-down list at the top.
 ![](https://main.qcloudimg.com/raw/4ee4cb3f5ff0a5634ef8ed49d26c549b.png)
  2. Click **Details** to the right of the object to enter the file details page. Click **Download Object** to download the object. Or, click **Copy Temporary Link**, paste the link into a browser address bar, and press Enter to download the object.
  ![](https://main.qcloudimg.com/raw/934b43a085b8cae825ddad88a0177caf.png)

>- If the bucket where the object is stored is Private Read/Write, a signature will be automatically calculated and added at the end of the address copied here. For more information on how to generate a signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- The temporary link with a signature is valid for one hour from the moment you click to view the **Details**. You can refresh the validity period of the signature by clicking **Refresh**.

## Downloading Objects/Folders in Batches
> You can only download individual objects in the COS console. To download multiple objects or folders in batches, it is recommended that you install the [COSBrowser client](https://intl.cloud.tencent.com/document/product/436/11366). Here is how to download objects or folders in batches in the console in conjunction with the **COSBrowser client**.
#### Directions
1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and enter the bucket list page. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
2. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
3. Select multiple objects and click **Download** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/26499cc4f21d5a76580627fe9fb0db56.png)
4. Follow the on-screen prompts to install or launch the COSBrowser client and log in.
5. After COSBrowser is launched, the selected files will be automatically added to the download queue and start to download. You can click **Download List** to view them.
![](https://main.qcloudimg.com/raw/140c741db0854e17d24d2b69e89bd268.png)
