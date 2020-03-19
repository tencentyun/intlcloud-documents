## Introduction

This document describes how to host an existing or new static website on COS and make it accessible to visitors through a custom domain name such as `www.example.com`. The specific steps are as follows:
![](https://main.qcloudimg.com/raw/91c2a01b31b1ee7998bad883d8eaea04.png)

## Preparations

The following services will be used in this practice:

- [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloudProductDns): Before hosting a static website, you need to register a domain name such as `www.example.com`. You can do so via [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloud).
- [COS](https://intl.cloud.tencent.com/product/cos): You need to create a bucket in COS for storing the uploaded webpage contents.
- [CDN](https://intl.cloud.tencent.com/product/cdn): Together with Tencent Cloud DNS, CDN can accelerate the delivery of static website contents, reduce access delay, and improve availability while binding the domain name to the contents.
- Tencent Cloud DNS: It enables access to the static website through a custom domain name.

> The sample domain name `www.example.com` is used in all steps in this document. In practice, replace it with your own domain name.

## Directions

### 1. Register a domain name and apply for ICP filing for it

Domain name registration is a prerequisite for any service built on the internet. After you register a domain name, you need to apply for ICP filing for it before your website can be accessed. Please proceed according to your actual situation:

- If you have already registered a domain name and obtained ICP filing for it, skip this step and proceed to [step 2](#Create a bucket).
- If you have already registered a domain name but have not obtained ICP filing for it, please [apply for ICP filing](https://intl.cloud.tencent.com/product/icp).
- If you have not registered a domain name, please [register one](https://dnspod.cloud.tencent.com/?from=qcloud) first and then [apply for ICP filing for it ](https://intl.cloud.tencent.com/product/icp).

<span id="Create a bucket"></span>

### 2. Create a bucket and upload contents

After completing the domain name registration and ICP filing application, you need to perform the following tasks in the COS Console to create and configure the website contents:

- [Create a bucket](#create)
- [Configure the bucket and upload contents](#upload)

<span id="create"></span>

#### 2.1. Create a bucket

Please log in to the [COS Console](https://console.cloud.tencent.com/cos5) with your Tencent Cloud account and create a bucket for your website. The bucket is used to store data, so you can store your website contents in it.

If you are using COS for the first time, you can directly create a bucket by clicking **Create Bucket** on the overview page or using the **Bucket List** on the left sidebar in the console. For detailed directions, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

<span id="upload"></span>

<spsn id="step2.2"></span>
#### 2.2. Configure the bucket and upload contents

1). Enable the **Static Website** setting of the bucket in the following way:
a. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, locate the created bucket, and click **Configuration Management** on its right.
b. Find the **Static Website** configuration item, click **Edit**, set the current status to "on", leave other settings as default for now, and click **Save**.
2). Upload your website contents to the created bucket. For detailed directions, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).

You can store in the bucket any contents you want to host, such as text files, photos, and videos. If you haven't built a website yet, just create a file as described in this document.

For example, you can create a file with the following HTML code and upload it to the bucket. The filename of the website homepage is usually index.html. In subsequent steps, you will need to provide this file as an index file for your website.

```shell
<!DOCTYPE html>
<html>
    <head>
        <title>Hello COS!</title>
        <meta charset="utf-8">
    </head>
    <body>
        <p>Thank you for using the static website feature of COS.</p>
        <p>This is the homepage!</p>
    </body>
</html>
```

> After the static website feature is enabled, if a user accesses the first-level directory without path to any file, COS will first match index.html in the bucket directory and then index.htm by default. If this file does not exist, a 404 error will be returned.

<span id="Step 3"></span>

### 3. Bind a custom domain name

In order to speed up access, you are recommended to set the domain name as a custom accelerated domain name, so that you can use Tencent Cloud CDN to accelerate your static website for a better user experience.

#### 3.1. Add a domain name

1). Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left sidebar, and click the bucket storing the website contents.
2). In the second-level menu bar on the left, click **Domain Name Management** to enter the domain name management page. Click **Add Domain Name** in the **Custom Domain Name** section to enter the configurable page. Configure the following items and click **Save**.
- **Domain Name**: Enter the custom domain name you have purchased (e.g. `www.example.com`).
- **Origin Server Type**: Select **Static Website**.
- **Origin-pull Authentication**: Check it.
  3). After clicking **Save**, follow the on-screen prompts to add **CDN service authorization**. In the pop-up window, click **OK**.

4). Wait a few minutes until the domain name deployment is completed. Then, copy the corresponding CNAME record and proceed to [step 3.2](#Step 3.2).

<span id="Step 3.2"></span>

### 3.2. Add domain name resolution

If you registered your custom domain name through a third-party service provider, add a CNAME record for your domain name at the service provider and point it to the CNAME record in step 3.1.

### 4. Verify the result

After completing the above steps, verify the result by entering the domain name (`www.example.com`) in a browser:

- `http://www.example.com`: The index page (index.html) in the bucket named "example" will be returned.
- `http://www.example.com/test.html` (a non-existing file): A 404 error will be returned. If you want to customize the **error document**, you can add it in [step 2.2](#step2.2) when configuring the static website, so that when an access attempt is made to a non-existing file, this error document will be displayed.

> In some cases, you may have to clear your browser's cache to see the expected result.
