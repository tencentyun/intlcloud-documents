## Overview
You can configure a bucket to host a static website in the COS Console and access the static website at the bucket's access domain name. For more information on static websites, see [Static Website Hosting](https://intl.cloud.tencent.com/document/product/436/30958).

> To use buckets to host static websites, you first need to set the access permission to the buckets to **Public Read/Private Write**.

## Prerequisites
A bucket has been created. For more information, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), select **Bucket List** on the left sidebar, and click the bucket to host a static website to enter the bucket details page.
![](https://main.qcloudimg.com/raw/f9c20d98125c2041bd52c78bdacbad1b.png)
2. Click **Permission Management** on the left and find **Bucket ACL**. Select **Public Read & Private Write** in the Public Permissions configuration item.
![](https://main.qcloudimg.com/raw/460f2cdd71d3a21a74911a52218e7670.png)
3. Click **Basic Configuration** on the left and find the **Static Website** configuration item. Click **Edit**, toggle on the **Status** switch, and set the static website configuration items, as shown below:
   **Force  HTTPS (optional)**: After Force HTTPS is enabled, when an end user accesses your static website, the access node of the static website will forcibly enable the HTTPS protocol.
    **Index Document (required)**: An index document (i.e., the homepage of the static website) is a page returned when the root directory or any subdirectory of a website is requested, which is usually named index.html.
 > If folders are created in the bucket, the index document needs to be added at each folder level.

  **Error Document (optional)**: An error document is a page returned after an error occurs in accessing a static website. This configuration item allows you to define an error document. When the static website cannot respond to end user requests, the specified custom error page will be returned. For example, when an HTTP error occurs in accessing, if an error document named error.html is configured, the error.html page will be returned for easy troubleshooting. However, if it is not configured, the default error message will be returned.
 > Only a file in the bucket root directory can be configured as an error document. A file that is recognizable by browsers should be used, such as an `.html` or `.htm` file. Most browsers will display "inaccessible" or "access request denied" if an unrecognizable file such as a `.zip` file is used.

 **Redirect Rules (optional)**: With redirection rules, you can redirect requests based on specific file paths, prefixes in requests, or response codes.
For example, if a file in a bucket is deleted or renamed, you can add a redirection rule to redirect requests to other files.

 - Error codes: The redirection rules only support redirection configurations for `4xx` error codes (e.g., 404). You can customize the error page and add troubleshooting guidelines there, so that when a corresponding HTTP error is triggered, the end user can find more useful information.
 - Prefix matching: You can use a prefix matching rule to redirect requests to files or folders in the bucket. For more information, see [Redirection Rule Example](https://intl.cloud.tencent.com/document/product/436/30958#.E9.87.8D.E5.AE.9A.E5.90.91.E8.A7.84.E5.88.99).

 ![](https://main.qcloudimg.com/raw/55ffdab17e3e7781e9d580dafc4c9969.png)

4. After completing the configuration, click **Save**.
![](https://main.qcloudimg.com/raw/4fbd19fa75087bf5201dac3d8517ed3d.png)



