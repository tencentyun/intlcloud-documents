Amazon Simple Storage Service (S3) is one of the earliest cloud services launched by AWS. After many years of development, the S3 protocol has become a de facto standard in the object storage field. Tencent Cloud Object Storage (COS) provides an S3-compatible implementation scheme, so you can directly use the COS service in most S3-compatible applications. This document describes how to configure such applications to use COS.

## Prerequisites

### Checking whether the application can use COS

- An application with `S3 Compatible` in its description can use COS in most cases. If you find that some of its features cannot work properly, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance, and be sure to indicate that you followed the steps in this document and provide information such as the application name and screenshots.
- If your application description only states that `Amazon S3` is supported, it means that the application can use the S3 service, but whether it can use COS needs to be further evaluated in relevant configurations as detailed below.

### Preparing COS service

#### Step 1. Sign up for a Tencent Cloud account

(If you already have a Tencent Cloud account, skip this step.)

<div style="background-color:#00A4FF; width: 300px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/account/register" target="_blank"  style="color: white; font-size:16px;">Click here to sign up for a Tencent Cloud account</a></div>

#### Step 2. Verify your identity

(If you have already done so, skip this step.)

<div style="background-color:#00A4FF; width: 280px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

For more information on how to verify your identity, see <a href="https://intl.cloud.tencent.com/document/product/378/3629">Identity Verification Guide</a>.

#### Step 3. Activate the COS service

<div style="background-color:#00A4FF; width: 260px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:16px;">Click here to activate the COS service.</a></div>

<span id="step4"></span>
#### Step 4. Prepare the APPID and access key

Get and note down the **APPID**, **SecretId**, and **SecretKey** on the [API Key](https://console.cloud.tencent.com/cam/capi) page in the CAM console.

![](https://qcloudimg.tencent-cloud.cn/raw/82216475f85f3bb8c9662e35998cbbc3.png)

<span id="step5"></span>
#### Step 5. Create a bucket

Create a COS bucket as instructed in [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

Some applications have a built-in process for creating buckets. If you want such applications to create buckets, skip this step.


## Configuring COS Service in Application

### Basic configuration

Most applications have similar configuration items for using a storage service. The common names and descriptions of these configuration items are as listed below:

>? If you have any questions during the configuration, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance, and be sure to indicate that you followed the steps in this document and provide information such as the application name and screenshots.
>


<table>
<thead>
<tr>
<th>Common Configuration Item Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Provider, service provider, storage service provider, storage provider, etc.</td>
<td>Select which storage service the application should use. There may be the following cases: <br><li>If an option has text like S3 Compatible Storage/S3 Compatible, then it will be used first. <br></li><li>If an option only has text like Amazon Web Services/AWS/Amazon S3, then use it but pay attention to our further instructions during configuration.<br></li><li>If there is no similar option, but the application description mentions that the application supports S3 services or S3-compatible services, then you can continue with the configuration below, but you also need to pay attention to our further instructions. <br></li><li>In other cases, the application may not be able to use COS.</li></td>
</tr>
<tr>
<td>Service endpoint, service address, service URL, endpoint, custom endpoint, server URL, etc.</td>
<td>This indicates the address of an S3-compatible service. If you use COS, enter the COS service address here in the format of <code>cos.&lt;Region&gt;.myqcloud.com</code> or <br><code>https://cos.&lt;Region&gt;.myqcloud.com</code>. <br>Whether <code>https://</code> needs to be entered is determined by the application, and you can make some attempts by yourself. Here, <code>&lt;Region&gt;</code> indicates the availability region of COS. <br>In the application, you can only create or select a bucket in the region specified in the service address. <br><li>For example, if your bucket is in Guangzhou region, the service address should be configured as <code>cos.ap-guangzhou.myqcloud.com</code>; otherwise, you cannot find the bucket in Guangzhou in the application. <br><li>If only <code>Amazon S3</code> can be selected as the application service provider and the service address can be configured, then you can change the service address to the aforementioned <code>cos.&lt;Region>.myqcloud.com</code> or <code>https://cos.&lt;Region>.myqcloud.com</code>. <br><li>If the service address cannot be configured or there is no such configuration item, the application cannot use COS.</td>
</tr>
<tr>
<td>Access key, access key ID, etc.</td>
<td>Enter the <strong>SecretId</strong> obtained in <a href="#step4">step 4</a>.</td>
</tr>
<tr>
<td>Secret key, secret, secret access key, etc.</td>
<td>Enter the <strong>SecretKey</strong> obtained in <a href="#step4">step 4</a>.</td>
</tr>
<tr>
<td>Region, etc.</td>
<td>Select "Default", "Auto", or "Automatic".</td>
</tr>
<tr>
<td>Bucket, etc.</td>
<td>You can select or enter the name of an existing bucket in the format of <code>&lt;BucketName-APPID&gt;</code>, such as <code>examplebucket-1250000000</code>. Here, <code>BucketName</code> is the name you entered when you created the bucket in <a href="#step5">step 5</a>, and <code>APPID</code> is the <strong>`APPID`</strong> obtained in <a href="#step4">step 4</a>. <br>As described above, the bucket must be in the region specified by the service address, and buckets in other regions will not be listed or cannot work properly. If you need to create a bucket, the name of the new bucket should be in the format of <code>&lt;BucketName-APPID&gt;</code> as mentioned above; otherwise, it cannot be properly created.</td>
</tr>
</tbody></table>


### Other advanced configuration items

In addition to the above basic configuration items, some applications have other advanced configuration items. The following describes some COS features for you to better use COS in such applications.

- Service port and protocol
  COS supports both HTTP and HTTPS protocols, with the default ports 80 and 443 used by default. For security considerations, we recommend you use COS over the HTTPS protocol preferably.
- Path-Style and Virtual Hosted-Style
  COS supports both styles.
- AWS v2 and AWS v4 signatures
  COS supports both signature formats.

## Summary

COS does not guarantee full compatibility with S3. If you have any questions when using COS in your application, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance, and be sure to indicate that you followed the steps in this document and provide information such as the application name and screenshots.
