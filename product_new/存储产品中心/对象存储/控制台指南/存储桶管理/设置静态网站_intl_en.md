## Overview
You can configure a bucket to host a static website in the COS Console and access the static website at the bucket's access domain name. For more information on static websites, see [Static Website Hosting](https://intl.cloud.tencent.com/document/product/436/30958).

> To use buckets to host static websites, you first need to set the access permission to the buckets to **Public Read/Private Write**.

## Prerequisites
A bucket has been created. For more information, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), select **Bucket List** on the left sidebar, and click the bucket to host a static website to enter the bucket details page.
![](https://main.qcloudimg.com/raw/46f3f6bcf85a1ca8f16a2f47479d0ef8.jpg)
2. Click **Permission Management** on the top and find **Bucket ACL**. Select **Public Read & Private Write** in the Public Permissions configuration item.
![](https://main.qcloudimg.com/raw/a62ac13b34f19027074c13a6cb0b62d7.jpg)
3. Click **Basic Configuration** on the top and find the **Static Website** configuration item. Click **Edit**, toggle on the **Status** switch, and set the static website configuration items, as shown below:
   **Mandatory HTTPS (optional)**: After mandatory HTTPS is enabled, when an end user accesses your static website, the access node of the static website will forcibly enable the HTTPS protocol.
    **Index Document (required)**: An index document (i.e., the homepage of the static website) is a page returned when the root directory or any subdirectory of a website is requested, which is usually named index.html.
 > If folders are created in the bucket, the index document needs to be added at each folder level.

  **Error Document (optional)**: An error document is a page returned after an error occurs in accessing a static website. This configuration item allows you to define an error document. When the static website cannot respond to end user requests, the specified custom error page will be returned. For example, when an HTTP error occurs in accessing, if an error document named error.html is configured, the error.html page will be returned for easy troubleshooting. However, if it is not configured, the default error message will be returned.
 > Only a file in the bucket root directory can be configured as an error document. A file that is recognizable by browsers should be used, such as an `.html` or `.htm` file. Most browsers will display "inaccessible" or "access request denied" if an unrecognizable file such as a `.zip` file is used.

 **Redirection Rules (optional)**: With redirection rules, you can redirect requests based on specific file paths, prefixes in requests, or response codes.
For example, if a file in a bucket is deleted or renamed, you can add a redirection rule to redirect requests to other files.
 - Error codes: The redirection rules only support redirection configurations for `4xx` error codes (e.g., 404). You can customize the error page and add troubleshooting guidelines there, so that when a corresponding HTTP error is triggered, the end user can find more useful information.
 - Prefix matching: You can use a prefix matching rule to redirect requests to files or folders in the bucket. For more information, see [Redirection Rule Example](https://intl.cloud.tencent.com/document/product/436/30958#.E9.87.8D.E5.AE.9A.E5.90.91.E8.A7.84.E5.88.99).

 ![](https://main.qcloudimg.com/raw/3754f0b0d19a815fc58896012e28025b.png)

4. After completing the configuration, click **Save**.
![](https://main.qcloudimg.com/raw/9888185749b48840c4b38af7383aac77.png)

## New Console vs. Legacy Console
Currently, the new and legacy consoles have different bucket domain name formats. Taking the Guangzhou region as an example, the bucket region name is referred to as ap-guangzhou in the new console, but it is cosgz in the legacy console. For more information on domain names, see [Regions and Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

Due to the differences in bucket domain name formats, when you use the static website feature, the access nodes for legacy and new versions of static website are also different. Take a bucket in the Chengdu region as an example:
- If you are using the console v5, your static website access node is in the format of `https://<BucketName-APPID>.cos-website.ap-chengdu.myqcloud.com`
- If you are using the console v4, your static website access node is in the format of `https://<BucketName>.cos-website.coscd.myqcloud.com`

If you have configured the static website feature in the legacy console, after upgrading to the new console, you can view it there, as shown below. To do so, simply click **Click to Load** in the **Historical Versions of Static Website** section.
![](https://main.qcloudimg.com/raw/dd6065f9cf4e8ffb1a2aec3be512794b.png)
After clicking it, you can view the legacy static website configuration, as shown below:
![](https://main.qcloudimg.com/raw/397c78be413c534f2857fdb2764177aa.png)
It should be noted that the legacy static website configuration can only be viewed but not edited. To experience the richer and more stable features of the new console, it is **recommended** that you reconfigure your static website domain name in the new console. Before reconfiguring, you need to take into account the following:

1. Before modifying the legacy static website configuration, be sure to check whether you have businesses that rely on the legacy static website, and if so, you need to modify them first.
2. Switch the legacy static website configuration to the new configuration. You only need to record the legacy configuration information, delete the legacy configuration, and then create a new configuration with the recorded information.
3. If you have a business that relies on the legacy static website domain name, you need to change the legacy domain name used by your business to the new static website domain name after step 2 is done.

> In addition to the domain name differences, the APIs called by the new and legacy consoles are different too. It is recommended that you use the new version of console, APIs, tools, and SDKs for a richer experience and more stable features. The APIs of object or bucket operations called in the new COS Console are XML APIs, while those in the legacy console are JSON APIs. For more information on the API differences, see [API and SDK](https://intl.cloud.tencent.com/document/product/436/10687).

