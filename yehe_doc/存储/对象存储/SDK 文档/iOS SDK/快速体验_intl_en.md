## Overview
This document describes how to configure your client and run the demo.

## Related Resources

All the tools and demos are available in the [Github repository](https://github.com/tencentyun/qcloud-sdk-ios-samples).

## Setting up your Client
### Configuring the client

Modify the file QCloudCOSXMLDemo/QCloudCOSXMLDemo/key.json by adding your APPID, secretID, and secretKey, and then run the following command:

```plaintext
pod install
```
>Get your APPID, secretID and secretKey from the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.

After executing the command, open QCloudCOSXMLDemo.xcworkspace to view the Demo.

### Running the demo

#### Querying a bucket list

Open the example App, and you will see the buckets you have created.

#### Creating a bucket

Click **Create Bucket** in the top-right corner to open the configuration page, enter the bucket name and select the bucket [region](https://intl.cloud.tencent.com/document/product/436/6224).

#### Querying an object list

Select a bucket, and enter its details page where you will see all the files and folders in it.

#### Uploading a file

Click **Upload** in the top-right corner of the file list page, and select files to upload. You can also set their access permission and upload status.

#### Downloading or deleting a file
Click a file name, and then click **Download** or **Delete**.

