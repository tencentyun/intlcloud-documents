
MediaLive supports exporting HLS files to COS for archiving, which requires you to create a bucket in COS and authorize MediaLive to access your bucket.
### Prerequisites
Before outputting HLS files to COS for archiving, please confirm that you have activated the [COS service](https://console.cloud.tencent.com/cos5).
### Step 1: Create a COS bucket
After activating the COS service, you can create a COS bucket in the nearest region.
 ![](https://main.qcloudimg.com/raw/e31c7202bb6435015f3093321a938155.jpg)

### Step 2: Select the output group type
Go back to the MediaLive console. Select HLS_ARCHIVE as the output group type.
 ![](https://main.qcloudimg.com/raw/bee1eddef01d63637ac7847ba10b645f.jpg)

### Step 3: Authorize MediaLive to access the COS bucket
Because you have not authorized MediaLive to access your COS bucket, the COS destination fields will be grayed out and cannot be filled in. Click “Click here” in the prompt box to authorize MediaLive.
 ![](https://main.qcloudimg.com/raw/e77c846ead0f4bd86dbe3e123f4633d4.jpg)
Click “Authorize Now” and go to the “Service Authorization” page. Click “Grant” to complete the authorization.
 ![](https://main.qcloudimg.com/raw/f7aea806667ee05ed69210e246efc3db.jpg)
Go back to the MediaLive page after completing the authorization. Select “Authorization completed.” Then, you can fill in the COS destination fields.
 ![](https://main.qcloudimg.com/raw/5bfb748841656922aa56ee9407330d30.jpg)

### Step 4: Enter the COS archiving URL
You can enter a COS archiving URL based on the created COS bucket. The format is `http://<BucketName-APPID>.cos.<Region>.myqcloud.com/path`.
### Step 5: Save and submit the configuration
You can go back to [MediaLive channel creation](https://intl.cloud.tencent.com/document/product/1048/38374) to complete the other channel configurations. Click “Done” to save and submit the configurations.
