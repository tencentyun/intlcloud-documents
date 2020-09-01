## Overview

This document describes how to host an existing or new static website on COS and make it accessible to visitors through a custom domain name such as `www.example.com`. The specific steps are outlined below:
![](https://main.qcloudimg.com/raw/2f3fbbcc08b15f6037efc40e625037a3.png)

>- For the static website configuration to take effect, you need to use the domain name of the static website instead of the COS default domain name to access the COS origin server.
>- This practice only applies to scenarios where you need a domain name in Mainland China for your business.

## Preparations

The following services will be used in the steps outlined below:

- [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloudProductDns): Before hosting a static website, you need to register a domain name such as `www.example.com`. You can do so via the [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloud).
- [COS](https://intl.cloud.tencent.com/product/cos): You need to create a bucket in COS for storing the uploaded webpage contents.
- [CDN](https://intl.cloud.tencent.com/product/cdn): Together with Tencent Cloud DNS, CDN can accelerate the delivery of static website contents, reduce access delay, and improve availability, in addition to binding the domain name to the website content.
- Tencent Cloud DNS: Allows you to access the static website through a custom domain name.

>The sample domain name `www.example.com` is used in the steps outlined in this document. For your purposes, replace it with your own domain name.


## Step 1. Register the domain name and obtain ICP filing for service in China

Domain registration is a prerequisite for any service built on the Internet. After the domain name is registered, it needs to go through the MIIT filing procedure before your website can be accessed.

- If you have already registered a domain name and obtained ICP filing for service in China for it, skip this step and proceed to [step 2](#Create a bucket).
- Obtain ICP filing for the registered domain name.
- Register a domain name and obtain ICP filing for it.

<span id="Create a bucket"></span>

## Step 2. Create a bucket and upload content

After having registered the domain name and obtained ICP filing, you need to perform the following steps on the COS console:

- [Create a bucket](#create)
- [Configure the bucket and upload content](#upload)

<span id="create"></span>

#### 1. Create a bucket

Please log in to the [COS Console](https://console.cloud.tencent.com/cos) with your Tencent Cloud account and create a bucket for your website. This bucket can be used to store website content and data.

If you are using COS for the first time, you can create a bucket by accessing the **Bucket List** page on the left sidebar of the console and then clicking **Create Bucket** in the upper left-hand corner. For detailed directions, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

<span id="upload"></span>

<spsn id="step2.2"></span>
#### 2. Configure the bucket and upload content

(1) Enable a **Static Website** for the bucket in the following way:
a. Log in to the [COS Console](https://console.cloud.tencent.com/cos), and click **Bucket List** on the left sidebar. Locate the bucket, and click **Configuration Management** under the **Actions** column.
![](https://main.qcloudimg.com/raw/0fc6b8f1001f38059fcdd3de7a7292a3.png)
b. Scroll down to the **Static Website** section under **Basic Configuration**, click **Edit**, and switch the **Status** to on. Configure the **Index document** field to `index.html`, leaving the other fields blank for now, and then click **Save**.
![](https://main.qcloudimg.com/raw/f17aa7d97f2fe37e6be7c59fbffb9741.png)

(2) Upload your website contents to the bucket. For detailed directions, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).

You can use the bucket to store any content you want to host, including text files, photos, and videos. If you haven't built your website yet, just create a file as described in this document.

For example, you can create a file with the following HTML code and upload it to the bucket. The filename of the website homepage is usually index.html. In subsequent steps, you will need to provide this file as an index document for your website.

```shell
<!DOCTYPE html>
<html>
    <head>
        <title>Hello COS!</title>
        <meta charset="utf-8">
    </head>
    <body>
        <p>Thank you for using the static website feature of &nbspCOS&.</p>
        <p>This is the homepage!</p>
    </body>
</html>
```

>After the COS static website feature is enabled, if a user accesses any first-level directory that does not point to any files, COS will first match `index.html` in the bucket directory and then `index.htm` by default. If this file does not exist, a 404 error will be returned.

<span id="Step 3"></span>

## Step 3. Bind a custom domain name

We recommend that you use a custom CDN domain name so that Tencent Cloud CDN can accelerate the delivery of your static website contents for a better user experience.

#### 1. Add a domain name

(1) Log in to the [COS Console](https://console.cloud.tencent.com/cos), go to the **Bucket List** page on the left sidebar, and click the bucket that hosts your website.
(2) Click **Domain Management** to open the details page and then click **Add Domain** in the **Custom CDN Acceleration Domain** section to add a domain. Configure the domain as follows and then click **Save**.
- **Domain**: Enter the custom domain name you have purchased (e.g. `www.example.com`).
- **Origin Server Type**: Select **Static website origin server**.
- **Origin-pull Authentication**: Turn it on.
	

![](https://main.qcloudimg.com/raw/419c8e900a0c3ead5f01a4240129dfc3.png)
(3) Follow the prompt above the domain list to add **CDN Service Authorization**.
Click **OK** in the pop-up window.
![](https://main.qcloudimg.com/raw/0a24c915f0e1f580faa4edc1d06a97ef.png)
(4) Wait a few minutes until the domain name’s status is displayed as **Online**. Then, copy the CNAME and proceed to [Step 3.2](#Step 3.2).
 ![](https://main.qcloudimg.com/raw/a86989a753ce5f807931c50a5800d559.png)

<span id="Step 3.2"></span>

#### 2. DNS

If you registered your domain name through a third-party ISP, go to your ISP, add a CNAME record for your custom CDN domain name, and point it to the CNAME record configured above. To use Tencent Cloud DNS, follow these steps:

(1) Log in to the [DNS Console](https://console.cloud.tencent.com/cns), locate your domain name, and click **DNS**.

(2) Click **Add Record**.

- **Host record**: www
- **Type**: CNAME
- **Value**: the CNAME from the preceding step

(3) Click **Save**.

## Step 4. Verify the result

After completing the above steps, verify the result by entering the domain name, e.g. `www.example.com`, in your browser:

- `http://www.example.com`: Returns the index page (index.html) in the bucket named `example`.
- `http://www.example.com/folder/`: Returns the index page (folder/index.html) under the `folder` directory in the bucket named `example`.
- `http://www.example.com/test.html` (a non-existing file): returns 404 error. If you want to customize the error document, you can do so in [step 2](#step2.2) when configuring the static website, so that when an access attempt is made to a non-existing file, this error document will be displayed.

>
> - In some cases, you may have to clear your browser's cache to see the expected result.
> - For each bucket, you can configure only one error document, which can be placed in a sub-directory, such as pages/404.html.
