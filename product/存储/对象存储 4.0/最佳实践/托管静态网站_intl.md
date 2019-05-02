## Introduction

This document describes how to host a static website on Tencent Cloud's COS, whether you want to host an existing static website or set up a website from scratch. Visitors can access the hosted static website via the custom domain name (such as `www.example.com`).
![](https://main.qcloudimg.com/raw/d70261f2d960e9da84a08db561af9b30.png)

## Preparations

The following are the services that will be used:

-  [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloudProductDns): Before the static website hosting, you need to register a domain name, such as `www.example.com`. You can apply for the domain name via Tencent Cloud's [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloud).
- [COS](https://cloud.tencent.com/product/cos): Create a bucket using COS. The uploaded webpage content will be stored in the bucket. Set the access permission for the bucket to **Public Read/Private Write** to allow everyone to view the webpage content.
- [CDN](https://cloud.tencent.com/product/cdn-scd): By using CDN with Tencent Cloud DNS, you can bind the domain name to the website content while accelerating the delivery of static website content, reducing access delay and improving availability.
-  [Tencent Cloud DNS](https://cloud.tencent.com/product/cns?from=qcloudProductCns): With Tencent Cloud DNS, you can access the static website with the custom domain name.

> ?The sample domain name `www.example.com` is used in all steps in this document. In practice, replace it with your own domain name.

## Directions

### 1. Register a domain name and file it with MIIT

Domain registration is a prerequisite for any service built on the Internet. After the domain name is registered, it needs to go through the filing procedure with MIIT before your website can be accessed. 

- If you have completed domain name registration and filing, skip this step and proceed to [Step 2](#创建存储桶).
- If you have registered the domain name but have not filed it with MIIT, complete [domain name filing](https://cloud.tencent.com/product/ba).
- If you have not registered the domain name, [register the domain name](https://dnspod.cloud.tencent.com/?from=qcloud) and then complete [domain name filing](https://cloud.tencent.com/product/ba).

<span id="Create Bucket"></span>

### 2. Create a bucket and upload content

After completing the domain name registration and filing, you need to perform the following tasks in the COS Console to create and configure the website content:

- [Create a bucket](#create)
- [Configure the bucket and upload content](#upload)

<span id="create"></span>

#### 2.1 Create a bucket

Log in to the [COS Console](https://console.cloud.tencent.com/cos) with your Tencent Cloud account to create a bucket used to store your website content. When you use COS for the first time, create a bucket directly from the **Overview** interface in the console, or create it in the **Bucket List** navigation pane. For more information, see [Creating a Bucket](https://cloud.tencent.com/document/product/436/13309).

<span id="upload"></span>

#### 2.2. Configure the bucket and upload content

(1) Set the access permissions for the bucket to **Public Read/Private Write** to make the website content accessible to anyone. For more information, see [Set Access Permissions](https://cloud.tencent.com/document/product/436/13315).

(2) Upload your website content to the created bucket. For more information, see [Upload Objects](https://cloud.tencent.com/document/product/436/13321).

You can store in the bucket any content you want to host, including text files, photos, and videos. If you haven't built a website yet, just create a file as described in this document.

For example, you can create a file with the following HTML and upload it to the bucket. The file name of the website home page is usually index.html. In subsequent steps, you will provide this file as an index file for your website.

```shell
<!DOCTYPE html>
<html>
    <head>
        <title>Hello COS!</title>
        <meta charset="utf-8">
    </head>
    <body>
        <p>Thank you for using &nbspCOS's&nbsp static website feature.</p>
        <p>This is home page!</p>
    </body>
</html>
```

> !After the static website feature is enabled, if a user accesses the first-level directory without path to any file, the COS first matches index.html in the bucket directory and then index.htm by default. If index.htm does not exist, 404 is returned.

<span id="Step 3"></span>

### 3. Bind custom domain name

> !
> - You need to bind the custom domain name and enable the static website feature before you can preview the content directly in the browser. If you use the default domain name (including CDN accelerated domain name and COS default domain name), the download box always pops up when you access the resources.
> - COS does not support adding a custom domain name without CDN activated. To use a custom domain name, you need to activate CDN acceleration. When you activate CDN, you must select **Static Website Origin Server** as the origin server before you can display the page directly via the custom domain name.

You can configure the custom domain name to point to the bucket, and enable the static website feature to make it possible to directly access the website (content in the bucket) via the browser while reducing the website access delay and improving availability. In the practice described in this document, a custom domain name is bound and CDN acceleration is activated for the domain name to give website visitors a better browsing experience.

#### 3.1 Add a domain name

There are two ways of adding a custom domain name:

- [Add via CDN Console](#通过CDN控制台): If you want to add a custom domain name while performing CDN advanced management and configuration, you can choose to add the domain name in the CDN Console. For more information, see [CDN Configuration Management](https://cloud.tencent.com/document/product/228/6288).
- [Add via COS console](#通过COS控制台): If you only need to add a custom domain name without making other configurations, you can add the domain name quickly in the COS Console.

<span id="Via CDN Console"></span>

- **Add Via CDN Console** 
  (1) Log in to [CDN Console](https://console.cloud.tencent.com/cdn), click **Domain Name Management** in the left navigation pane, and then click **Add Domain Name** to go to the **Add Domain Name** interface.
  ![](https://main.qcloudimg.com/raw/d6b5ea180a5bfe57ff0d1acf5861206f.png)
  (2) Enter the domain name for which you want to accelerate access, select **Cloud Object Storage (COS)** for origin server type, select the bucket and its default domain name of the hosted website content in **Bucket Settings**, select **Static Acceleration** for **Service Type**, and keep default settings for other configuration items.
  ![](https://main.qcloudimg.com/raw/15d1d5ed26b84b2dab8046ee7977469f.png)
  (3) Click **Submit** to add the domain name.
  (a). Close the pop-up window and wait until the domain name configuration items are distributed to the nodes across the network (about 5-10 minutes).
  ![](https://main.qcloudimg.com/raw/e352f9626cd1314615f8c8dd55b70211.png)
  (b). After your domain name is bound to the CDN, the system automatically assigns you a CNAME domain name suffixed with `.cdn.dnsv1.com`. The CNAME domain name cannot be accessed directly. You need to complete the CNAME configuration at the domain name service provider. When the configuration takes effect, you can use the CDN acceleration service. The CNAME record can be found in [Domain Name Management](https://console.cloud.tencent.com/cdn/access) in the CDN Console. After obtaining the CNAME record, proceed to [Step 3.2](#步骤3.2).
  ![](http://mc.qcloudimg.com/static/img/3922bf529760e262316381936e40e26c/image.png)

<span id="Via COS Console"></span>

- **Add via COS Console**
  (1) Log in to [COS Console](https://console.cloud.tencent.com/cos5), go to **Bucket List** in the left navigation pane, click the bucket storing the website content to enter the bucket details page.
  ![](https://main.qcloudimg.com/raw/e3fbbecd2816bb893bfbd5e739868a20.png)
  (2) Click **Domain Name Management** to go to the domain name management page, and then click **Add Domain Name** under the custom domain name to enter the configurable status.
  **Domain Name**: Enter the custom domain name you have purchased (e.g. `www.example.com`).
  **Origin Server Type**: Select **Static Website Origin Server**.
  Click **Save** to add the domain name.
  ![](https://main.qcloudimg.com/raw/7e642e83065c98fe80636432107abc4c.png)
  (3) Wait a few minutes until the domain name deployment is completed. Then copy the CNAME record and proceed to [Step 3.2](#步骤3.2).
  ![](https://main.qcloudimg.com/raw/fbab10f4b29381a0c0af4838f9bfc3cf.png)

<span id="Step 3.2"></span>

### 3.2 Domain name resolution

(1) After adding a custom domain name, you need to perform domain name resolution. Log in to [Tencent Cloud DNS](https://console.cloud.tencent.com/cns) and click **Domain Name Resolution List** on the left navigation pane to enter the domain name resolution list. When you click **Add Resolution**, the **Add Domain Name** dialog box pops up.
   ![](https://main.qcloudimg.com/raw/f0603d93d1417277f79562aa98dbc0c4.png)
(2) Enter the custom domain name and click **OK** to save it.
   ![](https://main.qcloudimg.com/raw/878946d926cae79f7451afcbb129c1dd.png)
(3) After the domain name is added successfully, click the domain name to enter the resolution record management page. Click **Add Record** to go to the **Add Record** dialog box.
   ![](https://main.qcloudimg.com/raw/deaec39dc4903ca72475a14d7373e034.png)
(4) Select CNAME for **Record Type**, leave **Host Name** empty, select **Default** for **Line Type**, enter the CNAME record obtained in [Step 3](#步骤3), keep the default of **TTL**, and click **OK**. After the resolution is added, it takes about 15 minutes to take effect.
   ![](https://main.qcloudimg.com/raw/1fb0076d1cebb05c4f58c9b61dd05044.png)

### 4. Enable static website feature

After binding the website content to the custom domain name, you need to enable the static website feature of COS to directly access the website content using your browser. For more information, see [Setting Up a Static Website](https://cloud.tencent.com/document/product/436/14984).

### 5. Verify the result

After completing the above steps, verify the result by entering the website's domain name in the browser's address bar, for example, #www.example.com`:

- `http://www.example.com` -- The index page (index.html) in the bucket named "example" is returned.
- `http://www.example.com/test.html` (a non-existent file) - A 404 file (error.html) in the bucket named "example" is returned.

> ?In some cases, you may need to clear up your browser's cache to see the expected result.

