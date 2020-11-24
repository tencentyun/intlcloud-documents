## Overview
You can configure a bucket to host a static website in the COS Console and access the static website at the bucket's access domain name. For more information on static websites, see [Static Website Hosting](https://intl.cloud.tencent.com/document/product/436/30958).

>
>- To use buckets to host static websites, you first need to set the access permission of buckets to **Public Read/Private Write**.
>- For the static website configuration to take effect, you should use a static website domain name instead of a COS default domain name to access the COS origin server.

## Prerequisites
You have created a bucket. For more information, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and then select the **Bucket List** in the left pane. Click the bucket to host static websites to enter the bucket details page.

2. Click **Permission Management** > **Bucket ACL(Access Control List)** on the left sidebar, select **Public Read/Private Write** for Public Permissions, and save.
![](https://main.qcloudimg.com/raw/460f2cdd71d3a21a74911a52218e7670.png)
3. Click **Basic Configuration** on the left, and find the **Static Website** configuration item. Click **Edit**, toggle on the **Status** switch, and set the static website configuration items as shown below:
   **Mandatory HTTPS (Optional)**: After mandatory HTTPS is enabled, when a user accesses your static website, the access node of the static website will be forced enabled by using HTTPS protocol.
   **Ignore html extension**: this field is optional. If you access the path "index", the object `index.html` will be automatically matched and returned.
   **Index Document (required)**: An index document (i.e., the homepage of the static website) is a page returned when the root directory or any subdirectory of a website is requested, which is usually named index.html.
 >! If folders are created in the bucket, the index document needs to be added at each folder level.

  **Error Document (optional)**: An error document is a page returned after an error occurs in accessing a static website. This configuration item allows you to define an error document. When the static website cannot respond to end user requests, the specified custom error page will be returned. For example, when an HTTP error occurs in accessing, if an error document named error.html is configured, the error.html page will be returned for easy troubleshooting. However, if it is not configured, the default error message will be returned.
  
>! You can specify the error document as a file in the root directory or a subdirectory of your bucket. Please use a file in `.html` or `.htm` format that the browser can recognize. If a file that is not recognized by the browser, such as a `.zip` file, is used, most browsers will display an error Cannot access or deny the access request.

 **Error document response code**: displayed only if you specify **Error document**, and used to configure an HTTP response code returned with the error document. You can set it to **Original error code** or **200**.
 **Redirection Rules (Optional)**: With redirection rules, you can redirect requests based on specific file paths, prefixes in requests, or response codes.
For example, if a file in a bucket is deleted or renamed, you can add a redirection rule to redirect requests to other files.
 - Error codes: The redirection rules only support redirection configurations for `4xx` error codes (such as 404). You can customize the error page. If a corresponding HTTP error is triggered, you can provide guidelines for your users in the error page.
 - Prefix matching: You can use a prefix matching rule to redirect requests to files or folders in the bucket. For more information, see [Redirection Rule Example](https://intl.cloud.tencent.com/document/product/436/30958#.E9.87.8D.E5.AE.9A.E5.90.91.E8.A7.84.E5.88.99).
	![](https://main.qcloudimg.com/raw/55ffdab17e3e7781e9d580dafc4c9969.png)
4. After configuration, click **Save**.
