
## Overview

The COS console is the easiest way to work with COS without even considering using code or programs.

## Preparations

If you are a first-time COS user, we recommend that you first learn about the following concepts:

- [Bucket](https://intl.cloud.tencent.com/document/product/436/13312): a container for objects stored in COS.
- [Object](https://intl.cloud.tencent.com/document/product/436/13324): the basic unit of COS storage, which can be understood as data in any format, such as images, documents, audio and video, etc.
- [Region](https://intl.cloud.tencent.com/document/product/436/6224): a physical location where data centers are hosted on Tencent Cloud. Buckets that store COS data reside in regions.

The following will describe how to get started with COS and store your data in the cloud using the console.

## Step 1. Sign up for a Tencent Cloud Account
You must register a Tencent Cloud account before you can use the COS service. To do so, click the button below (Skip this step if you already have an account.)

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:13px;">Sign Up</a></div>

## Step 2. Verify your Identity
Once registered, use your registered account to log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and verify your identity. For detailed instructions, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629) (If you are already done so, please skip this step.)

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:13px;"  hotrep="document.guide.3128.btn2">Verify</a></div>



## Step 3. Activate COS Service
Open the [Tencent Cloud Console](https://console.cloud.tencent.com/), and select **Products** > **Cloud Object Storage** to enter the COS console. Then, follow the on-screen instructions to activate COS service (If you have already done so, please skip this step.)

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:13px;">Activate COS</a></div>


## Step 4. Create a Bucket
You need to create a bucket to store your objects.

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket management page.
2. Click **Create Bucket** and configure information as follows:
 - Name: enter the bucket name, which cannot be modified once set, e.g. examplebucket.
 - Region: select a region nearest to your business where the bucket resides, e.g. Guangzhou.
 - Access Permissions: access permission for the bucket. You can leave the default option **Private Read/Write**.
3. Click **OK**.


## Step 5. Upload an Object
To upload a local file to your bucket:

1. Click the bucket name to enter the object list page.
2. Select **Upload Files** > **Select Files** and choose a file to upload, such as `exampleobjext.txt`.
3. Click **Upload**.


## Step 6. Download an Object
To download COS data locally:
1. Click **Details** under **Operation** for the object `exampleobjext.txt` to enter the object attribute page.
2. To download the object, simply click **Download Objects** under **Basic Information**, or click **Copy Temporary Link**, paste the link into a browser, and press Enter.

## More Features
To learn more about what COS can offer, such as setting object access permissions, hotlink protection, and static websites, please see [Console Overview](https://intl.cloud.tencent.com/document/product/436/11365).


## Other Accesses
In addition to the console, COS also offers the following accesses for you to get started with.

<table>
<thead>
<tr>
<th align="left" width="30%">Access</th>
<th align="left" width="70%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser</a></td>
<td align="left" width="70%">Provides a user-friendly interface to easily upload and download objects, and generate access URLs.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/10976">COSCMD</a></td>
<td align="left" width="70%">Enables you to use simple command lines to upload, download, and delete objects in batches.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">APIs</a></td>
<td align="left" width="70%">COS uses XML APIs, which are lightweight, connectionless, and stateless. By calling XML APIs, you can send requests to and accept responses from COS directly over HTTP/HTTPS.
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDKs</a></td>
<td align="left" width="70%">Support many major programming languages including Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and Wechat Mini Program.</td>
</tr>
</tbody></table>



## Troubleshooting

We are deeply sorry for any inconvenience you may have encountered when using the console. If you need to reach out, please contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
