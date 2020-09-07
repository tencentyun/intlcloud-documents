## Overview

### Introduction

This document describes how to upload a video file on your local server to VOD.

### Fees

The code provided in this document is open-source and free of charge, but it may incur the following fees during use:

- Fees for purchasing a Tencent Cloud CVM instance to run the upload script. For more information, please see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).

## Uploading Video in CVM to VOD

### Step 1. Prepare a CVM instance<span id="p1"></span>

The upload script needs to be executed on a CVM instance meeting the following requirements:

- Region: not limited.
- Model: the minimum official configuration (1 CPU core and 1 GB memory) is sufficient.
- Public network: a public IP is required, and the bandwidth should be at least 1 Mbps.
- Operating system: official public image `Ubuntu Server 16.04.1 LTS 64-bit` or `Ubuntu Server 18.04.1 LTS 64-bit`.

For detailed directions on how to purchase a CVM instance and reinstall the system, please see [Operation Guide - Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and [Operation Guide - Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933), respectively.

>!If you do not have a CVM instance satisfying the above conditions, you can also run the script on another Linux (such as CentOS or Debian) or macOS server with public network access, but you need to modify certain commands in the script based on the operating system. Please search for the specific modification method by yourself.

### Step 2. Activate VOD<span id="p2"></span>

Please activate the VOD service as instructed in [Getting Started - Step 1](https://intl.cloud.tencent.com/document/product/266/8757).

### Step 3. Get the API key<span id="p3"></span>

Your API key (i.e., `SecretId` and `SecretKey`) is required for video upload. If you have not created an API key yet, please generate one as instructed in [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228). If you have already created a key, please get it as instructed in the same document.

### Step 4. Download the code and install the SDK<span id="p4"></span>

Log in to the CVM instance prepared in [step 1](#p1) as instructed in [Logging into Linux Instance in Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) and enter and run the following command on the remote terminal:

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/server_upload.sh
```

>?Please assign the corresponding values obtained in [step 3](#p3) to `SECRET_ID` and `SECRET_KEY` in the command.

This command will download the demo source code from GitHub and automatically run the installation script. The installation process will take several minutes (subject to the CVM network conditions), during which the remote terminal will print information similar to the following:

```
[2020-06-23 19:56:31] Start installing pip3.
[2020-06-23 19:56:34] pip3 is successfully installed.
[2020-06-23 19:56:34] Start installing the VOD upload SDK for Python.
[2020-06-23 19:56:36] The VOD upload SDK for Python is successfully installed.
[2020-06-23 19:56:36] Start configuring SDK parameters.
[2020-06-23 19:56:36] SDK parameter configuration is completed.
```

### Step 5. Upload a video<span id="p5"></span>

Before initiating upload, you need to prepare a video file and a cover image (optional) on your CVM instance. If it is inconvenient for you to upload a video to the CVM instance, you can run the following command on the remote terminal to download the test video and cover onto the CVM instance:

```
ubuntu@VM-69-2-ubuntu:~$ wget http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/7a9b2b565285890804459281865/v.f100010.mp4 -O ~/vod-server-demo/server_upload/tencent_cloud.mp4; wget http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/5285890804459940825.jpg -O ~/vod-server-demo/server_upload/tencent_cloud.jpg
```

Run the `server_upload.py` script to initiate upload:

```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/server_upload/; python3 server_upload.py ./tencent_cloud.mp4 ./tencent_cloud.jpg
```

>?Please replace the paths of the video and cover image in the command with the actual file paths. Here, the cover image path parameter is optional, and if it is left empty, the uploaded video will have no cover.

This command will upload the `tencent_cloud.mp4` video to VOD and upload the `tencent_cloud.jpg` image as its cover. After the upload is completed, the remote terminal will print information similar to the following:

```
{"CoverUrl": "http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/5285890804459940825.jpg", "FileId": "5285890804459940822", "MediaUrl": "http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/f0.mp4", "RequestId": "84a7fb42-9f05-4acd-9cc8-843690b188ce"}
```

>?If you want to use your own video for test, we recommend you use a small video file (of several megabytes in size) to avoid taking too much time for upload due to insufficient CVM bandwidth.

### Step 6. View the result<span id="p6"></span>

On the [Video Management](https://console.cloud.tencent.com/vod/media) page in the console, you can see the uploaded video file and cover.

## Code Interpretation

1. `main()` is the script entry.
2. Call `parse_conf_file()` and read the configuration information from the `config.json` file. The configuration items are as described below:
<table>
<thead>
<tr>
<th>Field</th>
<th>Data Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>secret_id</td>
<td>String</td>
<td>API key</td>
</tr>
<tr>
<td>secret_key</td>
<td>String</td>
<td>API key</td>
</tr>
<tr>
<td>procedure</td>
<td>String</td>
<td>Task flow name. The specified task flow will be automatically triggered after video upload is completed. It is empty by default</td>
</tr>
<tr>
<td>subappid</td>
<td>String</td>
<td>Whether to upload the video to a <a href="https://intl.cloud.tencent.com/document/product/266/33987" target="_blank">VOD subapplication</a></td>
</tr>
</tbody></table>

	>?This demo supports only the `procedure` and `subappid` upload parameters. For the complete features, please see [SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917).
3. Get the local path of the video file to be uploaded and the path of the cover image (if any) from the command line parameters and call `upload_media()` to initiate upload:
```
       if len(sys.argv) < 2:
           usage()
           return
       video_path = sys.argv[1]
       cover_path = sys.argv[2] if len(sys.argv) > 2 else ""
   
       # Initiate upload
       rsp = upload_media(configuration, video_path, cover_path)
```
4. In `upload_media()`, use the method provided by the SDK for Python to construct an upload instance `client`, set upload parameters in `req`, and initiate upload:
   ```
           client = VodUploadClient(conf["secret_id"], conf["secret_key"])
           req = VodUploadRequest()
   
           req.MediaFilePath = video
           if cover != "":
               req.CoverFilePath = cover
           if conf["procedure"] != "":
               req.Procedure = conf["procedure"]
           req.SubAppId = int(conf["subappid"])
   
           rsp = client.upload("ap-guangzhou", req)
           return rsp
   ```
>!The first parameter (`"ap-guangzhou"`) in `client.upload()` is the access region of the upload instance rather than the storage region of the uploaded video. You can simply fix the parameter value as `"ap-guangzhou"`. If you want to specify the storage region for uploaded videos, please set the `req.StorageRegion` parameter.

## Other Features

The VOD SDK for upload from server supports other features such as setting the video name, category, and expiration time. For more information, please see the SDK development guide for the corresponding programming language:

- [Java](https://intl.cloud.tencent.com/document/product/266/33914)
- [C#](https://intl.cloud.tencent.com/document/product/266/33915)
- [PHP](https://intl.cloud.tencent.com/document/product/266/33916)
- [Python](https://intl.cloud.tencent.com/document/product/266/33917)
- [Go](https://intl.cloud.tencent.com/document/product/266/33919)

