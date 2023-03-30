## Resources
- [SDK source code download](https://github.com/TencentCloud/cos-sdk-react-native-plugin)
- [Demo](https://github.com/TencentCloud/cos-sdk-react-native-plugin/tree/main/example)
- [SDK release notes](https://github.com/TencentCloud/cos-sdk-react-native-plugin/blob/master/CHANGELOG.md)
- [NPM address](https://www.npmjs.com/package/react-native-cos-sdk)

## Before You Start

1. You need a pure or native hybrid React Native project, which can be one of your existing projects or a new one.
2. React Native version requirement: v0.69.7 or later.

## Step 1. Learn about the SDK
react-native-cos-sdk is currently compatible with iOS and Android and is implemented by bridging COS' native [Android](https://intl.cloud.tencent.com/document/product/436/12159) and [iOS](https://intl.cloud.tencent.com/document/product/436/11280) SDKs.

## Step 2. Integrate the SDK
1. Run the following command:

Use npm:
```
npm install --save react-native-cos-sdk
```
Or use YARN:
```
yarn add react-native-cos-sdk
```
2. In your code, use `import` to import and start using:
```
import Cos from 'react-native-cos-sdk';
```

## Step 3. Use the SDK

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://www.tencentcloud.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to limit the scope of permission on the permanent key.

### 1. Initialize the key

#### Obtaining a temporary key

Call the `initWithSessionCredentialCallback` method of COS to request a temporary key and return the result.

```ts
import Cos from 'react-native-cos-sdk';

Cos.initWithSessionCredentialCallback(async () => {
  // First, obtain the response containing the key from your temporary key server, for example:
  // URL of the temporary key server
  let stsUrl = "http://stsservice.com/sts";
  const response = await fetch(stsUrl);
  // Then, parse the response to obtain the temporary key
  const responseJson = await response.json();
  const credentials = responseJson.credentials;
  const startTime = responseJson.startTime;
  const expiredTime = responseJson.expiredTime;
  const sessionCredentials = {
    tmpSecretId: credentials.tmpSecretId,
    tmpSecretKey: credentials.tmpSecretKey,
    startTime: startTime,
    expiredTime: expiredTime,
    sessionToken: credentials.sessionToken
  };
  console.log(sessionCredentials);
  // Finally, return the temporary key object
  return sessionCredentials;
})
```

#### Using a permanent key for local debugging

You can use your Tencent Cloud permanent key for local debugging during the development phase. **Since this method exposes the key to leakage risks, please be sure to replace it with a temporary key before launching your application.**

```ts
import Cos from 'react-native-cos-sdk';

let SECRET_ID = "SECRETID"; // `secretId` of the permanent key
let SECRET_KEY = "SECRETKEY"; // `secretKey` of the permanent key

Cos.initWithPlainSecret(
  SECRET_ID,
  SECRET_KEY
)
```

### 2. Register the COS service
```ts
// Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
let region = "COS_REGION";
// Create a `CosXmlServiceConfig` object and modify the configuration parameters as needed
let serviceConfig = {
    region: region,
    isDebuggable: true,
    isHttps: true,
};
// Register the default COS service
let cosService = await Cos.registerDefaultService(serviceConfig);
// Get the default COS Service
let cosService1 = Cos.getDefaultService();

// Create a `TransferConfig` object and modify the configuration parameters as needed
// You can set the object size threshold for multipart upload in `TransferConfig`. By default, the system automatically executes multipart upload for files whose sizes are greater than or equal to 2 MB. You can use the following code to change the threshold:
let transferConfig = {
    forceSimpleUpload: false,
    enableVerification: true,
    divisionForUpload: 2097152, // Set multipart upload for files whose sizes are greater than or equal to 2 MB
    sliceSizeForUpload: 1048576, // Set the default part size to 1 MB
};
// Register the default COS TransferManger
let cosTransferManger = await Cos.registerDefaultTransferManger(serviceConfig, transferConfig);
// Get the default COS TransferManger
let cosTransferManger1 = Cos.getDefaultTransferManger();

// You can also register other instances through `registerService` and `registerTransferManger` for subsequent calls.
// Generally, use `region` as the registration key.
let newRegion = "NEW_COS_REGION";
serviceConfig.region = newRegion;
let cosServiceNew = await Cos.registerService(newRegion, serviceConfig);
let cosTransferMangerNew = await Cos.registerTransferManger(newRegion, serviceConfig, transferConfig);
// Get the COS Service and COS TransferManger through the key
let cosServiceNew1 = Cos.getService(newRegion);
let cosTransferMangerNew1 = Cos.getTransferManger(newRegion);
```

Note: You must register before getting the COS Service and COS TransferManger; otherwise, an error will be reported.
For example, you can control the process where registration is required before acquisition by encapsulating a method similar to the following:
```ts
const SERVICE_CONFIG = {
    region: "COS_REGION",
    isDebuggable: true,
}

export async function getDefaultService(): Promise<CosService> {
  if(Cos.hasDefaultService()){
      return Cos.getDefaultService()
  } else {
      // Register the default service
      return await Cos.registerDefaultService(SERVICE_CONFIG)
  }
}
```

#### Parameter description

`CosXmlServiceConfig` is used to configure the COS service and has the following members:

| Parameter  | Description | Type | Default Value | Supported Platform |
| ---------- | ------------------------------------------------------------ | ------ | ------ |------ |
| region | Bucket region. For more information, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | null | Android, iOS |
| connectionTimeout | Connection timeout period in ms | Int | Android(15000) iOS(30000) | Android, iOS |
| socketTimeout | Read/Write timeout period in ms | Int | 30000 | Android |
| isHttps | Whether to use the HTTPS protocol | Bool | true | Android, iOS |
| host | Sets the host for requests except `GetService` | String | null | Android, iOS |
| hostFormat | Sets the format string of `host`. The SDK will replace \$\{bucket\} and \$\{region\} with the real bucket name and region respectively. <br>For example, if `hostFormat` is set to \$\{bucket\}.\$\{region\}.tencent.com, and your bucket and region are `bucket-1250000000` and `ap-shanghai` respectively, then the final request address will be `bucket-1250000000.ap-shanghai.tencent.com`. <br><li>Note that this setting does not apply to the `GetService` request. | String | null | Android |
| port | Sets the port of the request | Int | null | Android |
| isDebuggable | Whether the debug mode is used (where debug logs will be printed) | Bool | false | Android |
| signInUrl | Whether to put the signature in the URL, which is put in the Header by default. | Bool | false | Android |
| userAgent | UA extended parameter | String | null | Android, iOS |
| dnsCache | Whether to enable the DNS cache. After it is enabled, the DNS result will be cached locally. Then, if the system DNS fails, the locally cached DNS result will be used. | Bool | true | Android |
| accelerate | Whether to use the global acceleration endpoint | Bool | false | Android, iOS |

`TransferConfig` is used to configure the COS upload service and has the following members:

| Parameter  | Description | Type | Default Value | Supported Platform |
| ---------- | ------------------------------------------------------------ | ------ | ------ |------ |
| divisionForUpload | Sets the minimum object size to enable multipart upload | Int | 2097152 | Android, iOS |
| sliceSizeForUpload | Sets the part size during multipart upload  | Int | 1048576 | Android, iOS |
| enableVerification | Whether to verify the entire object during multipart upload | Bool | true | Android, iOS |
| forceSimpleUpload | Whether to forcibly use simple upload | Bool | false | Android |

## Step 4. Access COS

### Uploading an object

```ts
    // Get `CosTransferManger`
    let cosTransferManger: CosTransferManger = Cos.getDefaultTransferManger();
    //let cosTransferManger: CosTransferManger = Cos.getTransferManger(newRegion);
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    let bucket = "examplebucket-1250000000";
    let cosPath = "exampleobject"; //Location identifier of the object in the bucket, i.e., the object key
    let srcPath = "Path of the local file"; // Path of the local file
    // If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. Otherwise, assign `undefined`.
    let _uploadId = undefined;

    // Callback for successful upload
    let successCallBack = (header?: object) => {
      // TODO: Logic after successful upload
    };
    // Callback for failed upload
    let failCallBack = (clientError?: CosXmlClientError, serviceError?: CosXmlServiceError) => {
      // TODO: Logic after failed upload
      if (clientError) {
        console.log(clientError);
      }
      if (serviceError) {
        console.log(serviceError);
      }
    };
    // Callback for the upload status, through which you can check the task process
    let stateCallBack = (state: TransferState) => {
      // todo notify transfer state
    };
    // Callback for the upload progress
    let progressCallBack = (complete: number, target: number) => {
      // todo Do something to update progress...
    };
    // Callback for the completion of multipart upload initialization
    let initMultipleUploadCallBack = (bucket: string, cosKey: string, uploadId: string) => {
      //The uploadId required for the subsequent checkpoint restarts
      _uploadId = uploadId;
    };
    
    // Start the upload
    let transferTask:TransferTask = await cosTransferManger.upload(
      bucket,
      cosPath,
      srcPath,
      {
        uploadId: _uploadId,
        resultListener: {
          successCallBack: successCallBack,
          failCallBack: failCallBack
        },
        stateCallback: stateCallBack,
        progressCallback: progressCallBack,
        initMultipleUploadCallback: initMultipleUploadCallBack,
      }
    );
    // Pause the task
    transferTask.pause();
    // Resume the task
    transferTask.resume();
    // Cancel the task
    transferTask.cancel();
```

### Downloading an object

```ts
    // The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information.
    // If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes HeadObject.

    // `CosTransferManger` supports checkpoint restart for download. You only need to ensure the consistency of parameters `bucket`, `cosPath`, and `savePath`.
    // Then the SDK will resume the download from where interrupted.

    // Get `CosTransferManger`
    let cosTransferManger: CosTransferManger = Cos.getDefaultTransferManger();
    //let cosTransferManger: CosTransferManger = Cos.getTransferManger(newRegion);
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    let bucket = "examplebucket-1250000000";
    let cosPath = "exampleobject"; //Location identifier of the object in the bucket, i.e., the object key
    let downliadPath = "Path of the local file"; // Path of the local file

    // Callback for successful download
    let successCallBack = (header?: object) => {
      // TODO: Logic after successful download
    };
    // Callback for failed download
    let failCallBack = (clientError?: CosXmlClientError, serviceError?: CosXmlServiceError) => {
      // TODO: Logic after failed download
      if (clientError) {
        console.log(clientError);
      }
      if (serviceError) {
        console.log(serviceError);
      }
    };
    // Callback for the download status, through which you can check the task process
    let stateCallBack = (state: TransferState) => {
      // todo notify transfer state
    };
    // Callback for the download progress
    let progressCallBack = (complete: number, target: number) => {
      // todo Do something to download progress...
    };

    // Start the download
    let transferTask:TransferTask = = await cosTransferManger.download(
      bucket,
      cosPath,
      downliadPath,
      {
        resultListener: {
          successCallBack: successCallBack,
          failCallBack: failCallBack
        },
        stateCallback: stateCallBack,
        progressCallback: progressCallBack
      }
    );
    // Pause the task
    transferTask.pause();
    // Resume the task
    transferTask.resume();
    // Cancel the task
    transferTask.cancel();
```
