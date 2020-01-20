This tutorial guides you through how to use VOD event notifications in "normal callback" and "reliable callback" modes.

## Prerequisites

- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and [verify your identity](https://intl.cloud.tencent.com/document/product/378/3629).
- Python 2.7 runtime environment for normal callback.

## Normal Callback
### Deploying callback receiving service

To get event notifications through [normal callback](https://intl.cloud.tencent.com/document/product/266/33948#normal-callback), you need to deploy a callback receiving service on a server with a public IP. Below describes how to deploy such a service on a CVM instance as an example:

1. Enter the [Instance List](https://console.cloud.tencent.com/cvm/index) page in the CVM Console and click **Create**.
2. Select the **Quick Configuration** menu, select **Ubuntu Server** or **CentOS** for **Image** and **1 Mbps** for **Public Network Bandwidth**, check **Allocate Free Public IP**, and then click **Buy Now**.
3. Enter the [Instance List](https://console.cloud.tencent.com/cvm/index) page again, find the CVM instance successfully created, and copy the public IP in **Primary IP Address** (**134.XXX.XXX.167** in this example).
![](https://main.qcloudimg.com/raw/d48f654b759159de0935e83bc0e6fdc8.png)
4. Log in to the purchased CVM instance, download the [source code package](http://document-1251659802.coscd.myqcloud.com/NotificationTuition.zip), extract it to your working directory, and run the following command:
		python NotificationReceiveServer.py
After the command is executed, the standard output of the CVM instance should print `Started httpserver on port 8080`, indicating that the service process has started and is listening on port 8080.
5. Enter `http://134.XXX.XXX.167:8080` in a browser, and the standard output of the CVM instance should print the following HTTP request information.
![](https://main.qcloudimg.com/raw/4e7eaffe641002f9b0307244e4bec8dc.png)

### Configuring normal callback
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Callback Settings** on the left sidebar.
2. Click **Settings**:
	- Callback Mode: select **Normal Callback**.
	- Callback URL: enter `http://134.XXX.XXX.167:8080`.
	- Callback Event: check **Callback on video upload completion**.
3. Click **OK**.

### Initiating and receiving normal callback

Please download the [demo video](http://1255566954.vod2.myqcloud.com/ca75586fvodgzp1255566954/484c46995285890788305672872/xUCHV5kOGyIA.wmv) to your local file system for getting started.
1. Click **Media Assets** on the left sidebar, select **Uploaded**, and click **Upload Video**.
![](https://main.qcloudimg.com/raw/4724951966b46c801498efed4b6ebec9.png)
2. In the **Upload Video** dialog box that pops up, select **Local Upload**, click **Select Video**, and upload the **demo video** to the VOD platform.
![](https://main.qcloudimg.com/raw/e0eb51db29de59e948b332ad05a069db.png)
 After performing the upload operation, you will see the video upload progress in the **Uploading** column.
![](https://main.qcloudimg.com/raw/7f072f0e67b4f3be6907ff1f5a414848.png)
 After the upload is completed, you will see the uploaded video and its corresponding ID (i.e., `FileId`) in the video list in the **Uploaded** column.
![](https://main.qcloudimg.com/raw/6c18e73eb8576fc120fe903fc0848927.png)
3. Check the CVM instance. The standard output should print the content of the notification for [video upload completion](https://intl.cloud.tencent.com/document/product/266/33950#817356113).
 <img src="https://main.qcloudimg.com/raw/f6439edcd8ae59cab1d393987382e136.png" width="818">
4. In the **Uploaded** column in **Media Assets**, select the video just uploaded and click **[Video Processing](https://intl.cloud.tencent.com/document/product/266/33892)**. Select **Manually select transcoding template** for **Processing Type**, check **MP4-LD-FLU (10)** in **Transcoding Template**, keep **Video Cover** checked, and click **OK**.
5. After waiting for 10 minutes, check the CVM instance, and its standard output should print the content of the notification for [task flow status change](https://intl.cloud.tencent.com/document/product/266/33953#.E6.99.AE.E9.80.9A.E5.9B.9E.E8.B0.83), including the results of transcoding (where `Type` is `Transcode`) and time point screencapturing for cover generation (where `Type` is `CoverBySnapshot`).
 <img src="https://main.qcloudimg.com/raw/4e577e7feb5524ff82e8a82c8e1cbdd2.png" width="818">

At this point, you have uploaded a video and performed a transcoding task on it. After the upload and transcoding were completed, your callback receiving service received notifications for **video upload completion** and **task flow status change**.

## Reliable Callback

1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Callback Settings** on the left sidebar.
2. Click **Settings**:
	- Callback Mode: select **Reliable Callback**.
	- Callback Event: check **video upload completion callback**.
3. Click **OK**.

### Initiating reliable callback

1. Click **Media Assets** on the left sidebar, select **Uploaded**, and click **Upload Video**.
![](https://main.qcloudimg.com/raw/4724951966b46c801498efed4b6ebec9.png)

2. In the **Upload Video** dialog box that pops up, select **Local Upload**, click **Select Video**, and upload the **demo video** to the VOD platform.
![](https://main.qcloudimg.com/raw/e0eb51db29de59e948b332ad05a069db.png)
 
 After performing the upload operation, you will see the video upload progress in the **Uploading** column.
![](https://main.qcloudimg.com/raw/7f072f0e67b4f3be6907ff1f5a414848.png)
 
 After the upload is completed, you will see the uploaded video and its corresponding ID (i.e., `FileId`) in the video list in the **Uploaded** column.
![](https://main.qcloudimg.com/raw/6c18e73eb8576fc120fe903fc0848927.png)

3. In the **Uploaded** column in **Media Assets**, select the video just uploaded and click **[Video Processing](https://intl.cloud.tencent.com/document/product/266/33892)**. Select **Manually select transcoding template** for **Processing Type**, check **MP4-LD-FLU (10)** in **Transcoding Template**, keep **Video Cover** checked, and click **OK**.

At this point, you have uploaded a video again and initiated a transcoding task for it. These operations have triggered event notifications.

### Pulling reliable callback

After an event notification is triggered, you need to proactively pull the reliable callback. You can use the API tool <!--api(https://intl.cloud.tencent.com/document/product/266/33433#API-Explorer)--> to run the `PullEvents` command for querying the event notifications to be consumed. The specific directions are as follows:
1. Go to the [API 3.0 Explorer of VOD's `PullEvents` command](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=PullEvents&SignVersion=) and enter your **key** (which can be viewed by clicking **View Key** in the [API Key Console](https://console.cloud.tencent.com/cam/capi)).
<img src="https://main.qcloudimg.com/raw/57bb4106c7ec29f0d49b94bafc95e38b.png" width="399">
2. Select **Online Call** in the right and click **Send Request**.
 <img src="https://main.qcloudimg.com/raw/d1bc047c565dbc00b1acd5607767a70b.png" width="615">
 
	After sending the request, observe the event list `EventSet` in the return result. The event list contains two event notifications for **video upload completion** and **task flow status change** respectively, and the corresponding event handlers are `8078360634045903972` and `8078360634045903972`.
 <img src="https://main.qcloudimg.com/raw/1497a3fd83ce599ef0a03437df53b6b4.png" width="579">
 <img src="https://main.qcloudimg.com/raw/9bf358ef2231a05237fe226cadebe136.png" width="579">
 
At this point, you have pulled two notifications for **video upload completion** and **task flow status change** in reliable callback. Next, you need to immediately confirm the pulled event notifications.

### Confirming reliable callback

The pulled reliable callback needs to be confirmed within **30 seconds**; otherwise:

* If the API for confirmation is called more than 30 seconds after an event handler is received, the call will fail.
* If the event is not confirmed within 30 seconds, it will be pulled again when the next reliable callback is pulled.

You can run the `ConfirmEvents` command in the API tool <!--api(https://intl.cloud.tencent.com/document/product/266/33434#API-Explorer)--> to query the event notifications to be consumed. The specific directions are as follows:

1. Go to the [API 3.0 Explorer of VOD's `ConfirmEvents` command](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ConfirmEvents&SignVersion=) and enter your **key**.
<img src="https://main.qcloudimg.com/raw/5b0e7986096a0e4512c5266a6c5e0073.png" width="399">

2. In the **EventHandles.N** input box, enter the event handler obtained when the event notification is pulled.

 <img src="https://main.qcloudimg.com/raw/9f6472bf94f362743ab0ef11858177c9.png" width="395">

3. Select **Online Call** in the right and click **Send Request**.
 
 <img src="https://main.qcloudimg.com/raw/d1bc047c565dbc00b1acd5607767a70b.png" width="615">

 After the request is successful, the following information will be returned.
 <img src="https://main.qcloudimg.com/raw/8ec26f2dd607232fc52b29c80868c364.png" width="433">
 
	If the return fails, please confirm:
	- Whether the event handler was entered incorrectly.
	- Whether the event was pulled more than 30 seconds ago.
4. After 5 minutes, use the API tool <!--api (https://intl.cloud.tencent.com/document/product/266/33433#API-Explorer)--> to run the `PullEvents` command again to pull event notifications.

  <img src="https://main.qcloudimg.com/raw/3d064849187be7c5d2c2da1f560e7b4a.png" width="462">

 If a **ResourceNotFound** error is returned, there are no more notifications that can be pulled.

