

## Overview

### Introduction

This document describes how to transcode a video in VOD and get the transcoding output result.

### Fees

The code provided in this document is open-source and free of charge, but it may incur the following fees during use:

- Fees for purchasing a Tencent Cloud CVM instance to run the TencentCloud API request script. For more information, please see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).

## Initiating Transcoding in Console

### Step 1. Activate VOD<span id="p11"></span>

Please activate the VOD service as instructed in [Getting Started - Step 1](https://intl.cloud.tencent.com/document/product/266/8757).

### Step 2. Upload a video<span id="p12"></span>

Upload a test video as instructed in [Getting Started - Step 2](https://intl.cloud.tencent.com/document/product/266/8757). Click [here](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) to view the test video used in the demo. The corresponding `FileId` is `5285890804162014755` as shown below:
![](https://main.qcloudimg.com/raw/f8aa62bd40ab37b8cdd371798d4ff1e9.png)
>?We recommend you use a short video file (of dozens of seconds in duration) for the test to avoid taking too much time for transcoding.

### Step 3. Initiate transcoding<span id="p13"></span>

Check the uploaded test video on the [Video Management](https://console.cloud.tencent.com/vod/media) page in the console and click **Process Video**:
![](https://main.qcloudimg.com/raw/cf6d8e0fa032b2a76acfd918cf5c3146.png)
In the pop-up window, select **Transcoding** as the processing type and click **Transcoding Template**:
![](https://main.qcloudimg.com/raw/fc857eebabee8b5c547774fed0fe2814.png)
Select the desired transcoding template and click **OK**. This demo uses the preset templates `MP4-FLU` (ID: 100010) and `MP4-SD` (ID: 100020) as examples. You can also use a custom template as instructed in [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059).
![](https://main.qcloudimg.com/raw/e82be691470090beccf1ea27dbdcb4c3.png)
Click **OK** to initiate transcoding:
![](https://main.qcloudimg.com/raw/f52ec218600e19af3e42359a90d03298.png)
On the "Video Management" page, you can see that the test video status is "Processing", which indicates that the video is being transcoded:
![](https://main.qcloudimg.com/raw/30d3c90f55970568f55ce09be4cdb32b.png)

### Step 4. View the transcoding result<span id="p14"></span>

On the [Video Management](https://console.cloud.tencent.com/vod/media) page in the console, wait for the test video status to become "Normal", which indicates that the transcoding is completed. Then, click **Manage** on the right of the test video to enter the video management page:
![](https://main.qcloudimg.com/raw/694f1b000cea813d12397fcb1c3a86a0.png)
In the **Standard Transcoding List** on the "Basic Information" tab, videos in `MP4-FLU` and `MP4-SD` specifications are output. You can click **Preview** on the right to directly watch the corresponding video. You can also click **Copy Address** to copy the URL of the corresponding output video and publish it to viewers through other channels.
![](https://main.qcloudimg.com/raw/38db47dcfbd840bd6d67478ce42fd1cd.png)

## Calling TencentCloud API to Initiate Transcoding

### Step 1. Prepare a CVM instance<span id="p21"></span>

The TencentCloud API request script needs to be executed on a CVM instance meeting the following requirements:

- Region: not limited.
- Model: the minimum official configuration (1 CPU core and 1 GB memory) is sufficient.
- Public network: a public IP is required, and the bandwidth should be at least 1 Mbps.
- Operating system: official public image `Ubuntu Server 16.04.1 LTS 64-bit` or `Ubuntu Server 18.04.1 LTS 64-bit`.

For detailed directions on how to purchase a CVM instance and reinstall the system, please see [Operation Guide - Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and [Operation Guide - Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933), respectively.

>!If you do not have a CVM instance satisfying the above conditions, you can also run the script on another Linux (such as CentOS or Debian) or macOS server with public network access, but you need to modify certain commands in the script based on the operating system. Please search for the specific modification method by yourself.

### Step 2. Get the API key<span id="p22"></span>

Your API key (i.e., `SecretId` and `SecretKey`) is required for TencentCloud API request. If you have not created an API key yet, please generate one as instructed in [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228). If you have already created a key, please get it as instructed in the same document.

### Step 3. Activate VOD<span id="p23"></span>

Please activate the VOD service as instructed in [Getting Started - Step 1](https://intl.cloud.tencent.com/document/product/266/8757).

### Step 4. Upload a video<span id="p24"></span>
Upload a test video as instructed in [Getting Started - Step 2](https://intl.cloud.tencent.com/document/product/266/8757). Click [here](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) to view the test video used in the demo. The corresponding `FileId` is `5285890804162014755` as shown below:
![](https://main.qcloudimg.com/raw/f8aa62bd40ab37b8cdd371798d4ff1e9.png)
>?We recommend you use a short video file (of dozens of seconds in duration) for the test to avoid taking too much time for transcoding.


### Step 5. Initiate transcoding<span id="p25"></span>

Log in to the CVM instance prepared in [step 1](#p21) as instructed in [Logging into Linux Instance in Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) and enter and run the following command on the remote terminal:
```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/transcode_api.sh
```
>?Please assign the corresponding values obtained in [step 2](#p22) to `SECRET_ID` and `SECRET_KEY` in the command.

This command will download the demo source code from GitHub and automatically run the installation script. The installation process will take several minutes (subject to the CVM network conditions), during which the remote terminal will print the following information:
```
  [2020-06-15 20:39:56] Start installing pip3.
  [2020-06-15 20:40:06] pip3 is successfully installed.
  [2020-06-15 20:40:06] Start installing the TencentCloud API SDK for Python.
  [2020-06-15 20:40:07] The TencentCloud API SDK for Python is successfully installed.
  [2020-06-15 20:40:07] Start configuring API parameters.
  [2020-06-15 20:40:07] API parameter configuration is completed.
```
Run the `process_media.py` script to initiate transcoding:
```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/transcode_api/; python3 process_media.py 5285890804162014755
```
>?Please replace `5285890804162014755` in the command with the actual `FileId` obtained in [step 4](#p24).

This command will initiate a [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) request to the `5285890804162014755` video so as to transcode it to two VOD [preset transcoding template](https://intl.cloud.tencent.com/document/product/266/33932) specifications (`100010` and `100020`) and print the request response content:
```
{"TaskId": "1400329073-procedurev2-f6bf6f01612369b6db30f2224792a2aft0", "RequestId": "809918fb-791c-4937-b684-5027ba6bc5f0"}
```

### Step 6. View the transcoding result<span id="p14"></span>

On the "Video Management" page, you can see that the test video status is "Processing", which indicates that the video is being transcoded:
![](https://main.qcloudimg.com/raw/30d3c90f55970568f55ce09be4cdb32b.png)
Wait for the test video status to become "Normal", which indicates that the transcoding is completed. Then, click **Manage** on the right of the test video to enter the video management page:
![](https://main.qcloudimg.com/raw/694f1b000cea813d12397fcb1c3a86a0.png)
In the **Standard Transcoding List** on the "Basic Information" tab, videos in `MP4-FLU` and `MP4-SD` specifications are output. You can click **Preview** on the right to directly watch the corresponding video. You can also click **Copy Address** to copy the URL of the corresponding output video and publish it to viewers through other channels.
![](https://main.qcloudimg.com/raw/38db47dcfbd840bd6d67478ce42fd1cd.png)

## Automatic Transcoding After Video Upload (Through Task Flow)

VOD provides multiple video upload methods such as upload through console, upload from server, upload from client, and pull from URL (for more information, please see [Overview](https://intl.cloud.tencent.com/document/product/266/9760)). All upload methods allow you to specify a [task flow](https://intl.cloud.tencent.com/document/product/266/33931), which can automatically trigger transcoding after the upload is completed.

## Automatic Transcoding After Video Upload (Through Event Notification)

After video upload or a transcoding task is completed, the VOD backend will initiate an [event notification](https://intl.cloud.tencent.com/document/product/266/33948) request. You can use the event notification mechanism to initiate transcoding for the newly uploaded video and automatically get the transcoding result through an event notification (the method of manually viewing the transcoding result in the console is as described above).