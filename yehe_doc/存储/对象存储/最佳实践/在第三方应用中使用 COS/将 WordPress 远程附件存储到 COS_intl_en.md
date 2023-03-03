## Overview

[WordPress](https://cn.wordpress.org/) is a blogging platform built with PHP. You can use it to build your own website on a server that supports PHP and MySQL databases, or simply as a content management system (CMS).

WordPress is a powerful, scalable, and easy-to-expand platform with a wide range of plugins. With third-party plug-ins, it offers everything that a website should have.

This document describes how to use a plugin to store remote attachments from the WordPress media library in [COS](https://www.tencentcloud.com/products/cos).

Since COS is highly scalable, reliable, secure, and cost-effective, storing your media library attachments in COS offers the following benefits:

- Higher reliability for your attachments.
- No need to prepare additional storage capacity on your server for attachments.
- Faster access to image attachments through the COS server rather than taking up downstream bandwidth/increasing the traffic on your own server.
- Accelerated user access to image attachments through [CDN](https://www.tencentcloud.com/products/cdn).



## Prerequisites

1. You have created a bucket; otherwise, create one as instructed in [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309).
2. You have created a server such as a CVM instance as instructed in [Cloud Virtual Machine](https://www.tencentcloud.com/document/product/213).


## Directions

### Deploying a WordPress website

To quickly build a WordPress website in CVM, you can deploy it via an image or manually. If you have high requirements for extensibility of your business website, you can deploy it manually as instructed in the following documents:

- [Building a WordPress Website (Linux)](https://intl.cloud.tencent.com/document/product/213/8044)
- [Building a WordPress Website (Windows)](https://intl.cloud.tencent.com/document/product/213/34806)

You can deploy a WordPress website via an image easily as follows:

1. Deploy a WordPress website via an image.
   1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index) and click **Create Instance** on the instance management page.
   2. Select a model as prompted. In **Instance Configuration** > **Image**, click **Image Marketplace** and select **Select from image marketplace**.
   3. In the **Image Marketplace** pop-up window, select **Basic Software** and enter **wordpress** for search.
   4. Select an image as needed. Here, **WordPress Blog Program\_v5.5.3(CentOS | LAMP)** is selected. Then, click **Free Trial**.
   5. After purchase, log in to the CVM console, associate the newly created instance with a security group, and open port 80 in the inbound rules.
2. On the CVM instance management page, copy the **public IP** of the instance and access `http://public IP/wp-admin` in your local browser to start installing the WordPress website:
   1. Select the WordPress language and click **Continue**.
   2. Enter the WordPress website title and admin username, password, and email address.
   3. Click **Install WordPress**.
   4. Click **Log In**.
4. Upgrade WordPress to v6.0.2.
On the left sidebar, click **Dashboard** > **Updates** to update WordPress to v6.0.2.





### Creating a COS bucket

1. Create a **Public Read/Private Write** bucket as instructed in [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309), preferably in the same region as the CVM instance where WordPress is running.
2. Locate the bucket you created on the **Bucket List** page and click its name to enter the details page.
3. Click **Overview** on the left sidebar. Then, find and record the endpoint.


### Installing and configuring the plugin

You can install the plugin in the plugin library or via the source code.

#### Installation in the plugin library (recommended)

On the WordPress backend, click **Plugins**, directly search for the **tencentcloud-cos** plugin, and click **Install Now**.


#### Installation via the source code

Download the plugin source code, upload it to the WordPress plugin directory `wp-content/plugins`, and run it on the backend.

The following steps take Ubuntu as an example to describe how to install a plugin:

1. Go to the parent directory of `wp-content`: 
```
cd /var/www/html/ 
```
2. Add permissions: 
```
chmod -R 777 wp-content 
```
3. Create a plugin directory:
```
cd wp-content/plugins/
mkdir tencent-cloud-cos
cd tencent-cloud-cos
```
4. Download the plugin to the plugin directory:
```
wget https://cos5.cloud.tencent.com/cosbrowser/code/tencent-cloud-cos.zip
unzip tencent-cloud-cos.zip
rm tencent-cloud-cos.zip -f
```
5. Click **Plugins** on the left sidebar, and you can see the plugin. Click **Activate** to activate it.





#### **Configuring the plugin**

Configure the COS bucket information in the tencent-cloud-cos plugin:

1. Click **Settings** to configure the tencent-cloud-cos plugin.

2. Configure the COS information as follows:
<table>
<thead>
<tr>
<th align="left">Configuration Item</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">SecretId and SecretKey</td>
<td align="left">Enter the access key information, which can be created and obtained on the <a href="https://console.cloud.tencent.com/capi">Manage API Key</a> page.</td>
</tr>
<tr>
<td align="left">Region</td>
<td align="left">The region selected during bucket creation</tdz
</tr>
<tr>
<td align="left">Bucket Name</td>
<td align="left">The bucket name customized during bucket creation, such as `examplebucket-1250000000`</td>
</tr>
<tr>
<td align="left">Endpoint</td>
<td align="left">The COS bucket's default domain name, which is automatically generated when the bucket is created. Buckets residing in different regions have different default domain names. To view the default domain name, go to the <a href="https://console.cloud.tencent.com/cos5">COS console</a>, click the name of the target bucket, and view it in <strong>Overview > Domain Information</strong>.</td>
</tr>
<tr>
<td align="left">Auto-Rename</td>
<td align="left">This option can automatically rename files uploaded to COS based on the specified format to avoid conflicts with existing files with the same name.</td>
</tr>
<tr>
<td align="left">Do Not Save Locally</td>
<td align="left">After this option is enabled, source files will not be retained locally.</td>
</tr>
<tr>
<td align="left">Retain Remote File</td>
<td align="left">After this option is enabled, if a file is deleted, only the local file copy will be deleted, and the file copy in the remote COS bucket will still be retained in case you want to recover it.</td>
</tr>
<tr>
<td align="left">Forbid Thumbnail</td>
<td align="left">After this option is enabled, thumbnail files will not be uploaded.</td>
</tr>
<tr>
<td align="left">Cloud Infinite</td>
<td align="left">After the CI service is enabled, you can perform various operations on images, such as editing, compression, format conversion, and watermarking. For more information, see <a href="https://cloud.tencent.com/product/ci">Cloud Infinite</a>.</td>
</tr>
<tr>
<td align="left">File Moderation</td>
<td align="left">After file moderation is enabled, it intelligently moderates the multimedia content of images, videos, audios, text, files, and webpages. It helps you effectively identify non-compliant content such as pornographic, vulgar, illegal, disgusting, and offensive information to avoid operational risks. For more information, see <a href="https://cloud.tencent.com/document/product/436/45435">Sensitive Content Moderation Overview</a>.</td>
</tr>
<tr>
<td align="left">File Preview</td>
<td align="left">After file preview is enabled, it converts files into images, PDF files, or HTML5 pages to display the file content on webpages. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/49159">File Preview Overview</a>.</td>
</tr>
<tr>
<td align="left">Debugging</td>
<td align="left">This feature logs errors, exceptions, and warnings.</td>
</tr>
</tbody></table>


2. After completing the configuration, click **Save**.



## **Verifying WordPress Attachment Storage to COS**

You can create a post with an image in WordPress and check whether the image is stored in COS.

1. On the WordPress dashboard, click **Posts** on the left sidebar to create a post with an image.

2. Edit the "Hello world!" post generated by WordPress by default.

3. Click **+** on the right.

4. Upload an image.

5. Then, check whether the URL of the uploaded image is a COS URL such as `https://wd-125000000.cos.ap-nanjing.myqcloud.com/2022/10/Start of Summer-1200x675.jpeg` in the format of `https://<BucketName-APPID>.cos.<Region>.myqcloud.com/<ObjectKey>`, and if so, the image has been uploaded to the COS bucket.

6. Log in to the COS console, and you can see the newly uploaded image in the bucket.

>? Once confirmed, sync your old WordPress resources to the COS bucket by using [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) or [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392). **This step must be performed; otherwise, you will not be able to view these resources in COS.** Then, you can optionally enable origin-pull as instructed below in [Setting origin-pull](#1).


## Others

1. Using CDN for access acceleration
To configure CDN acceleration for your bucket, see [Setting CDN Acceleration](https://intl.cloud.tencent.com/document/product/436/18670). You will then need to change the URL prefix to the default or custom CDN acceleration domain name in the WordPress plugin settings.
2. Replacing the resource URL in the WordPress database
Unless it’s a newly created WordPress site, you will need to use the plugin to replace the old resource URLs in your WordPress database with new ones (if it’s your first time, we recommend backing up your information before proceeding with this step).
 - Enter the old domain name for the resource, e.g. `https://example.com/`.
 - Enter the current domain name for the resource, e.g. `https://img.example.com/`.
3. Setting cross-origin access
When you reference a WordPress resource link in a document, you may receive the following prompt on the Tencent Cloud console: `No 'Access-Control-Allow-Origin' header is present on the requested resource`. This is most likely due to the fact that you haven’t configured the `HTTP Header` parameter in your CORS settings. You can configure this parameter in one of the following two ways:
 - Configuring on the COS console

>? For more information, please see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
>
 - Configuring on the CDN console
    - To allow all domain names, configure the following:
```plaintext
Access-Control-Allow-Origin: *
```
    - To allow access for only your own domain name, configure the following:
```plaintext
Access-Control-Allow-Origin: https://example.com
```
<span id=1></span>
4. Setting origin-pull
If you do not upload resources to the WordPress media library through the COS console, we recommend using COS origin-pull. For detailed directions, see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).
Once origin-pull is enabled, when a client accesses a source object in COS for the first time, if COS cannot hit the object, it will return a 302 HTTP status code and automatically redirect the request to the origin-pull address. Then, the origin will provide the object for access. Meanwhile, COS will copy this object from the origin and store it in the corresponding COS directory so that COS will be able to directly return the object to the client in subsequent requests.




