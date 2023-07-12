## Scenario

This scenario involves the use of [SCF](https://intl.cloud.tencent.com/document/product/583) and [COS](https://intl.cloud.tencent.com/document/product/436). Assume that you want to unzip (decompress) a ZIP file uploaded to COS, and upload the unzipped file back to COS using the same file name. You can extend the sample code to do more things such as decompressing files in other formats.

>As the temporary storage capacity allocated by SCF for each execution is currently 512 MB, it is recommended to keep the size of a single ZIP file below 300 MB and the size of a single decompressed file below 200 MB.

## Directions

<span id="step01"></span>

### Creating a bucket

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. Create a source bucket to store the uploaded ZIP file, name it "zip-upload", select **Beijing** for its region, and select **Private Read/Write** for its access permission.
![](https://main.qcloudimg.com/raw/d53dcc605e19b60dcd731677be6bce8d.png)
3. Create a destination bucket to store the decompressed files, name it "unzip", select **Beijing** for its region, and select **Private Read/Write** for its access permission.
![](https://main.qcloudimg.com/raw/a21e6da03df0a67097c5bdf9b16f8d15.png)

>For more information on how to create a bucket and set access permissions for it, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309) and [Setting Access Permissions](https://intl.cloud.tencent.com/document/product/436/13315). 

<span id="step02"></span>

### Creating an SCF function

1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default), and enter the **Function Service** page.
2. Select **Beijing** region and click **Create** to enter the function creating page.
3. Configure the following fields:
	- **Function Name**: enter "unzip_to_cos".
	- **Creation Method**: select "Function Template".
	- **Fuzzy Search**: enter “unzip” as search keyword, and select one of the optional unzipping templates (Currently, they only support ZIP format. For Rar, 7z, or any other formats, please expand the function code.) Click **Learn More** for the function template you want, and you can view its details and download it.
![](https://main.qcloudimg.com/raw/747fe3b60669de32af760620830f00d4.png)
4. Click **Next** to enter the function configuration page. Keep the default configuration, and click **Completed** to complete the function creation.
![](https://main.qcloudimg.com/raw/4df6cd01e6a521acb244fe21b5eb2fe8.png)
5. Click **Function Code**, and modify the following parameters in the function code editor as per the comments. Once completed, click **Save**.
 - appid: you can check it in [**Account information**](https://console.cloud.tencent.com/developer).
 - secret_id and secret_key: you can check them in [API Key Management](https://console.cloud.tencent.com/cam/capi).
 - region: the region where the destination bucket resides. Enter `ap-beijing`.
 - bucket_upload: enter `unzip-125xxxxxxx`.
 - password: the password for decompressing the zipped file. Leave it empty if you don’t want one.
![](https://main.qcloudimg.com/raw/67a9e79779146fd29772fdbff549a556.png)
6. Click **Function Configuration**, change the timeout period of the function to 100 seconds, and click **Save**. In actual executions, if the function times out, you can increase the timeout period as needed.
![](https://main.qcloudimg.com/raw/69884533f9d712a17d9ea99de2e8e1fb.png)

<span id="step03"></span>

### Configuring a COS trigger
1. Create the function as instructed in the above steps.
2. Select **Trigger Method**>**Add Trigger** to add a COS trigger for the function, configure the following items, and click **Save**.
 - **Trigger Method**: select "COS trigger".
 - **COS Bucket**: select "zip-upload".
 - **Event Type**: select "All creation events". Keep the default values for other parameters.
![](https://main.qcloudimg.com/raw/88590d14d8aa829c69f9a4ba1d3c74b5.png)

<span id="step04"></span>

### Testing the function

1. Download the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip) in **ZIP format**.
2. Go to the [COS](https://console.cloud.tencent.com/cos5/bucket) Console, select the created bucket "zip-upload", and click **Upload File**.
3. In the **Upload File** window that pops up, select the test sample downloaded in step 1 and click **Upload**.
4. Enter the other bucket "unzip" and you can view the decompressed files.
![](https://main.qcloudimg.com/raw/bc3a4919b73683a5a8a3f5b74b52e420.png)
5. Go to the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default), and view the execution result. Select **Function Service**>**Functions**>**Execution Log** to check the printed log.
<img src="https://main.qcloudimg.com/raw/66ec9c1e7268d7ad5a22bf7e000a9739.png" width="93%">

