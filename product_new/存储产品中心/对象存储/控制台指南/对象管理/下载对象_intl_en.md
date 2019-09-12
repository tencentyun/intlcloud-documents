## Overview
You can download existing objects in a bucket in the COS Console. Specifically, you can download a single object in the console or download multiple objects in batches using the COSBrowser tool.

## Prerequisites
Before downloading an object, make sure that the object already exists in the bucket. If no objects have been uploaded, upload them first as instructed in [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/13321).

## Downloading a Single Object
#### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click Bucket List on the left sidebar to enter the bucket list page.
2. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
   ![](https://main.qcloudimg.com/raw/46307132ac1ef1e8422667abd896f878.png)
3. On the "Objects" tab, find the object you want to download. You can download it in three ways:
  1. Click **Download** to the right of the selected object to download it.
![](https://main.qcloudimg.com/raw/dbd6d274ad940889ffaa5f23d9062d9a.png)
  2. Select the object and click **Download** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/5c3a1e304185faa6fcbf7f5e7a237055.png)
  3. Click **Details** to the right of the object to enter the file details page. Click **Download Object** to download the object. Or, click **Copy Temporary Link**, paste the link into a browser address bar, and press Enter to download the object.
![](https://main.qcloudimg.com/raw/fea63064704835d1d99bfe0da3ddff40.png)

>- If the bucket where the object is stored is Private Read/Write, a signature will be automatically calculated and added at the end of the address copied here. For more information on how to generate a signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- The temporary link with a signature is valid for one hour from the moment you click to view the **Details**. You can refresh the validity period of the signature by clicking **Refresh**.

## Downloading Objects/Folders in Batches
> You can only download individual objects in the COS Console. To download multiple objects or folders in batches, it is recommended that you install the [COSBrowser client](https://intl.cloud.tencent.com/document/product/436/11366). Here is how to download objects or folders in batches in the console in conjunction with the **COSBrowser client**.
#### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and enter the bucket list page. Find the bucket where the object is stored and click the bucket name to enter the bucket management page.
![](https://main.qcloudimg.com/raw/46307132ac1ef1e8422667abd896f878.png)
2. Select multiple objects and click **Download** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/b78cedfcbb1ab9ebe317d0a51116960e.png)
3. Follow the on-screen prompts to install or launch the COSBrowser client and log in.
![](https://main.qcloudimg.com/raw/0e5706fb690d250200d1fe9bf3b86b8d.png)
4. After COSBrowser is launched, the selected files will be automatically added to the download queue and start to download. You can click **Download List** to view them.
![](https://main.qcloudimg.com/raw/140c741db0854e17d24d2b69e89bd268.png)
