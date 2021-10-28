

## Overview

### Demo features
This demo describes how to use the [key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986) mechanism of VOD, including enabling key hotlink protection in the console, building a hotlink protection signature distribution service, and playing back a video with a hotlink protection signature.

### Architecture and process

An HTTP service is built based on SCF in the demo to receive the requests for getting hotlink protection signatures from clients. It gets the original URL of a video in VOD from the request body, calculates a signature, and returns the URL with the signature to the client.

The system mainly involves four components: developer (you), API Gateway, SCF, and VOD. Here, API Gateway and SCF are the deployment objects of this demo as shown below:
<img src="https://main.qcloudimg.com/raw/f30d9b832b388c9ffe35551ef26743b4.png" width="600">

The specific business process is as follows:

1. Get the original URL of the video in the VOD Console (in the actual production environment, it should be the player that requests the video URL from the business backend; to simplify the process, this document takes your operation as an example to simulate such business behavior here).
2. Use the original URL of the video to request a hotlink protection signature from SCF.
3. Use the video URL with the hotlink protection signature to request VOD CDN to play back the video.

> ?The SCF code in the demo is developed based on Python 3.6. SCF also supports other programming languages such as Python 2.7, Node.js, Go, PHP, and Java for your choice as needed. For more information, please see [Development Guide](https://intl.cloud.tencent.com/document/product/583/11061).

### Fees
The VOD key hotlink protection signature distribution service demo provided in this document is open-source and free of charge, but it may incur the following fees during service building and use:

- Fees for purchasing a Tencent Cloud CVM instance to run the service deployment script. For more information, please see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).
- Fees for using signature distribution service provided by SCF. For more information, please see [Billing Mode](https://intl.cloud.tencent.com/document/product/583/12284) and [Free Tier](https://intl.cloud.tencent.com/document/product/583/12282).
- Fees for using Tencent Cloud API Gateway to provide public network APIs for SCF. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/628/11771).
- Fees for VOD storage of uploaded videos.
- VOD storage space will be taken up by uploaded videos. For more information, please see [Video Storage Pricing](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E).

## Quickly Deploying Key Hotlink Protection Signature Distribution Service
<span id="p1"></span>
### Step 1. Prepare a CVM instance

The deployment script needs to be executed on a CVM instance meeting the following requirements:

- Region: not limited.
- Model: the minimum official configuration (1 CPU core and 1 GB memory) is sufficient.
- Public network: a public IP is required, and the bandwidth should be at least 1 Mbps.
- Operating system: official public image `Ubuntu Server 16.04.1 LTS 64-bit` or `Ubuntu Server 18.04.1 LTS 64-bit`.

