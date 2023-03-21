## Background
Apps are the building blocks of the mobile internet, and they often require massive data uploads and downloads. Therefore, data security and reliability are crucial. Developers can let [Tencent Cloud COS](https://www.tencentcloud.com/products/cos) handle data storage, and can focus on their app business logics to reduce workload and improve development efficiency. This document describes how to quickly build a COS-based app transfer service to upload and download app data on Tencent Cloud COS. All you need to do is deploy your businesses and generate and manage temporary keys on your server.

COS provides a demo, which you can run as instructed below.

## Resources

Download the demo from the repository on [GitHub](https://github.com/TencentCloud/cos-sdk-flutter-plugin/tree/main/example).

## Preparations
- System version: Android 4.1 and later or iOS 11 and later.
- Your temporary key server or permanent key (`SecretId` and `SecretKey` can be obtained from the [Manage API Key](https://console.cloud.tencent.com/capi) page in the Tencent Cloud console).
- Tencent Cloud `APPID` (if you need to try out the bucket adding feature).

## Setting up Your Client

### Configuring the client

1. Download the project files from [GitHub](https://github.com/TencentCloud/cos-sdk-flutter-plugin/tree/main/example) and open them in your IDE.
2. Create `config.dart` as instructed in the `example/lib/config/config.template` file and modify relevant values.
3. Run your project to try out the demo.

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://www.tencentcloud.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, do not expose the plaintext of `SecretId` and `SecretKey` to unsecured environments, and we recommend that you follow the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to limit the scope of permission on the permanent key.

### Running the Demo

#### Querying a bucket list
Open the sample app, and you will see all the buckets that you have created.



#### Creating a bucket
Click **+Create Bucket** in the top-right corner to open the configuration page, enter the bucket name and select the bucket [region](https://www.tencentcloud.com/document/product/436/6224).



#### Querying an object list

Click a bucket, and you will see all the files and folders that it contains.



#### Uploading an object
On the file list page, click **Upload** in the top-right corner and select the file to be uploaded.



#### Downloading an object
In the object list, click **Download** below a file to download it.


