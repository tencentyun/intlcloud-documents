## Overview

You can store multimedia content in WordPress to Tencent Cloud COS through a third-party plugin for the following benefits:

- Multimedia content can be more reliable.
- You don't have to prepare additional storage capacity on your server for multimedia content.
- Visitors' requests to view and download multimedia content can be redirected to COS servers for faster access without consuming your downstream bandwidth/traffic.
- Tencent Cloud CDN can be leveraged to further accelerate visitor's requests to view and download multimedia content.

### Preparations

1. Build WordPress.
	- You can download the latest version of WordPress and view installation instructions at [WordPress's official website](https://wordpress.org/download/).
2. Create a **Public Read/Private Write** bucket as instructed in [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309), preferably in the same region as the CVM instance where WordPress runs.
3. Find the just created bucket in the bucket list and note down its **name** and **region abbreviation**. For more information on region abbreviations, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
	 ![](https://main.qcloudimg.com/raw/c870439faef702733e9ba18085b74a08.png)
4. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) and note down the **`SecretId`** and **`SecretKey`**.
   ![](https://main.qcloudimg.com/raw/4345f6d65e385fe85256ddfa853e73d4.png)

## Installing and Configuring the WordPress Plugin

1. Log in to the WordPress **Dashboard**.
2. On the left sidebar, select **Plugins** > **Add New** to enter the plugin installation page. Search for and install the **Media Cloud** plugin here.
   ![](https://main.qcloudimg.com/raw/bdf45611e8da6480b73fdb6a826f2540.png)
3. Start the **Media Cloud** plugin. The Setup Wizard will be automatically launched. Click **NEXT**.
> If the Setup Wizard is not automatically launched, select **Media Cloud** on the left sidebar in the WordPress Dashboard and click **Setup Wizard** below **Cloud Storage**.
>![](https://main.qcloudimg.com/raw/4e217b187497555d4fa10b5d748642a2.png)
4. On the "Choose Your Storage Provider" page, select **S3 Compatible** and click **NEXT**.
	 ![](https://main.qcloudimg.com/raw/d80c199ab89ce3bd3e8ff67eee1ae5b0.jpg)
5. Configure the displayed form as follows and click **NEXT**:
<table>
<thead>
<tr>
<th nowrap="nowrap">Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">ACCESS KEY</td>
<td><strong>`SecretId`</strong> in the access key</td>
</tr>
<tr>
<td>SECRET</td>
<td><strong>`SecretKey`</strong> in the access key</td>
</tr>
<tr>
<td>BUCKET</td>
<td><strong>Bucket name</strong></td>
</tr>
<tr>
<td>REGION</td>
<td>Select <strong>"Automatic"</strong></td>
</tr>
<tr>
<td>CUSTOM ENDPOINT</td>
<td>Format: <code>cos.&lt;Region&gt;.myqcloud.com</code>, where `&lt;Region&gt;` is the <strong>region abbreviation</strong> of the bucket; for example, if the Guangzhou region (abbreviation: ap-guangzhou) is used, enter <code>cos.ap-guangzhou.myqcloud.com</code> here</td>
</tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/cc7d9766d5148873fa5fe6ba3eeee2b2.jpg"></img>
6. At this point, Media Cloud will test whether the configuration is correct. Click **START TESTS** to start the test and click **NEXT** after all test items pass.
	 ![](https://main.qcloudimg.com/raw/db2aba4cd987b9114b9165ae72106e3f.jpg)
7. Media Cloud will display that "You are ready to use Media Cloud!". Click **ADVANCED SETTINGS** to close the Setup Wizard.
<img src="https://main.qcloudimg.com/raw/5f838b8215ace7fa20150110f8f7d313.jpg" width="100%"></img>

## Testing Multimedia Content

1. Write an article, add multimedia content to it, and publish it.
<img src="https://main.qcloudimg.com/raw/b55edab7cca56ed7d2fd4c92eba41e17.png" width="100%"></img>
2. Copy the image address in the article or use a browser debugger to view the image path. As can be seen, the image address is an address on COS (as shown in box 1 in the screenshot in step 3).
3. View the download address of the article attachment. As can be seen, the download address also points to COS (as shown in box 2 below).
<img src="https://main.qcloudimg.com/raw/fc877fc5b4b85f403420bd6467fa74ac.png" width="100%"></img>



## Using Tencent Cloud CDN

1. If you want to configure CDN acceleration for the bucket saved in the WordPress attachment, follow the steps in [CDN Acceleration Configuration](https://intl.cloud.tencent.com/document/product/436/18670).
2. Enter the management page of Media Cloud and click **Settings** below **Cloud Storage**.
![](https://main.qcloudimg.com/raw/9a8091ed7562e12955a54d088f31a251.png)
3. Set the **CDN Base URL** in **CDN SETTINGS** to your CDN domain name, such as the default acceleration domain name for COS `https://wordpress-1250000000.file.myqcloud.com/` or your custom acceleration domain name `https://static.foo.bar/`.
![](https://main.qcloudimg.com/raw/5eb0c4f85ad3d393198057dfaf64b4c8.png)
4. Check the multimedia content in the previously published article. As can be seen, the address points to the CDN domain name you configured.
![](https://main.qcloudimg.com/raw/cffd2acdc27873d56c40804bb108a55f.png)
