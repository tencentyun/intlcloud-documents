## Overview

[WordPress](https://cn.wordpress.org/) is a blogging platform built with PHP. You can use it to build your own website on a server that supports PHP and MySQL databases, or simply as a content management system (CMS).

WordPress is powerful and scalable thanks to its wide range of plugins easy to extend. Basically, it can have everything that a website should have through its third-party plug-ins.

This document will describe how to use a plugin to store remote attachments from WordPress media library into [Tencent Cloud COS](https://intl.cloud.tencent.com/product/cos).

Since Tencent Cloud COS is highly scalable, reliable, secure, and cost-effective, there will be benefits as follows if you store your media library attachments on it:

- Higher reliability for your attachments.
- No need to prepare additional storage capacity on your server for attachments.
- Faster access to image attachments through connection to COS server in place of downstream bandwidth/traffic of your own server.
- Further faster access to image attachments and your website by using Tencent Cloud [CDN](https://intl.cloud.tencent.com/product/cdn).

## Preparations

1. Build a blog using WordPress.
 - You can download the latest version of WordPress and view installation instructions on [WordPress.org](https://wordpress.org/download/).
 - You can alternatively select a CVM image with built-in WordPress from Tencent Cloud image market when you install a CVM instance.
2. Create a **Public Read/Private Write** bucket as instructed in [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309), preferably in the same region as the CVM instance where WordPress runs.
3. Locate the bucket you created from the **Bucket List**, and click its name to enter the details page.
![](https://main.qcloudimg.com/raw/13d88e1cf3ad72e6f198a328d21cef13.png)
4. Click **Basic Configuration** and copy the bucket endpoint.
![](https://main.qcloudimg.com/raw/a8eb4239f4ad0e0b24881e3d710318a3.png)

## Installing and Configuring the Plugin

### Installing the plugin

In your WordPress admin panel, click **Plugins** > **Add New**. To install the plugin, you can use one of the following two ways:

 - Search for and install **Sync QCloud COS** directly here (recommended).
 - Download the latest release of source code from [Github](https://github.com/sy-records/wordpress-qcloud-cos/releases/latest), and upload it using the admin panel, or upload it directly to the plugins directory `wp-content/plugins` and run it in the admin panel.

### Configuring the plugin

1. Click **Settings** in WordPress navigation pane, and configure COS information as follows:

| Configuration Item              | Description                                                       |
| :------------------ | :----------------------------------------------------------- |
| Bucket Name          | Name you specify when you create a bucket                                     |
| Bucket Region          | Region you choose when you create a bucket                                     |
| APPID               | A permanent unique application ID assigned to you after you signed up to Tencent Cloud. You can view it in [Account Information](https://console.cloud.tencent.com/developer). |
| SecretID, SecretKey | Your access key; obtained from [API Key Management](https://console.cloud.tencent.com/capi). |
| Upload no Thumbnails        | Select this option, and no thumbnails will be uploaded (not recommended).                   |
| No Local Backups    | Select this option, and no local source files will be retained (not recommended).                       |
| Local Folder          | A local path in which to save a file, such as `wp-content/uploads`.                       |
| URL Prefix            | Format: `<COS endpoint>/<local folder>`, e.g. `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/wp-content/uploads`. |

2. After completing the configuration, click **Save**.
3. Upload a new test file, and confirm that its URL as part of attachment details points to Tencent Cloud COS.

>Once confirmed, sync your old resources in WordPress to the COS bucket (using [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) or [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392)). **Otherwise, you are unable to view them in COS**. Then, you can optionally enable COS origin-pull as instructed below in [Setting Origin-Pull](#1).

## More Capabilities

1. Using CDN for access acceleration
To configure CDN acceleration for your bucket, see [Setting CDN Acceleration](https://intl.cloud.tencent.com/document/product/436/18670). You also need to change the URL prefix to the default or custom CDN acceleration domain name in WordPress plugin settings.
2. Replacing the resource URL in the WordPress database
Unless it’s a newly created WordPress site, you need to replace the old resource URLs (backups recommended for the first time) in your WordPress database with new ones using the plugin.
 - Enter the old domain name for the resource, e.g. `https://example.com/`.
 - Enter the current domain name for the resource, e.g. `https://img.example.com/`.
3. Setting cross-origin access
When you reference a WordPress resource link in a document, you may be prompted that `No 'Access-Control-Allow-Origin' header is present on the requested resource` in the Tencent Cloud console. It is probably because you haven’t configured `HTTP Header` in your CORS settings. To configure it, use one of the 2 following ways:
 - By COS console
![](https://main.qcloudimg.com/raw/71dcabb63c9d0d4120eb33bfd7df92f1.png)
>For more information, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
 - By CDN console
    - To allow all domains, configure the following:
```plaintext
Access-Control-Allow-Origin: *
```
    - To allow only your own domain, configure the following:
```plaintext
Access-Control-Allow-Origin: https://example.com
```

<span id=1>

4. Setting origin-pull
If you do not set the WordPress media library to COS and upload resources using the COS console, it’s recommended to use COS origin-pull. For detailed directions, see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).
Once you enable COS origin-pull, COS will return 302 HTTP status code to the client for an unsuccessful request for a COS source file, and jump to the file corresponding to the origin-pull address. Then, the origin server will provide the file for access. Meanwhile, COS will copy this file to a directory in the COS bucket. For subsequent requests, COS will directly return the COS file to the client.