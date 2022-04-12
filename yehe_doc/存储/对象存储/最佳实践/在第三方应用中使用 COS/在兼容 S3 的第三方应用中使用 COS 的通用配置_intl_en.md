Amazon Simple Storage Service (S3) is one of the earliest cloud services provided by AWS. Through many years of development, the S3 protocol has become a standard in the object storage industry. Tencent Cloud Object Storage (COS) provides implementation methods compatible with S3; therefore, you can directly use COS in most of S3 applications. This document describes how to configure such applications with COS.

## Preparations

### Confirming whether an application can use COS

- An application with `S3 Compatible` in its description can use COS in most cases. If you find that some of its features cannot work properly, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance where you should indicate that you followed the steps in this document and provide information such as the application name and screenshots.
- If an application only claims that it supports `Amazon S3`, it can use the S3 service, but whether it supports COS needs to be further confirmed in relevant configuration. Application support for COS will be described in detail in the "Basic configurations" section in this document.

### Preparing the COS service

#### Step 1. Sign up for a Tencent Cloud account

(If you already have a Tencent Cloud account, you can ignore this step.)

<div style="background-color:#00A4FF; width: 355px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/en/account/register" target="_blank"  style="color: white; font-size:16px;">Click here to sign up for a Tencent Cloud account</a></div>

#### Step 2. Verify your identity

(If you have already completed identity verification, you can ignore this step.)

<div style="background-color:#00A4FF; width: 250px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

For more information on how to verify your identity, please see <a href="https://intl.cloud.tencent.com/document/product/378/3629">Identify Verification Overview</a>.

#### Step 3. Activate COS

<div style="background-color:#00A4FF; width: 280px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:16px;">Click here to activate the COS service</a></div>

<span id="step4"></span>
#### Step 4. Prepare the `APPID` and access key

On the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console, get and record the **APPID**, **SecretId**, and **SecretKey**.

![](https://main.qcloudimg.com/raw/974b7e89ba39d4f301daa6deac0711c3.png)

<span id="step5"></span>
#### Step 5. Create a bucket

Some applications have an in-built bucket creation procedure. If you want your application to create a bucket, you can ignore this step.

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket management page.
2. Click **Create Bucket** and enter the bucket information.
	- Name: bucket name, such as `examplebucket`.
	- Region: region where the bucket resides. Please select the region closest to you. For example, if you are in Shenzhen, you can select the Guangzhou region.
	- Access Permission: bucket access permission. For example, you can select "Private Read/Write".
		![](https://main.qcloudimg.com/raw/f8582be0ef7e9cc7bcd52b607e619d4c.png)
3. Click **OK**.


## Configuring COS in Application

### Basic configurations

Most applications have similar configuration items when they are configured with a storage service. Common names and descriptions of these configuration items are as follows:

>? If you have any question during the configuration, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance where you should indicate that you followed the steps in this document and provide information such as the application name and screenshots.


<table>
<thead>
<tr>
<th>Common Name of Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Service Provider, <br>Storage Provider, <br>Provider, etc.</td>
<td>This indicates the storage type to be used by the application and may have the following options: <br><li>If an option contains phrases such as `S3-compatible storage/S3 Compatible`, use it preferably. <br></li><li>If an option contains phrases such as `amazon web services/AWS/Amazon S3`, you can use it but need to pay extra attention to the further description in this document during your subsequent configuration. <br></li><li>If there are no similar options, but the application claims that it supports or is compatible with S3, you can proceed with the configuration but also need to pay extra attention to the further description in this document. <br></li><li>If none of the above is the case, the application may be unable to use COS.</li></td>
</tr>
<tr>
<td>Service Endpoint, Service Address, Service URL, Endpoint, Custom Endpoint, Server URL, etc.</td>
<td>This indicates the address of an S3-compatible service. If you use COS, enter the COS service address here in the format of <code>cos.&lt;Region&gt;.myqcloud.com</code> or <br><code>https://cos.&lt;Region&gt;.myqcloud.com</code>. <br>Whether <code>https://</code> needs to be entered is determined by the application, and you can make some attempts by yourself. Here, <code>&lt;Region&gt;</code> indicates the availability region of COS. <br>In the application, you can only create or select a bucket in the region specified in the service address. <br><li>For example, if your bucket is in the Guangzhou region, the service address should be configured as <code>cos.ap-guangzhou.myqcloud.com</code>; otherwise, you cannot find the bucket in Guangzhou in the application. <br><li>If only <code>Amazon S3</code> can be selected as the application service provider and the service address can be configured, then you can change the service address to the aforementioned <code>cos.&lt;Region>.myqcloud.com</code> or <code>https://cos.&lt;Region>.myqcloud.com</code>. <br><li>If the service address cannot be configured or there is no such configuration item, the application cannot use COS.</td>
</tr>
<tr>
<td>Access Key, Access Key ID, etc.</td>
<td>Here, enter the <strong>`SecretId`</strong> obtained in <a href="#step4">step 4</a>.</td>
</tr>
<tr>
<td>Secret Key, Secret, <br>Secret Access Key, etc.</td>
<td>Here, enter the <strong>`SecretKey`</strong> obtained in <a href="#step4">step 4</a>.</td>
</tr>
<tr>
<td>Region, etc.</td>
<td>Select "Default", "Auto", or "Automatic" for this configuration item.</td>
</tr>
<tr>
<td>Bucket, etc.</td>
<td>You can select or enter the name of an existing bucket in the format of <code>&lt;BucketName-APPID&gt;</code>, such as <code>examplebucket-1250000000</code>. Here, <code>BucketName</code> is the name you entered when you created the bucket in <a href="#step5">step 5</a>, and <code>APPID</code> is the <strong>`APPID`</strong> obtained in <a href="#step4">step 4</a>. <br>As described above, the bucket must be in the region specified by the service address, and buckets in other regions will not be listed or cannot work properly. If you need to create a bucket, the name of the new bucket should be in the format of <code>&lt;BucketName-APPID&gt;</code> as mentioned above; otherwise, it cannot be properly created.</td>
</tr>
</tbody></table>



### Other configuration items and advanced configurations

Some applications have more configuration items such as advanced configurations in addition to the aforementioned ones. Some COS features are further described below for you to better use COS in your application.

- Service port and protocol
  COS supports HTTP and HTTPS protocols, which use ports 80 and 443 by default, respectively. For the sake of security, you are recommended to use HTTPS for COS.
- Path-style and virtual hosted-style
  COS supports both styles.
- AWS V2 signature and AWS V4 signature
  COS supports both signature formats.

## Note

COS does not guarantee full compatibility with S3. If you have any question when using COS in your application, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance where you should indicate that you followed the steps in this document and provide information such as the application name and screenshots.
