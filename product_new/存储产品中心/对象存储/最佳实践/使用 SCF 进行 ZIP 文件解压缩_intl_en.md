## Scenario

[SCF](https://intl.cloud.tencent.com/document/product/583) and [COS](https://intl.cloud.tencent.com/document/product/436) are used in this example where a .zip file you uploaded to COS needs to be decompressed and the zip package name needs to be returned to COS as the folder name. You can extend the sample code to do more things such as decompressing files in other formats.

> As the temporary storage space allocated by SCF for each execution is currently 512 MB, it is recommended to keep the size of a single zip package below 300 MB and size of a single extracted file below 200 MB.

## Directions

<span id="step01"></span>

### Creating a Bucket

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. Create a source bucket to store the uploaded .zip file, name it "zip-upload", select **Beijing** for its region, and select **Private read/write** for its access permission.
![](https://main.qcloudimg.com/raw/d53dcc605e19b60dcd731677be6bce8d.png)
3. Create a destination bucket to store the extracted files, name it "unzip", select **Beijing** for its region, and select **Private read/write** for its access permission.
![](https://main.qcloudimg.com/raw/a21e6da03df0a67097c5bdf9b16f8d15.png)

> For more information on how to create a bucket and set access permissions for it, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309) and [Setting Access Permissions](https://intl.cloud.tencent.com/document/product/436/13315). 

<span id="step02"></span>

### Creating an SCF Function

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) and enter the **Function Service** page.
2. Select **Beijing** region and click **Create** to enter the function creating page.
![](https://main.qcloudimg.com/raw/6d7c01d8a8e05fa3ba314c2a81d3cde0.png)
3. On the **Create a Function** page, Configure the following information:
	- **Function Name**: "unzip_to_cos".
	- **Creation Method**: Select "Template function". After completing the configuration, click **Save**.
	- **Template Search**: Enter the search keyword "unzip" and select the "unzip_to_cos" template (this template currently only supports the zip format. If you need to process other formats such as rar or 7z, you need to expand the code by yourself). You can move the cursor over the template function and click **Learn More** to view the template function details. The function code can be downloaded.
![](https://main.qcloudimg.com/raw/747fe3b60669de32af760620830f00d4.png)
4. Configure information and click **Next**. Go to the function configuration page, keep the default configuration, and click **Completed** to complete the function creation.
5. Click **Function Code**. In this function, you need to modify the following parameters according to the comments in the function code editor. After the modification is completed, click **Save**.
 - appid: Available in [Account Information](https://console.cloud.tencent.com/developer).
 - secret_id、secret_key: Available in [API Key Management](https://console.cloud.tencent.com/cam/capi).
 - region: The region of the target bucket, here is ap-beijing.
 - bucket_upload: which should be "unzip bucket" here.
 - password: which is the password of the zip package and optional.
![](https://main.qcloudimg.com/raw/67a9e79779146fd29772fdbff549a556.png)
6. Click **Function Configuration** and change the timeout period of the function to 100 seconds. Finally click【Save】. In actual executions, if the function times out, you can increase the timeout period as needed.
![](https://main.qcloudimg.com/raw/69884533f9d712a17d9ea99de2e8e1fb.png)

<span id="step03"></span>

### Configuring a COS Trigger
1. Create the function as instructed in the above steps.
2. Select **Trigger Method** > **Add Trigger** to add a COS trigger for the function and configure the following items. After configuring the following information, Click **Save**.
 - **Trigger Method**: Select "COS trigger".
 - **COS Bucket**: Select "zip-upload".
 - **Event Type**: Select "All creation events" and keep the default values for other parameters.
![](https://main.qcloudimg.com/raw/88590d14d8aa829c69f9a4ba1d3c74b5.png)

<span id="step04"></span>

### Testing the Function

1. Download the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip) in .zip format.
2. Go to the [COS](https://console.cloud.tencent.com/cos5/bucket) Console, select the created bucket "zip-upload", and click **Upload File**.
3. In the **Upload File** window that pops up, select the test sample downloaded in step 1 and click **Upload**.
4. Enter the other bucket "unzip" and you can view the extracted files.
![](https://main.qcloudimg.com/raw/bc3a4919b73683a5a8a3f5b74b52e420.png)
5. Go to the [SCF](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) Console and view the execution result. Select **Function Service** > **Function** > **Execution Log** to see the printed log information.
![](https://main.qcloudimg.com/raw/66ec9c1e7268d7ad5a22bf7e000a9739.png)
