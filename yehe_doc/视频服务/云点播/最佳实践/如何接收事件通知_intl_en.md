## Overview

### Demo features

This document uses the video upload and transcoding process as an example to describe how to use the [event notification mechanism](https://intl.cloud.tencent.com/document/product/266/33948) of VOD.

### Architecture and process

An HTTP service is built based on SCF in the demo to receive event notification requests from VOD. It initiates video transcoding and gets the transcoding result by processing `NewFileUpload` ([video upload completion](https://intl.cloud.tencent.com/document/product/266/33950)) and `ProcedureStateChanged` ([task flow status change](https://intl.cloud.tencent.com/document/product/266/33953)) event notifications.

The system mainly involves four components: console, API Gateway, SCF, and VOD. Here, API Gateway and SCF are the deployment objects of this demo as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/ec5a27df9988417547c884df4ac28816.png" width="550">

The specific business process is as follows:

1. Upload a video to VOD in the console.
2. The VOD backend initiates the `NewFileUpload` event notification request to the demo.
3. The demo parses the event notification content and calls the [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) API of VOD to initiate transcoding for the uploaded video with the `100010` and `100020` [preset transcoding templates](https://intl.cloud.tencent.com/document/product/266/33932).
4. After completing the transcoding task, VOD initiates the `ProcedureStateChanged` event notification request to the demo.
5. The demo parses the event notification content and prints the URL of the transcoding output file into SCF logs.

> ?The SCF code in the demo is developed based on Python 3.6. SCF also supports other programming languages such as Python 2.7, Node.js, Go, PHP, and Java for your choice as needed. For more information, please see [Development Guide](https://intl.cloud.tencent.com/document/product/583/11061).

### Fees

The VOD event notification receipt service demo provided in this document is open-source and free of charge, but it may incur the following fees during service building and use:

- Fees for purchasing a Tencent Cloud CVM instance to run the service deployment script. For more information, please see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).
- Fees for using signature distribution service provided by SCF. For more information, please see [Billing Mode](https://intl.cloud.tencent.com/document/product/583/12284) and [Free Tier](https://intl.cloud.tencent.com/document/product/583/12282).
- Fees for using Tencent Cloud API Gateway to provide public network APIs for SCF. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/628/11771).
- VOD storage space will be taken up by uploaded videos. For more information, please see [Video Storage Pricing](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E).
- VOD transcoding service will be used for video transcoding. For more information, please see [Video Transcoding Pricing](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E).

<span id="p0"></span>
### Avoiding affecting production environment

The business logic of the event notification receipt service demo uses the VOD event notification mechanism; therefore, you need to set the event notification address during deployment. If there is already a VOD-based production environment under your account, changing the event notification address may cause business exceptions. **Before doing so, please confirm that this will not affect the production environment. If you are not sure, please use a new account to deploy the demo.**

## Quickly Deploying Event Notification Receipt Service
<span id="p1"></span>
### Step 1. Prepare a CVM instance

The deployment script needs to be executed on a CVM instance meeting the following requirements:

- Region: not limited.
- Model: the minimum official configuration (1 CPU core and 1 GB memory) is sufficient.
- Public network: a public IP is required, and the bandwidth should be at least 1 Mbps.
- Operating system: official public image `Ubuntu Server 16.04.1 LTS 64-bit` or `Ubuntu Server 18.04.1 LTS 64-bit`.

For detailed directions on how to purchase a CVM instance and reinstall the system, please see [Operation Guide - Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and [Operation Guide - Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933), respectively.

>!
>- The event notification receipt service demo itself does not depend on CVM but only uses CVM to run the deployment script.
>- If you do not have a CVM instance satisfying the above conditions, you can also run the script on another Linux (such as CentOS or Debian) or macOS server with public network access, but you need to modify certain commands in the deployment script based on the operating system. Please search for the specific modification method by yourself.
<span id="p2"></span>
### Step 2. Activate VOD

Activate the VOD service as instructed in [Getting Started - Step 1](https://intl.cloud.tencent.com/document/product/266/8757).
<span id="p3"></span>
### Step 3. Get the API key and APPID

Your API key (i.e., `SecretId` and `SecretKey`) and `APPID` are required for deploying and running the event notification receipt service demo.

- If you have not created an API key yet, please generate one as instructed in [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228). If you have already created a key, please get it as instructed in the same document.
- You can view the `APPID` on the [Account Information](https://console.cloud.tencent.com/developer) page in the console as shown below:
  ![](https://main.qcloudimg.com/raw/6c9fe4238232392c8d914f9ebf0f53aa.png)
<span id="p4"></span>
### Step 4. Deploy the event notification receipt service

Log in to the [CVM instance prepared in step 1](#p1) as instructed in [Logging into Linux Instance in Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) and enter and run the following command on the remote device:

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;export APPID=125xxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/callback_scf_en.sh
```

>?Please assign the corresponding values obtained in [step 3](#p3) to `SECRET_ID`, `SECRET_KEY`, and `APPID` in the command.

This command will download the demo source code from GitHub and automatically run the installation script. The installation process will take several minutes (subject to the CVM network conditions), during which the remote device will print the following information:

```
[2020-06-05 17:16:08] Start checking npm.
[2020-06-05 17:16:12] npm is successfully installed.
[2020-06-05 17:16:12] Start installing ServerLess.
[2020-06-05 17:16:13] ServerLess is successfully installed.
[2020-06-05 17:16:14] Start deploying the event notification receipt service of VOD.
[2020-06-05 17:16:24] The event notification receipt service of VOD is deployed.
[2020-06-05 17:16:26] Service address: https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/callback
```

Copy the address of the event notification receipt service in the output log (which is `https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/callback` in this example).

> !If the following warning is displayed in the output log, it is generally because the CVM instance cannot immediately parse the service domain name deployed just now. You can ignore this warning.
> ```
> [2020-04-25 17:18:44] Warning: the event notification receipt service failed the test.
> ```

### Step 5. Configure the event notification address

As described in [Avoiding affecting production environment](#p0), please confirm that your business in the production environment does not depend on VOD event notifications before performing the following operations:

Log in to the [VOD console](https://console.cloud.tencent.com/vod/callback), click **Set**, select **Normal Callback** as the event notification method, enter the event notification receipt service address obtained in [step 4](#p4) as the callback URL, select all callback events, and click **Confirm** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0e5631bc9013b6e30283a7ac5411e332.png)

>!If two callback URL configuration items (v2.0 format and v3.0 format) are displayed at the same time in the console, please configure the v3.0 one.

### Step 6. Test the demo

Upload a test video to VOD as instructed in [Uploading Video - Local Upload](https://intl.cloud.tencent.com/document/product/266/33890). Select the default option "No Processing After Upload" during the upload. After the upload is completed, you can see that the video status is "Processing" on the "Uploaded" tab, which indicates that the demo has received the `NewFileUpload` event notification and initiated a transcoding request.

Wait for the video processing to complete (indicated by the "Normal" status), click **Quick View**, and you can see that there are two output videos for the uploaded video on the right of the page.

Log in to the SCF Console and enter the [log page](https://console.cloud.tencent.com/scf/list-detail?rid=1&ns=vod_demo&id=callback&menu=log) to view the SCF logs. In the latest log, you can see that the URLs of the two output files have been printed out. In actual use cases, you can use SCF to record the URLs in your database or publish them to viewers through other channels.

>?SCF log generation may have a certain delay. If no logs are displayed on the page, please wait for one or two minutes and click **Reset** to refresh.
<span id="design"></span>
## System Design Description

### API protocol

The event notification receipt function uses API Gateway to provide APIs. For the specific API protocols, please see [Video Upload Completion](https://intl.cloud.tencent.com/document/product/266/33950) and [Task Flow Status Change](https://intl.cloud.tencent.com/document/product/266/33953).

### Event notification receipt service code interpretation

1. `main_handler()` is the entry function.
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
<td>region</td>
<td>String</td>
<td>TencentCloud API request region, which can be any region for VOD</td>
</tr>
<tr>
<td>definitions</td>
<td>Integer Array</td>
<td>Transcoding template</td>
</tr>
<tr>
<td>subappid</td>
<td>Integer</td>
<td>Whether the event notification is from a <a href="https://intl.cloud.tencent.com/document/product/266/33987" target="_blank">VOD subapplication</a></td>
</tr>
</tbody></table>
3. For `NewFileUpload` event notifications, call `deal_new_file_event()` to parse the request and get the `FileId` of the newly uploaded video from it.
```
           if event_type == "NewFileUpload":
               fileid = deal_new_file_event(body)
               if fileid is None:
                   return ERR_RETURN
```
4. Call `trans_media()` to initiate transcoding, output the TencentCloud API's response packets to SCF logs, and send the response packets to the event notification service of VOD.
```
               rsp = trans_media(configuration, fileid)
               if rsp is None:
                   return ERR_RETURN
               print(rsp)
```
5. In `trans_media()`, call the TencentCloud API SDK to initiate the `ProcessMedia` request:
```
        cred = credential.Credential(conf["secret_id"], conf["secret_key"])
        client = vod_client.VodClient(cred, conf["region"])

        method = getattr(models, API_NAME + "Request")
        req = method()
        req.from_json_string(json.dumps(params))

        method = getattr(client, API_NAME)
        rsp = method(req)
        return rsp
```
6. For `ProcedureStateChanged` event notifications, call `deal_procedure_event()` to parse the request to get the transcoding output video URL and print it to SCF logs:
```
           elif event_type == "ProcedureStateChanged":
               rsp = deal_procedure_event(body)
               if rsp is None:
                   return ERR_RETURN
```

   
