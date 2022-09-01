## Overview

[WordPress](https://cn.wordpress.org/) is a blogging platform built with PHP. You can use it to build your own website on a server that supports PHP and MySQL databases, or simply as a content management system (CMS).

WordPress is a powerful, scalable, and easy-to-expand platform with a wide range of plugins. With third-party plugins, it offers everything that a website should have.

This document describes how to use a plugin to store remote attachments from the WordPress media library in [COS](https://www.tencentcloud.com/products/cos).

As COS is highly scalable, reliable, secure, and cost-effective, storing your media library attachments in COS offers the following benefits:

- Higher reliability for your attachments.
- No need to prepare additional storage capacity on your server for attachments.
- Faster access to image attachments through the COS server rather than taking up downstream bandwidth/increasing the traffic on your server.
- Accelerated user access to image attachments through [CDN](https://www.tencentcloud.com/products/cdn).

## Preparations

1. Create a blog website with WordPress.
 - You can download the latest version of WordPress and view installation instructions at [Get WordPress](https://wordpress.org/download/).

2. Create a **Public Read/Private Write** bucket as instructed in [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309), preferably in the same region as the CVM instance where WordPress is running.
3. Find the bucket you created on the **Bucket List** page and click its name to enter the details page.

4. Click the **Overview** tab on the left sidebar. Then, find and record the endpoint.


## Installing and Configuring Plugin

### Installing plugin

On the WordPress backend, click **Plugins** > **Add New**. You can install the plugin in one of the following two ways:

 - Search for **tencentcloud-cos** directly and install it (recommended).
 - Download the latest release of the source code from [GitHub](https://github.com/Tencent-Cloud-Plugins/tencentcloud-wordpress-plugin-cos), and then upload it on the WordPress backend. You can also upload it directly to the plugin directory `wp-content/plugins` and run it on the backend.

### Configuring plugin

1. Click **Tencent Cloud Settings** on the left sidebar of WordPress and configure relevant COS information as follows:
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
<td align="left">Space Name</td>
<td align="left">The bucket name customized during bucket creation, such as `examplebucket-1250000000`</td>
</tr>
<tr>
<td align="left">Access Domain Name</td>
<td align="left">The COS bucket's default domain name, which is automatically generated when the bucket is created. Buckets in different regions have different default domain names. To view the default domain name, go to the <a href="https://console.cloud.tencent.com/cos5">COS console</a>, click the name of the target bucket, click <strong>Overview</strong>, and find the <strong>Domain Information</strong> section.</td>
</tr>
<tr>
<td align="left">Auto-Rename</td>
<td align="left">This option can automatically rename files uploaded to COS based on the specified format to avoid conflicts with existing files with the same name.</td>
</tr>
<tr>
<td align="left">Do Not Save Locally</td>
<td align="left">After this option is enabled, source files will not be retained locally. We recommend you not enable it.</td>
</tr>
<tr>
<td align="left">Forbid Thumbnail</td>
<td align="left">After this option is enabled, corresponding thumbnail files will not be uploaded. We recommend you not enable it.</td>
</tr>
<tr>
<td align="left">CI</td>
<td align="left">After the CI service is enabled, you can perform various operations on images, such as editing, compression, format conversion, and watermarking. For more information, see <a href="https://www.tencentcloud.com/products/ci">Cloud Infinite</a>.</td>
</tr>
<tr>
<td align="left">Debugging</td>
<td align="left">This feature logs errors, exceptions, and warnings. You can enable it as needed.</td>
</tr>
</tbody></table>
2. After completing the configuration, click **Save Configuration**.
3. Upload a new test file and confirm that its URL points to COS.

>? Once confirmed, sync your old WordPress resources to the COS bucket by using [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) or [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392). **This step must be performed; otherwise, you will not be able to view these resources in COS.** Then, you can optionally enable origin-pull as instructed below in [Set origin-pull](#1).
>

## More Capabilities

1. Use CDN for access acceleration
To configure CDN acceleration for your bucket, see [Setting CDN Acceleration](https://intl.cloud.tencent.com/document/product/436/18670). You will need to change the URL prefix to the default or custom CDN acceleration domain name in the WordPress plugin settings.
2. Replace resource URLs in the database
Unless your website is newly created, you will need to use the plugin to replace the old resource URLs in the database with new ones. We recommend you back up your data before replacing for the first time.
 - Enter the old domain name for the resource, such as `https://example.com/`.
 - Enter the current domain name for the resource, such as `https://img.example.com/`.
3. Configure cross-origin access
When you reference a resource link in a document, you may receive the following prompt in the console: `No 'Access-Control-Allow-Origin' header is present on the requested resource`. This is most likely because you haven't configured the `HTTP Header` parameter in the CORS settings. You can configure this parameter in one of the following two ways:
 - Configure in the COS console

>? For more information, see [Setting CORS](https://intl.cloud.tencent.com/document/product/436/13318).
>
 - Configure in the CDN console
    - To allow all domain names, configure the following:
```plaintext
Access-Control-Allow-Origin: *
```
    - To allow access for only your own domain name, configure the following:
```plaintext
Access-Control-Allow-Origin: https://example.com
```
<span id=1></span>
4. Set origin-pull
If you don't upload resources to the WordPress media library through the COS console, we recommend you use COS origin-pull. For detailed directions, see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).
Once origin-pull is enabled, when a client accesses a source object in COS for the first time, if COS cannot hit the object, it will return a 302 HTTP status code and automatically redirect the request to the origin-pull address. Then, the origin will provide the object for access. Meanwhile, COS will copy this object from the origin and store it in the corresponding COS directory so that COS will be able to directly return the object to the client in subsequent requests.

