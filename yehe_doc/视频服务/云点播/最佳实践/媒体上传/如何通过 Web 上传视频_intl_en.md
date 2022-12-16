## Overview

### Demo features

This demo shows you how to upload videos to VOD through the webpage. It builds two HTTP services based on SCF:

- The first service is used to receive a request from the browser to get the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922), calculate the signature, and return it.
- The second service uses VOD's [web upload SDK](https://intl.cloud.tencent.com/document/product/266/33924) to implement a page. You can access the page in a browser to upload local videos to VOD.

### Architecture and process

The system mainly involves four components: browser, API Gateway, SCF, and VOD. Here, API Gateway and SCF are the deployment objects of this demo as shown below:
<img src="https://main.qcloudimg.com/raw/a5243b83531f4a2d98a63970d1f7a1b3.png" width="500">

The main business process is as follows:

1. The browser requests SCF for an upload page.
2. You select a local video and click upload on the upload page, and the browser requests SCF for an upload signature.
3. The browser uses the upload signature to initiate an upload request to VOD and displays the upload result on the upload page after completion.

> ?The SCF code in the demo is developed based on Python 3.6. SCF also supports other programming languages such as Python 2.7, Node.js, Go, PHP, and Java for your choice as needed. For more information, please see [Development Guide](https://intl.cloud.tencent.com/document/product/583/11061).

### Fees

The VOD web upload demo (including the webpage code and service backend code) provided in this document is open-source and free of charge, but it may incur the following fees during service building and use:

- Fees for purchasing a Tencent Cloud CVM instance to run the service deployment script. For more information, please see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).
- Fees for using the upload page and signature distribution service provided by SCF. For more information, please see [Billing Mode](https://intl.cloud.tencent.com/document/product/583/12284) and [Free Tier](https://intl.cloud.tencent.com/document/product/583/12282).
- Fees for using Tencent Cloud API Gateway to provide public network APIs for SCF. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/628/11771).
- Fees for VOD storage of uploaded videos. For more information, please see [Pay-as-You-Go (Postpaid Daily Billing Cycle)](https://intl.cloud.tencent.com/document/product/266/14666).
- Fees for VOD traffic consumed by video playback. For more information, please see [Pay-as-You-Go (Postpaid Daily Billing Cycle)](https://intl.cloud.tencent.com/document/product/266/14666).

## Quick Deployment of Web Upload Demo

The web upload demo is deployed on SCF with a service entry provided by API Gateway. To make it easier for you to build services, we provide a quick deployment script as detailed below.
<span id="p1"></span>
### Step 1. Prepare a CVM instance

The deployment script needs to be executed on a CVM instance meeting the following requirements:

- Region: not limited.
- Model: the minimum official configuration (1 CPU core and 1 GB memory) is sufficient.
- Public network: a public IP is required, and the bandwidth should be at least 1 Mbps.
- Operating system: official public image `Ubuntu Server 16.04.1 LTS 64-bit` or `Ubuntu Server 18.04.1 LTS 64-bit`.

For detailed directions on how to purchase a CVM instance and reinstall the system, please see [Operation Guide - Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and [Operation Guide - Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933), respectively.

>!
>- **The web upload demo itself does not depend on CVM but only uses CVM to run the deployment script.**
>- If you do not have a CVM instance satisfying the above conditions, you can also run the script on another Linux (such as CentOS or Debian) or macOS server with public network access, but you need to modify certain commands in the deployment script based on the operating system. Please search for the specific modification method by yourself.

### Step 2. Activate VOD

Please activate the VOD service as instructed in [Getting Started - Step 1](https://intl.cloud.tencent.com/document/product/266/8757).

<span id="p3"></span>
### Step 3. Get the API key and APPID

Your API key (i.e., `SecretId` and `SecretKey`) and `APPID` are required for deploying and running the web upload demo service.
- If you have not created an API key yet, please generate one as instructed in [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228). If you have already created a key, please get it as instructed in the same document.
- You can view the `APPID` on the [Account Information](https://console.cloud.tencent.com/developer) page in the console.


### Step 4. Deploy the service backend and webpage

Log in to the [CVM instance prepared in step 1](#p1) as instructed in [Logging In to Linux Instance in Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) and enter and run the following command on the remote terminal:

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;export APPID=125xxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/web_upload_scf_en.sh
```
>?Please assign the corresponding values obtained in [step 3](#p3) to `SECRET_ID`, `SECRET_KEY`, and `APPID` in the command.

This command will download the demo source code from GitHub and automatically run the installation script. The installation process will take several minutes (subject to the CVM network conditions), during which the remote terminal will print the following information:

```
[2020-04-25 23:03:20] Start installing pip3.
[2020-04-25 23:03:23] pip3 is successfully installed.
[2020-04-25 23:03:23] Start installing Tencent Cloud SCF.
[2020-04-25 23:03:26] SCF is successfully installed.
[2020-04-25 23:03:26] Start configuring SCF.
[2020-04-25 23:03:28] SCF configuration is completed.
[2020-04-25 23:03:28] Start deploying the VOD client upload client signature distribution service.
[2020-04-25 23:03:40] The deployment of the VOD client upload signature distribution service is completed.
[2020-04-25 23:03:44] Start deploying the VOD web upload page.
[2020-04-25 23:03:53] The deployment of the VOD web upload page is completed.
[2020-04-25 23:03:53] Please access the following address in your browser to use the demo: https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/web_upload_html
```

<span id="p4"></span>Copy the address of the webpage in the output log (which is `https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/web_upload_html` in this example).

> !If the following warning is displayed in the output log, it is generally because the CVM instance cannot immediately parse the service domain name deployed just now. You can ignore this warning.
>```
>[2020-04-25 17:18:44] Warning: the client upload signature distribution service failed the test.
>```

### Step 5. Use the web upload demo

1. Access the address copied in [step 4](#p4) in a browser to start using the web upload demo.
2. Perform video upload operations on this page:
	1. Select a local video file (MP4 format is recommended).
	2. (Optional) Select a local cover image (in JPG or PNG format).
	3. (Optional) Enter the video name.
	4. Click **Start Upload** to upload the video.
3. After the upload is completed, the VOD media IDs (i.e., `fileId`) and URLs of the uploaded video and cover will be displayed at the bottom of the page.
You can view the uploaded video in the [VOD console](https://console.cloud.tencent.com/vod/media).

>?You can try out other features on the upload page as prompted.

## System Design Description

### API protocol and test

Both the **upload page** and **upload signature distribution** functions use API Gateway to provide APIs. The specific API protocol is as detailed below:

| Service | Function Name | API Form | Response Content |
| ------------ | --------------- | --------- | --------- |
| Upload page     | web_upload_html | HTTP GET  | HTML page |
| Upload signature distribution | ugc_upload_sign | HTTP POST | Upload signature |

<span id="p6"></span>
#### Upload page

You can access the [SCF service list](https://console.cloud.tencent.com/scf/list) to view the details of the upload page service:

>?
>- The two SCF functions used by the demo are deployed under the namespace `vod_demo` in the Guangzhou region.
>- You need to select the corresponding region and namespace in the console to view the deployed SCF functions.

Click the function name, select **Trigger Management** on the left, and **Access Path** on the right is the URL of the upload page. Click **API Service Name** to redirect to the corresponding API Gateway page.
To test the service, directly access the page URL in a browser to check whether the upload page is displayed normally.

#### Upload signature distribution

You can access the [SCF service list](https://console.cloud.tencent.com/scf/list) to view the details of the upload signature distribution service in the same way as detailed in [Upload page](#p6).

Click the function name, select **Trigger Management** on the left, and **Access Path** on the right is the URL of the service. Click **API Service Name** to redirect to the corresponding API Gateway page.
To test the service, manually send an HTTP request and run the following command on a Linux or macOS device with public network access (please modify the service URL according to the actual situation):
```
curl -d '' https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/ugc_upload_sign
```
If the service is normal, an upload signature will be returned. Below is a sample signature:
```
VYapc9EYdoZLzGx0CglRW4N6kuhzZWNyZXRJZD1BS0lEZk5xMzl6dG5tYW1tVzBMOXFvZERia25hUjdZa0xPM1UmY3VycmVudFRpbWVTdGFtcD0xNTg4NTg4MDIzJmV4cGlyZVRpbWU9MTU4ODU4ODYyMyZyYW5kb209MTUwNzc4JmNsYXNzSWQ9MCZvbmVUaW1lVmFsaWQ9MCZ2b2RTdWJBcHBJZD0w
```
You can also use third-party tools such as Postman to send HTTP requests. Please search for specific usage on the internet. 

### Upload page service code interpretation

1. `main_handler()` is the entry function.
2. Read the content of the `web_upload.html` file, which is the upload page content.
```
		html_file = open(HTML_FILE, encoding='utf-8')
		html = html_file.read()
```
3. Read configuration items from `config.json`, which refer to the content that you cannot predict when you write the SCF service and need to determine during the deployment process. The content is written into `config.json` in real time by the deployment script before deploying the upload page service.
```
		conf_file = open(CONF_FILE, encoding='utf-8')
		conf = conf_file.read()
		conf_json = json.loads(conf)
```
4. Call `render_template` and modify the upload page content according to the configuration information obtained in the previous step. The configuration items are expressed in the format of `"variable name": "value"` in the `config.json` file or in the format of `{variable name}` in the `web_upload.html` file. **When modifying them, please replace them with the specific values as detailed below.**
```
  def render_template(html, keys):
      """Replace the variables (in the format of `${variable name}`) in HTML with specific content."""
      for key, value in keys.items():
          html = html.replace("${" + key + "}", value)
      return html
```
<table>
<thead>
<tr>
<th>Variable</th>
<th>Description</th>
<th>Value Type</th>
<th>Value Source</th>
</tr>
</thead>
<tbody><tr>
<td>UGC_UPLOAD_SIGN_SERVER</td>
<td>Upload signature distribution service URL</td>
<td>String</td>
<td>Output by <a href="https://intl.cloud.tencent.com/document/product/583/36267" target="_blank">SCF CLI</a> after the deployment of the upload signature distribution service is completed.</td>
</tr>
</tbody></table>
5. Return the modified content of the upload page. For the formats and descriptions of the returned data, please see [Overview of API Gateway Trigger](https://intl.cloud.tencent.com/document/product/583/12513).
  ```
      return {
          "isBase64Encoded": False,
          "statusCode": 200,
          "headers": {'Content-Type': 'text/html'},
          "body": html
      }
  ```


### Upload signature distribution service code interpretation

1. `main_handler()` is the entry function.
2. Call `parse_conf_file()` and read the configuration information from the `config.json` file. The configuration items are as described below (for specific parameters, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922#.3Cspan-id-.3D.22p2.22.3E.3C.2Fspan.3E.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E)):
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
<td>sign_expire_time</td>
<td>Integer</td>
<td>Signature validity period in seconds</td>
</tr>
<tr>
<td>class_id</td>
<td>Integer</td>
<td>Category ID of the uploaded video. 0 indicates the default category</td>
</tr>
<tr>
<td>otp</td>
<td>Integer</td>
<td>Whether the signature is one-time</td>
</tr>
<tr>
<td>subappid</td>
<td>Integer</td>
<td>Whether to upload to a <a href="https://intl.cloud.tencent.com/document/product/266/33987" target="_blank">VOD subapplication</a></td>
</tr>
</tbody></table>
3. Call `parse_source_context()` to parse the `sourceContext` field in the request body, which can be passed through to the event notification receipt service during [video upload completion event notification](https://intl.cloud.tencent.com/document/product/266/33950) (not used in this demo).
>?This field is optional during the upload process. If you don't need this feature, you can ignore this part of the code.
4. Call the `generate_sign()` function to calculate the signature. For more information, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).
5. Return the signature. For the formats and descriptions of the returned data, please see [Overview of API Gateway Trigger](https://intl.cloud.tencent.com/document/product/583/12513).
  ```
      return {
          "isBase64Encoded": False,
          "statusCode": 200,
          "headers": {"Content-Type": "text/plain; charset=utf-8",
                      "Access-Control-Allow-Origin": "*",
                      "Access-Control-Allow-Methods": "POST,OPTIONS"},
          "body": str(signature, 'utf-8')
      }
  ```

