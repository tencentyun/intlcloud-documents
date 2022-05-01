## Overview

You can configure a bucket to host a static website in the COS console and access the static website at the bucket's access endpoint. For more information about static websites, please see [Static Website Hosting](https://intl.cloud.tencent.com/document/product/436/30958).

>!
>- To use buckets to host static websites, you first need to set the access permission of buckets to **Public Read/Private Write**.
>- For the static website configuration to take effect, you should use a static website endpoint instead of a COS default endpoint to access the COS origin server.
>

## Prerequisites

You have created a bucket. For more information, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and then click **Bucket List** in the left sidebar. Then, click the bucket to host static websites to enter the bucket detail page.
2. Click **Permission Management** > **Bucket ACL (Access Control List)** on the left. Then, select **Public Read/Private Write** for **Public Permissions** and click **Save**.
![](https://main.qcloudimg.com/raw/460f2cdd71d3a21a74911a52218e7670.png)
3. Click **Basic Configurations** > **Static Website** on the left. Then, click **Edit**, toggle on the **Status** switch, and set the configuration items.
![](https://main.qcloudimg.com/raw/e7365ffd7beca545f275ec36cdaa8cce.png)
Notes:
 - **Force HTTPS (optional)**: After force HTTPS is enabled, when a user accesses your static website, the access node of the static website will be forced to use the HTTPS protocol.
 >! If you access the static website using a custom endpoint with force HTTPS enabled, ensure that you have correctly configured a certificate for the custom endpoint. Otherwise, the website will be redirected to the default endpoint for access.
 >
 - **Ignore .html Extension (optional)**: If the access path is "index", the "index.html" object is automatically matched and returned.
 - **Index Document (required)**: homepage of the static website. It is a page returned when the root directory or any subdirectory of a website is requested, which is usually named "index.html".
 >! If folders are created in the bucket, the index document needs to be added at each folder level.
 >
 - **Error Document (optional)**: a page returned when an access error occurs. This configuration item allows you to define an error document. When the static website failed to respond to the user’s requests, the specified custom error page will be returned. For example, if you have configured an error document named "error.html", the "error.html" page will be returned when an HTTP error occurs to guide the user. If no error document is configured, the default error message will be returned.
 >! Only files in the bucket’s root directory or subdirectories can be configured as error documents. Please use browser-supported formats such as `.html` or `.htm`. If the file format (for example, `.zip`) is not supported, most browsers will display "inaccessible" or "access request denied".
 >
 - **Error Document Response Code** (valid only when **Error Document** is set): It can be set to **Original error code** or **200** as the HTTP response code for the returned error document.
 - **Redirect Rules (optional)**: With redirection rules, you can redirect requests based on specific file paths, prefixes in requests, or response codes.
For example, if a file in a bucket is deleted or renamed, you can add a redirection rule to redirect requests to other files.
    - Error codes: The redirection rules only support redirection configurations for 4xx error codes (such as 404). You can customize the error page. If a corresponding HTTP error is triggered, you can provide guidelines for your users on the error page.
    - Prefix matching: You can use a prefix matching rule to redirect requests to files or folders in the bucket. For more information, see [Redirection Rule Example](https://intl.cloud.tencent.com/document/product/436/30958#.E9.87.8D.E5.AE.9A.E5.90.91.E8.A7.84.E5.88.99).
4. After the configuration, click **Save**.
