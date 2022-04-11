## Background
Applications are the building blocks of the mobile Internet. As they often require massive data upload and download, data security and reliability are extremely crucial. Now, developers can let [Tencent Cloud COS（Cloud Object Storage）](https://intl.cloud.tencent.com/product/cos) handle data storage for them, allowing them to solely focus on the business logic of their applications with a lighter workload and higher development efficiency. This document describes how to quickly build a COS-based application transfer service to upload and download your application data through Tencent Cloud COS. All you need to do is deploy your business components and generate and manage temporary keys on your server.

COS provides a demo for XML, which you can run as instructed below.

## Relevant Resources

Download the demo from the repository on [GitHub](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice).

## Preparations
- Android OS: 4.4 or above.
- Your APPID, SecretId, and SecretKey from the [API Key Management](https://console.cloud.tencent.com/capi) page on the Tencent Cloud console.

## Setting up a User's Application Client

### Configuring the client

1. Download the project files from [GitHub](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice), and open them in your IDE.
2. Configure your COS_APP_ID, SecretId、SecretKey in the environment variables.
3. Run your project to try out the demo.

>!
>- Do not expose your plaintext SecretId or SecretKey to any unsecure environments.
>- The `ShortTimeCredentialProvider` authorization method in the demo is simply used for demonstration purposes and should not be used in your production environment. Instead, we recommend [authorizing via temporary keys](https://intl.cloud.tencent.com/document/product/436/12159).
>- After the environment variables have been altered, you may need to restart Android Studio  for the updated configuration to take effect.

### Running the Demo

#### Querying a bucket list
Open the sample app, and you will see all the buckets that you have created.

#### Creating a bucket
Click **New Bucket** in the upper right-hand corner, enter the bucket name on the configuration page, and select the [region](https://intl.cloud.tencent.com/document/product/436/6224) in which the bucket resides.

#### Querying an object list

Click on a bucket, and you will see all the files and folders that it contains.

#### Uploading a file
On the file list page, click **Upload** in the upper right corner, and select the file to upload.

#### Downloading a file
On the file list page, click **Download** below a file to directly download it.