For detailed directions on how to purchase a CVM instance and reinstall the system, please see [Operation Guide - Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and [Operation Guide - Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933), respectively.

>!
>- The key hotlink protection signature distribution service demo itself does not depend on CVM but only uses CVM to run the deployment script.
>- If you do not have a CVM instance satisfying the above conditions, you can also run the script on another Linux (such as CentOS or Debian) or macOS server with public network access, but you need to modify certain commands in the deployment script based on the operating system. Please search for the specific modification method by yourself.
<span id="p2"></span>
### Step 2. Activate VOD and configure key hotlink protection

1. Activate the VOD service as instructed in [Getting Started - Step 1](https://intl.cloud.tencent.com/document/product/266/8757).
2. After activation, enable key hotlink protection as instructed in [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/14060) and record the hotlink protection key:
![](https://qcloudimg.tencent-cloud.cn/raw/c43642ea12afda47aff5ca5205f63f4f.png)
>!Here, enable key hotlink protection instead of referer hotlink protection. If you enable referer hotlink protection at the same time, the request may fail as the test method below does not meet the corresponding requirements.
<span id="p3"></span>
### Step 3. Get the API key and APPID

Your API key (i.e., `SecretId` and `SecretKey`) and `APPID` are required for deploying and running the key hotlink protection signature distribution service demo.

- If you have not created an API key yet, please generate one as instructed in [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228). If you have already created a key, please get it as instructed in the same document.
- You can view the `APPID` on the [Account Information](https://console.cloud.tencent.com/developer) page in the console as shown below:
  ![](https://main.qcloudimg.com/raw/6c9fe4238232392c8d914f9ebf0f53aa.png)

### Step 4. Deploy the hotlink protection signature distribution service

Log in to the [CVM instance prepared in step 1](#p1) as instructed in [Logging into Linux Instance in Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) and enter and run the following command on the remote terminal:

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;export APPID=125xxxxxxx;export ANTI_LEECH_KEY=xxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/anti_leech_sign_scf.sh
```

>?Please assign the corresponding values obtained in [step 3](#p3) to `SECRET_ID`, `SECRET_KEY`, and `APPID` in the command and assign the hotlink protection key obtained in [step 2](#p2) to `ANTI_LEECH_KEY`.

This command will download the demo source code from GitHub and automatically run the installation script. The installation process will take several minutes (subject to the CVM network conditions), during which the remote terminal will print the following information:

```
[2020-06-04 15:57:10] Start installing pip3.
[2020-06-04 15:57:18] pip3 is successfully installed.
[2020-06-04 15:57:18] Start installing Tencent Cloud SCF.
[2020-06-04 15:57:19] SCF is successfully installed.
[2020-06-04 15:57:19] Start configuring SCF.
[2020-06-04 15:57:20] SCF configuration is completed.
[2020-06-04 15:57:20] Start deploying the VOD key hotlink protection signature distribution service.
[2020-06-04 15:57:30] The deployment of the VOD key hotlink protection signature distribution service is completed.
[2020-06-04 15:57:32] Service address: https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/anti_leech_sign
```

Copy the address of the signature distribution service in the output log (which is `https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/anti_leech_sign` in this example).

> !If the following warning is displayed in the output log, it is generally because the CVM instance cannot immediately parse the service domain name deployed just now. You can ignore this warning.
> ```
> [2020-04-25 17:18:44] Warning: the key hotlink protection signature distribution service failed the test.
> ```

### Step 5. Test key hotlink protection

Upload a test video to VOD as instructed in [Uploading Video - Local Upload](https://intl.cloud.tencent.com/document/product/266/33890). After the video is uploaded, click **Quick View** and click **Copy Address** on the right to copy the video URL.
![](https://qcloudimg.tencent-cloud.cn/raw/ac27b65a2bb0cc91ac9f71b141a31cb2.png)
On the command line on the CVM instance, run the `curl` command to try directly accessing this URL. The access will be rejected by the server for non-compliance with the key hotlink protection rule, and the HTTP return code will be 403 (during the test, please replace the URL in the command with the actual URL, which also applies below):

```
ubuntu@VM-69-2-ubuntu:~$ curl -I "http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4"
HTTP/1.1 403 Forbidden
Server: NWS_VP
Connection: keep-alive
Date: Thu, 04 Jun 2020 08:27:54 GMT
Content-Type: text/plain
Content-Length: 14
```
On the command line on the CVM instance, run the `curl` command to request the URL with the hotlink protection signature from the service deployed in step 4 (`-d` means to initiate the request in POST method, and the carried parameter is the video URL):
```
ubuntu@VM-69-2-ubuntu:~$ curl -d 'http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4' https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/anti_leech_sign; echo
http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4?t=5ed8b8d2&exper=0&rlimit=0&us=455041&sign=fe6394007c2e7aef39fc70a02e897f69
```
Run the `curl` command again to access the URL with the hotlink protection signature obtained in the previous step, and the URL can be accessed normally (the HTTP return code will be 200):
```
ubuntu@VM-69-2-ubuntu:~$ curl -I "http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4?t=5ed8b8d2&exper=0&rlimit=0&us=455041&sign=fe6394007c2e7aef39fc70a02e897f69"
HTTP/1.1 200 OK
Server: tencent-cos
Connection: keep-alive
Date: Thu, 04 Jun 2020 08:37:17 GMT
Last-Modified: Fri, 22 May 2020 15:06:15 GMT
Content-Type: video/mp4
Content-Length: 232952632
Accept-Ranges: bytes
ETag: "1da6be3a0d1da5edae4ff0b1feff02cf-223"
x-cos-hash-crc64ecma: 16209801220610226954
x-cos-request-id: NWVkOGIyYmVfZDUyMzYyNjRfYWMwMF85YjkyNzA=
X-Daa-Tunnel: hop_count=4
X-NWS-LOG-UUID: b404f43e-3c86-4c54-8a78-fb78e4e85cf2 add71e19fb08c6d9dbe1b21a2fb157bf
Access-Control-Allow-Credentials: true
Access-Control-Allow-Headers: Origin,No-Cache,X-Requested-With,If-Modified-Since,Pragma,Last-Modified,Cache-Control,Expires,Content-Type,X_Requested_With,Range
Access-Control-Allow-Methods: GET,POST,OPTIONS
Access-Control-Allow-Origin: *
```
>?You can access the URL with the hotlink protection signature in a browser and verify the signature by playing back the video. However, this method has certain requirements for the video format. Generally, H.264-encoded .mp4 videos have high compatibility, which are recommended. You can also use a third-party tool such as Postman to send HTTP requests for test. Please search for the specific usage by yourself. 

## System Design Description

### API protocol

The key hotlink protection signature distribution function uses API Gateway to provide APIs. The specific API protocol is as detailed below:

| Service | Function Name | API Form | Request Content | Response Content |
| ------------------ | --------------- | --------- | ------------ | ---------------- |
| Key hotlink protection signature distribution | anti_leech_sign | HTTP POST | Original video URL | URL with hotlink protection signature |

### Signature distribution service code interpretation

1. `main_handler()` is the entry function.
2. Call `parse_conf_file()` and read the configuration information from the `config.json` file. The configuration items are as described below (for specific parameters, please see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)):
<table>
<thead>
<tr>
<th>Field</th>
<th>Data Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>key</td>
<td>String</td>
<td>Key hotlink protection key</td>
</tr>
<tr>
<td>t</td>
<td>Integer</td>
  <td>Signature validity period in seconds. When a request is being processed, this parameter plus the current time on the SCF server will be `t` in the hotlink protection parameters</td>
</tr>
<tr>
<td>exper</td>
<td>Integer</td>
<td>Preview duration</td>
</tr>
<tr>
<td>rlimit</td>
<td>Integer</td>
<td>Maximum number of client IPs that can access the signature</td>
</tr>
</tbody></table>
3. Parse the `Dir` parameter from the request body, generate the `t` and `us` parameters locally, and read the `exper` and `rlimit` parameters from the configuration file:
```
       original_url = event["body"]
       parse_result = urlparse(original_url)
       directory = path.split(parse_result.path)[0] + '/'
       # Signature parameters
       timestamp = int(time.time())
       rand = random.randint(0, 999999)
       sign_para = {
           "t": hex(timestamp + configuration['t'])[2:],
           "exper": configuration['exper'],
           "rlimit": configuration['rlimit'],
           "us": rand
       }	
```
4. Call `generate_sign()` to calculate the hotlink protection signature. For the specific algorithm, please see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F).
5. Generate the `QueryString` and add it at the end of the original URL to concatenate a URL with the hotlink protection signature:
```
       sign_para["sign"] = signature
       query_string = urlencode(sign_para)
       new_parse_result = parse_result._replace(query=query_string)
       signed_url = urlunparse(new_parse_result)
```
6. Return the signature. For the formats and descriptions of the returned data, please see [Overview of API Gateway Trigger](https://intl.cloud.tencent.com/document/product/583/12513).
```
       return {
           "isBase64Encoded": False,
           "statusCode": 200,
           "headers": {"Content-Type": "text/plain; charset=utf-8",
                       "Access-Control-Allow-Origin": "*",
                       "Access-Control-Allow-Methods": "POST,OPTIONS"},
           "body": signed_url
       }
```

   
