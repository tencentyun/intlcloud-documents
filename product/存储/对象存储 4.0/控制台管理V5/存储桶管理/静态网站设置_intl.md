## Overview
You can set a bucket to host a static website through the COS Console and access the static website by accessing the domain name of the bucket.

>! To use buckets to host static websites, you first need to set the access permission of buckets to **Public Read/Private Write**.

## Procedure
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and then select the **Bucket List** in the left pane. Click the bucket to host static websites to enter the bucket details page.
![](https://main.qcloudimg.com/raw/b90ad17947a0ec530db87210f4b9027d.png)

2. Click **Permission Management** on the top and find **Bucket Access Permission**. Select **Public Read/Private Write** for public permissions.
![](https://main.qcloudimg.com/raw/db25a763ebb71786309a9a09efefa5fa.png)

3. Click the **Basic Configuration** on the top and find the **Static Website** configuration item. Click **Edit** and turn on the **Current Status** switch, and enter the content of static website configuration items. Configuration items are as follows:

 **Mandatory HTTPS (Optional)**: After mandatory HTTPS is enabled, when a user accesses your static website, the access node of the static website will be forced enabled by using HTTPS protocol.
**Index File (Required)**: An index file, the homepage of the static website, is a page returned when the root directory or any subdirectory of a website is requested, and is usually named index.html.

 >! If a folder is created in the bucket, the index file needs to be added at each level of the folder.

 **Error File (Optional)**: An error file is a page returned after an error occurs in accessing a static website. This configuration item allows you to define an error file. When a static website cannot respond to user requests, the specified custom error page is returned. For example, when an HTTP error occurs in accessing, if an error file named error.html is configured, the error.html page is returned to provide users with guidelines. But if it is not configured, the default error information is returned.

 >! Only files in the bucket root directory can be configured as error files. Files that are recognizable by browsers should be used, such as `.html` or `.htm` files. Most browsers will display "inaccessible" or "access request denied" if files that cannot be recognized by browsers, such as `.zip` files, are used.

 **Redirection Rules (Optional)**: With redirection rules, you can redirect requests based on specific file paths, prefixes in requests, or response codes.
For example, if a file in a bucket is deleted or renamed, you can add a redirection rule to redirect requests to other files.
 - Error codes: The redirection rules only support redirection configurations for `4xx` error codes (such as 404). You can customize the error page. If a corresponding HTTP error is triggered, you can provide guidelines for your users in the error page.
 - Prefix Match: You can use the prefix match rules to redirect files or folders in the bucket.

 ![](https://main.qcloudimg.com/raw/3754f0b0d19a815fc58896012e28025b.png)

4. After configuration, click **Save**.
![](https://main.qcloudimg.com/raw/9888185749b48840c4b38af7383aac77.png)

