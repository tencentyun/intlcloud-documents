## Scenario

[SCF](https://intl.cloud.tencent.com/document/product/583) and [COS](https://intl.cloud.tencent.com/document/product/436) are used in this example where a .zip file you uploaded to COS needs to be decompressed and the zip package name needs to be returned to COS as the folder name. You can extend the sample code to do more things such as decompressing files in other formats.

> As the temporary storage space allocated by SCF for each execution is currently 512 MB, it is recommended to keep the size of a single zip package below 300 MB and size of a single extracted file below 200 MB.

## Directions

<span id="step01"></span>

### Creating a Bucket

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. Create a source bucket to store the uploaded .zip file, name it "zip-upload", select **Beijing** for its region, and select **Private read/write** for its access permission.
3. Create a destination bucket to store the extracted files, name it "unzip", select **Beijing** for its region, and select **Private read/write** for its access permission.

> For more information on how to create a bucket and set access permissions for it, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309) and [Setting Access Permissions](https://intl.cloud.tencent.com/document/product/436/13315). 

<span id="step02"></span>

### Creating an SCF Function

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) and enter the **Function Service** page.
2. Select **Beijing** region and click **Create** to enter the function creating page.
3. On the **Create a Function** page, configure the following information and click **Next**.
	- **Creation Method**: Select "Template function".
	- **Function Name**: "unzip_to_cos".
	- **Template Search**: Select the "Zip package decompression" template with "Python2.7" as "language". You can move the cursor over the template function and click **View Details** to view the template function details. The function code can be downloaded.
![](https://main.qcloudimg.com/raw/1cee42e5814793159daecd8387fb37ee.jpg)
4. Go to the function configuration page, keep the default configuration, and click **Finish** to complete the function creation.
5. Click **Function Code**. You need to modify the parameters according to the comments in the function code editor.
Modify the configuration variables: appid, secret_id, secret_key, region, bucket_upload (which should be "unzip bucket" here), and password (which is the password of the zip package and optional). After completing the configuration, click **Save**.
6. Click **Function Configuration** and change the timeout period of the function to 100 seconds. In actual executions, if the function times out, you can increase the timeout period as needed.

<span id="step03"></span>

### Configuring a COS Trigger
1. Create the function as instructed in the above steps.
2. Select **Triggers** > **Add a Trigger** to add a COS trigger for the function and configure the following items.
 - **Trigger**: Select "COS trigger".
 - **COS Bucket**: Select "zip-upload".
 - **Event Type**: Select "All creation events" and keep the default values for other parameters.
3. Click **Save**.

<span id="step04"></span>

### Testing the Function

1. Download the [test sample](https://main.qcloudimg.com/raw/6e0d4837eefd0ce77dac8a3973acdf39.zip) in .zip format.
2. Go to the [COS](https://console.cloud.tencent.com/cos5/bucket) Console, select the created bucket "zip-upload", and click **Upload File**.
3. In the **Upload File** window that pops up, select the test sample downloaded in step 1 and click **Upload**.
4. Enter the other bucket "unzip" and you can view the extracted files.
5. Go to the [SCF](https://console.cloud.tencent.com/scf/list?rid=8&ns=default) Console and view the execution result. Select **Function Service** > **Function** > **Execution Log** to see the printed log information.

