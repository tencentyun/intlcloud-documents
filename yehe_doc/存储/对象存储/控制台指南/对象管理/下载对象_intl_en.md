## Overview
You can download existing objects in a bucket in the COS console. Specifically, you can download a single object in the console or download multiple objects in batches using the COSBrowser tool.

## Prerequisites
Before downloading an object, make sure that the object already exists in the bucket. If no objects have been uploaded, upload them first as instructed in [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/13321).

## Directions

### Downloading a single object
1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Find the target object and choose the following options to download it as needed.
 - Click **Download** in the **Operation** column on the right of the object.

 - Select the object and click **More Actions > Download** at the top.

 - Click **Download** in the **Operation** column on the right of the object to enter the file details page, and then click **Download Object**.
 You can also click **Copy Temporary Link**, paste the link into a browser, and press **Enter**.
![](https://main.qcloudimg.com/raw/934b43a085b8cae825ddad88a0177caf.png)
>?
>- If the bucket where the object is stored is private read/write, a signature will be automatically calculated and added at the end of the address copied here. For more information on how to generate a signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- The temporary link with a signature is valid for one hour from the moment you click to view the **Details**. You can refresh the validity period of the signature by clicking **Refresh**.
>

### Downloading objects or folders in batches
>? You can only download individual objects in the COS console. To download multiple objects or folders in batches, it is recommended that you install the [COSBrowser client](https://intl.cloud.tencent.com/document/product/436/11366). Here is how to download objects or folders in batches in the console in conjunction with the **COSBrowser client**.
>

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Select multiple objects and click **More Actions > Download** at the top.
![](https://main.qcloudimg.com/raw/26499cc4f21d5a76580627fe9fb0db56.png)
6. Follow the on-screen prompts to install or launch the COSBrowser client and log in.
5. Select the file storage location, and selected files will automatically enter the download queue. You can click **Download List** to view them.
![](https://main.qcloudimg.com/raw/140c741db0854e17d24d2b69e89bd268.png)
