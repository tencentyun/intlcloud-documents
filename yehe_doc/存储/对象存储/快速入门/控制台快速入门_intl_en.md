

## Feature Overview


The Cloud Object Storage (COS) console is the easiest way to work with COS without writing code or programs. You can use COS services with the COS console directly.

## Limits

If this is your first time using COS, you are advised to learn the following concepts first.

- [Bucket](https://intl.cloud.tencent.com/document/product/436/13312): a carrier of objects, which can be considered as a "container" for storing objects. Each bucket can store an unlimited number of objects.
- [Object](https://intl.cloud.tencent.com/document/product/436/13324): the basic unit of COS storage. It can be data in any format, such as images, documents, audio and video, and others.
- [Region](https://intl.cloud.tencent.com/document/product/436/6224): a physical location where data centers are hosted on Tencent Cloud. COS data is stored in the buckets in these regions.

This document describes how to get started and store your data in the cloud using the COS console.

## Step 1. Sign up for a Tencent Cloud account
You must register a Tencent Cloud account before using the COS service. To do so, click the button below. Skip this step if you already have an account.

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://www.tencentcloud.com/en/account/register" target="_blank"  style="color: white; font-size:13px;">Account Sign Up</a></div>

## Step 2. Verify your identity
Once registered, use your registered account to log in to [Tencent Cloud console](https://console.cloud.tencent.com/) and verify your identity. For detailed directions, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629). If you have already done so, skip this step.

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:13px;"  hotrep="document.guide.3128.btn2">Identity Verification</a></div>


## Step 3. Activate COS service
Open the [Tencent Cloud console](https://console.cloud.tencent.com/), and select **Products** > **Cloud Object Storage** and enter the COS console. Then, follow the instructions to activate COS. If you have already done so, please skip this step.

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:13px;">Activate COS</a></div>


## Step 4. Create a bucket
You need to create a bucket to store your objects.

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket management page.
2. Click **Create Bucket** and configure the following items. Remaining items can be kept as default.
 - Name: enter the bucket name, which cannot be modified once set, such as examplebucket.
 - Region: select a region nearest to your business, such as Guangzhou.
 - Access permissions: access permission for the bucket. You can retain the default option **Private Read/Write**.
3. Click **OK**.


## Step 5. Upload an object
To upload a local file to your bucket, perform the following.

1. Click the bucket name to enter the object list page.
2. Select **Upload Files** > **Select Files** and choose a file to upload, such as `exampleobjext.zip`.
3. Click **Upload**.


## Step 6. Download an object
To download COS data, perform the following.
1. Click **Details** under **Operation** for the object `exampleobjext.zip` and enter the object attribute page.
2. To download the object, click **Download Objects** under **Basic Information**, or click **Copy Temporary Link**, paste the link into a browser, and press Enter.
>?If the object to download can be opened directly using a browser, you will directly preview the object instead of downloading the object after you access the temporary link.

## More
To learn more about what the COS console can offer, such as setting object access permissions, hotlink protection, and static websites, please see [Console Overview](https://intl.cloud.tencent.com/document/product/436/11365).


## Other methods
In addition to the console, the following methods are also provided for you to get started with.

<table>
<thead>
<tr>
<th align="left" width="30%">Method</th>
<th align="left" width="70%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser</a></td>
<td align="left" width="70%">Provides a user-friendly interface to easily upload and download objects and generate access URLs</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://cloud.tencent.com/doc/product/436/10976">COSCMD</a></td>
<td align="left" width="70%">Enables you to use simple commands to upload, download, and delete objects in batches</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">APIs</a></td>
<td align="left" width="70%">COS uses XML APIs, which are lightweight, connectionless, and stateless. By calling XML APIs, you can send requests to and accept responses from COS directly over HTTP/HTTPS
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDKs</a></td>
<td align="left" width="70%">Supports multiple mainstream programming languages including Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and WeChat Mini Program</td>
</tr>
</tbody></table>



## Troubleshooting

If you have any questions, [contact us](https://intl.cloud.tencent.com/contact-sales).



