## Overview
You can download existing objects in a bucket in the COS console. Specifically, you can download a single object in the console or download multiple objects in batches using the COSBrowser tool.

## Prerequisites
Before downloading an object, make sure that the object already exists in the bucket. If no objects have been uploaded, upload them first as instructed in [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/13321).

## Directions

### Downloading a single object
1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left.
5. Find the target object and click the corresponding **Download** button.
 - Click **Download** in the **Operation** column on the right of the object.
 - Select the object and click **More Actions > Download** at the top.
 - Click **Download** in the **Operation** column on the right of the object to enter the file details page, and then click **Download Object**.
 You can also click **Copy Temporary Link**, paste the link into a browser, and press **Enter**.
>?
> - If the bucket where the object is stored is private read/write, a signature will be automatically calculated and added at the end of the address copied here. For more information on how to generate a signature, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
> - The temporary link with a signature is valid for 1 hour from the moment you click to view the **Details**. You can refresh the validity period of the signature by clicking **Refresh**.
>- By default, if the downloaded object can be directly opened in the browser, then accessing the temporary URL will directly preview the object rather than downloading it.


### Downloading objects or folders in batches
>? You can only download individual objects in the COS console. To download multiple objects or folders in batches, we recommend you install the [COSBrowser client](https://intl.cloud.tencent.com/document/product/436/11366). Here is how to download objects or folders in batches in the console in conjunction with the **COSBrowser client**.
>

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left.
5. Select multiple objects and click **More Actions > Download** at the top.
6. Follow the on-screen prompts to install or launch the COSBrowser client and log in.
5. Select the file storage location, and selected files will automatically enter the download queue. You can click **Download List** to view them.



