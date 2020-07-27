## Overview

[WordPress](https://cn.wordpress.org/) is a blogging platform built with PHP. You can use it to build your own website on a server that supports PHP and MySQL databases, or simply as a content management system (CMS).

WordPress is powerful and scalable platform due to its wide range of plugins and the ease with which you can to expand its features. With a plethora of third-party plug-ins, it offers everything that a website should have.

This document will describe how to use a plugin to store remote attachments from the WordPress media library in [Tencent Cloud COS](https://intl.cloud.tencent.com/product/cos).

Since Tencent Cloud COS is highly scalable, reliable, secure, and cost-effective, storing your media library attachments in COS offers the following benefits:

- Higher reliability for your attachments.
- No need to prepare additional storage capacity on your server for attachments.
- Faster access to image attachments through the COS server rather than taking up downstream bandwidth/increasing the traffic on your own server.
- Overall faster access to image attachments and websites through Tencent Cloud [CDN](https://intl.cloud.tencent.com/product/cdn).

## Preparations

1. Create a blog using WordPress.
 - You can download the latest version of WordPress and view installation instructions on the [WordPress official website] (https://wordpress.org/download/).
 - You can alternatively select a CVM image with  WordPress already pre-installed from the Tencent Cloud image market when you install a CVM instance.
2. Create a **Public Read/Private Write** bucket as instructed in [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309), preferably in the same region as the CVM instance where WordPress is running.
3. Locate the bucket you created on the **Bucket List** page, and click its name to enter the details page.
![](https://main.qcloudimg.com/raw/13d88e1cf3ad72e6f198a328d21cef13.png)
4. Click **Basic Configuration** and copy the bucket endpoint.
![](https://main.qcloudimg.com/raw/a8eb4239f4ad0e0b24881e3d710318a3.png)

## Installing and Configuring the Plugin

### Installing the plugin

In your WordPress admin panel, click **Plugins** > **Add New**. You can install the plugin in one of the following two ways:

 - Directly search for and install **Sync QCloud COS** (recommended).
 - Download the latest release of the source code from [Github](https://github.com/sy-records/wordpress-qcloud-cos/releases/latest), and upload it using the admin panel. Alternatively, you can upload it directly to the plugins directory `wp-content/plugins` and run it on the admin panel.

### Configuring the plugin

1. Click **Settings** in the left sidebar of WordPress and configure the relevant COS information as follows:

| Configuration Item              | Description                                                       |
| :------------------ | :----------------------------------------------------------- |
| Bucket Name          | The name you specified when you created the bucket |
| Bucket Region          | The region you chose when you created the bucket |
| APPID               | A permanent unique application ID assigned to you after you sign up for a Tencent Cloud account. You can view your APPID on your [Account Information](https://console.cloud.tencent.com/developer) page. |
| SecretID, SecretKey | Your access key; This value can be obtained from the [API Key Management](https://console.cloud.tencent.com/capi) page on the console. |
| Upload no Thumbnails        | Select this option, and no thumbnails will be uploaded (not recommended).                   |
| No Local Backups    | Select this option, and no local source files will be backed-up (not recommended). |
| Local Folder          | A local path in which you can save files, such as `wp-content/uploads`.                       |
| URL Prefix            | Format: `<COS endpoint>/<local folder>`, e.g. `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/wp-content/uploads`. |

2. After completing the configuration, click **Save**.
3. Upload a new test file and confirm that its URL points to Tencent Cloud COS.

>Once confirmed, sync your old WordPress resources to the COS bucket using [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) or [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392). **This step must be performed or you will be unable to view these resources in COS**. Then, you can optionally enable COS origin-pull as instructed below in [Setting Origin-Pull](#1).

## More Capabilities

1. Using CDN for access acceleration
To configure CDN acceleration for your bucket, see [Setting CDN Acceleration](https://intl.cloud.tencent.com/document/product/436/18670). You will then need to change the URL prefix to the default or custom CDN acceleration domain name in the WordPress plugin settings.
2. Replacing the resource URL in the WordPress database
Unless it’s a newly created WordPress site, you will need to use the plugin to replace the old resource URLs in your WordPress database with new ones (if it’s your first time, we recommend backing up your information before proceeding with this step).
 - Enter the old domain name for the resource, e.g. `https://example.com/`.
 - Enter the current domain name for the resource, e.g. `https://img.example.com/`.
3. Setting cross-origin access
When you reference a WordPress resource link in a document, you may receive the following prompt on the Tencent Cloud console: `No 'Access-Control-Allow-Origin' header is present on the requested resource`. This is most likely due to the fact that you haven’t configured the `HTTP Header` parameter in your CORS settings. You can configure this parameter in one of the following two ways:
 - Configuring on the COS console
![](https://main.qcloudimg.com/raw/ec11051c0737ca9b66710d368106cbd6.png)
>For more information, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
 - Configuring on the CDN console
    - To allow all domain names, configure the following:
```plaintext
Access-Control-Allow-Origin: *
```
    - To allow access for only your own domain name, configure the following:
```plaintext
Access-Control-Allow-Origin: https://example.com
```

<span id=1>

4. Setting origin-pull
If you do not upload resources to the WordPress media library through the COS console, we recommend using COS origin-pull. For detailed directions, see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).
Once you enable COS origin-pull, COS will return a 302 HTTP status code upon an unsuccessful request for a COS source file, and the request will be automatically redirected to the file corresponding to the origin-pull address. Then, the origin server will provide the file for access. Meanwhile, COS will copy this file from the origin server and store it in the corresponding COS directory and bucket so that, for subsequent requests, COS will be able to directly return the file to the client.