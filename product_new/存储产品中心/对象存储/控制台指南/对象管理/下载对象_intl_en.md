## Overview
You can download existing objects in a bucket in the COS Console. Specifically, you can download a single object in the console or download multiple objects in batches using the COSBrowser tool.

## Prerequisites
Before downloading an object, make sure that the object already exists in the bucket. If no objects have been uploaded, upload them first as instructed in [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/13321).

## Downloading a Single Object
#### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and enter the bucket list page. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
   ![](https://main.qcloudimg.com/raw/33e6c5aea515dbcfd5edcaa6f0c08875.png)
2. On the "Objects" tab, find the object you want to download. You can download it in three ways:
 1. Click **Download** to the right of the selected object to download it.
![](https://main.qcloudimg.com/raw/89035f8bdc59d1a51e17e7b7939c5b33.png)
 2. Select the object and click **Download** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/9b39ce4a4c1c1f6ac7040d68f0a51b95.png)
 3. Click **Details** to the right of the object to enter the file details page. Click **Download Object** to download the object. Or, click **Copy Temporary Link**, paste the link into a browser address bar, and press Enter to download the object.
![](https://main.qcloudimg.com/raw/e420cb9d1ea1325d4091295fe10c54ba.png)

>- If the bucket where the object is stored is private read/write, a signature will be automatically calculated and added at the end of the address copied here. For more information on how to generate a signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- The temporary link with a signature is valid for one hour from the moment you click to view the **Details**. You can refresh the validity period of the signature by clicking **Refresh**.

## Downloading Objects/Folders in Batches
> You can only download individual objects in the COS Console. To download multiple objects or folders in batches, it is recommended that you install the [COSBrowser client](https://intl.cloud.tencent.com/document/product/436/11366). Here is how to download objects or folders in batches in the console in conjunction with the **COSBrowser client**.
#### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and enter the bucket list page. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
![](https://main.qcloudimg.com/raw/33e6c5aea515dbcfd5edcaa6f0c08875.png)
2. Select multiple objects and click **Download** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/20a424347ddb521534b367f0cfa0f87e.png)
3. Follow the on-screen prompts to install or launch the COSBrowser client and log in.
![](https://main.qcloudimg.com/raw/ed780ab4afb1f4354cce6b006a483ead.png)
4. After COSBrowser is launched, the selected files will be automatically added to the download queue and start to be downloaded. You can click **Download List** to view them.
![](https://main.qcloudimg.com/raw/b3582a16ffe6d743da0610409fc28af3.png)
