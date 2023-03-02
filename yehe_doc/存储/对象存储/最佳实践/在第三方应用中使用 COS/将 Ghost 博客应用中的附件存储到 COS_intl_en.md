## Overview
[Ghost](https://ghost.org/docs) is a Node.js-based framework for quickly building a blog website. You can use its official CLI tool to quickly generate your personal website and deploy it in CVM or Docker.

As a blog website, attachment upload is a necessary feature. Ghost stores attachments locally by default. This document describes how to save an attachment in [COS](https://www.tencentcloud.com/products/cos) through the plugin. Saving forum attachments in COS has the following benefits:
- Higher reliability for your attachments.
- No need to prepare additional storage capacity on your server for forum attachments.
- Faster access to image attachments through the COS server rather than taking up downstream bandwidth/increasing the traffic on your own server.
- Accelerated forum user access to image attachments through [CDN](https://www.tencentcloud.com/products/cdn).

## Preparations

### Building a Ghost website

1. Install the [Node.js](https://nodejs.org/en/download/) environment.
2. Install ghost-cli.
```js
npm install ghost-cli@latest -g
```
3. Create a project and run the following command in the project's root directory:
```js
ghost install local
```
After successful creation, the project structure is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/76e74eff7779379f2e40c5c9220453fc.jpg)
4. Open the browser and access `localhost:2368`. On the sign-up page, sign up for an account and go to the management backend.
![](https://qcloudimg.tencent-cloud.cn/raw/16c412b34d8d9eda9525d12b7e34f5cf.jpg)


### Creating a COS bucket

1. In the [COS console](https://console.cloud.tencent.com/cos/bucket), create a bucket with access permissions of **public read/private write** as instructed in [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309).
2. Click **Security Management** > **CORS (Cross-Origin Resource Sharing)** and add a CORS configuration as instructed in [Setting Cross-Origin Resource Sharing (CORS)](https://intl.cloud.tencent.com/document/product/436/13318). You can use the following configuration to facilitate debugging:




## Associating Ghost with a COS Bucket

>!We recommend you use a sub-account key and follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) to reduce risks. For information about how to obtain a sub-account key, see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675).


1. Add the following configuration to the `config.development.json` configuration file in the Ghost project's root directory:
```json
  "storage": {
    "active": "ghost-cos-store",
    "ghost-cos-store": {      
      "BasePath": "ghost/", // You can change it to your directory name. If you leave it empty, the root directory will be used by default. 
      "SecretId": "AKID*************",
      "SecretKey": "***************",
      "Bucket": "xxx-125********", 
      "Region": "**-*******"
    }
  }
```
The parameters are described as follows:
<table>
   <tr>
      <th width="0%" >Configuration Item</td>
      <th width="0%" >Value</td>
   </tr>
   <tr>
      <td>BasePath</td>
      <td>The COS path where files are stored. You can modify it as needed. If you leave it empty, the root directory will be used by default.</td>
   </tr>
   <tr>
      <td>SecretId</td>
      <td>Enter the access key information, which can be created and obtained on the <a href="https://console.cloud.tencent.com/capi">Manage API Key</a> page.</td>
   </tr>
   <tr>
      <td>SecretKey</td>
      <td>Your access key information, which can be created and obtained on the <a href="https://console.cloud.tencent.com/capi">Manage API Key</a> page.</td>
   </tr>
   <tr>
      <td>Bucket</td>
      <td>The name customized during bucket creation such as `examplebucket-1250000000`.</td>
   </tr>
   <tr>
      <td>Region</td>
      <td>The region selected during bucket creation</td>
   </tr>
</table>
2. Create a custom storage directory and run the following command in the project's root directory:
```js
mkdir -p content/adapters/storage
```
3. Install the [ghost-cos-store](https://github.com/tencentyun/ghost-cos-store) plugin provide by Tencent Cloud.
   1. Install it through npm.
```js
npm install ghost-cos-store
```
   2. Create the `ghost-cos-store.js` file with the following content in the `storage` directory:
```js
//  content/adapters/storage/ghost-cos-store.js
module.exports = require('ghost-cos-store');
```
   3. Run `git clone` for installation.
```js
cd content/adapters/storage
git clone https://github.com/tencentyun/ghost-cos-store.git
cd ghost-cos-store  
npm i
```
   4. After the installation, restart Ghost.
```js
ghost restart
```



## Publishing a Post and Testing Upload

1. In the Ghost console, click **+** to publish a post.
![](https://qcloudimg.tencent-cloud.cn/raw/27dc54b218009f64bd319707700dba71.jpg)
2. Click **+** to upload an image. From the packets captured by the browser, you can see that the `upload` request succeeds and the COS URL of the image is returned.



