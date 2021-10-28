## Overview

### Introduction

This document describes how to pull an online video (provided in the form of URL) to VOD.

### Fees

The code provided in this document is open-source and free of charge, but it may incur the following fees during use:

- Fees for purchasing a Tencent Cloud CVM instance to run the API request script. For more information, please see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).

- VOD storage space will be taken up by uploaded videos via pulling. For more information, please see [Video Storage Pricing](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E).

### Limits

The pull from URL feature provided by VOD has the following limits:

- The URL should directly point to a video file but cannot be a link to a video website page.
- If the URL has a timestamp for hotlink protection, please make sure that the hotlink protection limits (such as the validity period and number of allowed access requests) are favorable; otherwise, the access may fail.
- URLs with referer hotlink protection enabled are not supported.
- DASH (MPD file type) is unsupported.
- If the pull object is an HLS (.m3u8 file type) file, the URIs of media segments (generally in .ts file type) should be relative paths without parameters.

## Upload by Pull in Console
<span id="p11"></span>
### Step 1. Activate VOD

Please activate the VOD service as instructed in [Getting Started - Step 1](https://intl.cloud.tencent.com/document/product/266/8757).
<span id="p12"></span>
### Step 2. Create a pull task

Go to the [upload page](https://console.cloud.tencent.com/vod/media/upload) in the VOD Console, select **Pull Video** as the upload method, click **Add a Row**, enter the URL of the video to be pulled (the [test URL](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) is used here as an example. Other configuration items are optional, which can be entered as needed), and click **Pull Video** in the bottom-left corner:

![](https://main.qcloudimg.com/raw/3871a2c05ca1f26f62e0518cb3943309.png)
>?The time it takes to pull a video is directly proportional to the video file size. We recommend you use a small video (of dozens of megabytes in size) for the test to avoid long wait.
<span id="p13"></span>
### Step 3. View the pull result

After waiting for one or two minutes (subject to the video file size), you can see the pulled video on the [Media Assets page](https://console.cloud.tencent.com/vod/media).

![](https://main.qcloudimg.com/raw/7329a44db45f6cc11fa48ac41ae9cf7c.png)
>?If the browser is stuck at the media assets page during the pull process, you need to refresh the page to view the pulled video.

## Calling TencentCloud API for Pull
<span id="p21"></span>
### Step 1. Prepare a CVM instance

The TencentCloud API request script needs to be executed on a CVM instance meeting the following requirements:

- Region: not limited.
- Model: the minimum official configuration (1 CPU core and 1 GB memory) is sufficient.
- Public network: a public IP is required, and the bandwidth should be at least 1 Mbps.
- Operating system: official public image `Ubuntu Server 16.04.1 LTS 64-bit` or `Ubuntu Server 18.04.1 LTS 64-bit`.

For detailed directions on how to purchase a CVM instance and reinstall the system, please see [Operation Guide - Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and [Operation Guide - Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933), respectively.

>!If you do not have a CVM instance satisfying the above conditions, you can also run the script on another Linux (such as CentOS or Debian) or macOS server with public network access, but you need to modify certain commands in the script based on the operating system. Please search for the specific modification method by yourself.
<span id="p22"></span>
### Step 2. Get the API key

Your API key (i.e., `SecretId` and `SecretKey`) is required for TencentCloud API request. If you have not created an API key yet, please generate one as instructed in [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228). If you have already created a key, please get it as instructed in the same document.
<span id="p23"></span>
### Step 3. Activate VOD

Please activate the VOD service as instructed in [Getting Started - Step 1](https://intl.cloud.tencent.com/document/product/266/8757).
<span id="p24"></span>
### Step 4. Initiate a pull task

Log in to the CVM instance prepared in [step 1](#p21) as instructed in [Logging into Linux Instance in Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) and enter and run the following command on the remote terminal:

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/pull_upload_api.sh
```

>?Please assign the corresponding values obtained in [step 2](#p22) to `SECRET_ID` and `SECRET_KEY` in the command.

This command will download the demo source code from GitHub and automatically run the installation script. The installation process will take several minutes (subject to the CVM network conditions), during which the remote terminal will print the following information:

```
[2020-07-15 17:40:13] Start installing pip3.
[2020-07-15 17:40:39] pip3 is successfully installed.
[2020-07-15 17:40:39] Start installing the TencentCloud API SDK for Python.
[2020-07-15 17:40:42] The TencentCloud API SDK for Python is successfully installed.
[2020-07-15 17:40:42] Start configuring API parameters.
[2020-07-15 17:40:42] API parameter configuration is completed.
```

Run the `pull_upload.py` script to initiate upload:

```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/pull_upload_api/; python3 pull_upload.py http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4 API-PullUpload
```

>?Please replace the URL in the command with the actual address of the video to be pulled.

This command will initiate a [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118) request to the specified URL and print the response similar to the following:

```
{"TaskId": "1400329073-PullUpload-4ea60158fc6f8e611bbfa750eb1fd0a9t0", "RequestId": "4e821b4a-9a29-409f-99cb-b703fa184e50"}
```
<span id="p25"></span>
### Step 5. View the pull result

After waiting for one or two minutes (subject to the video file size), you can see the pulled video on the [Media Assets page](https://console.cloud.tencent.com/vod/media).

![](https://main.qcloudimg.com/raw/b5d62be7e0f70654483513a6885ff65b.png)
> ?If the browser is stuck at the media assets page during the pull process, you need to refresh the page to view the pulled video.
