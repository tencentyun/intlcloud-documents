## Resources
- [SDK source code download](https://github.com/TencentCloud/cos-sdk-flutter-plugin)
- [Demo](https://github.com/TencentCloud/cos-sdk-flutter-plugin/tree/main/example)
- [SDK changelog](https://github.com/TencentCloud/cos-sdk-flutter-plugin/blob/master/CHANGELOG.md)
- [Pub address](https://pub.flutter-io.cn/packages/tencentcloud_cos_sdk_plugin)

## Preparations

1. You need a pure Flutter project or a Flutter native hybrid project, which can be one of your existing projects or a new one.
2. Flutter version requirement:
```
  sdk: ">=2.12.0 <3.0.0"
  flutter: ">=2.5.0"
```

## Step 1. Learn about the SDK
tencentcloud_cos_sdk_plugin is currently compatible with iOS and Android and is implemented by bridging COS' native [Android](https://intl.cloud.tencent.com/document/product/436/12159) and [iOS](https://intl.cloud.tencent.com/document/product/436/11280) SDKs.

## Step 2. Integrate the SDK
1. Run the following command:
```
flutter pub add tencentcloud_cos_sdk_plugin
```
2. This will add a line like the following to your package's `pubspec.yaml` (and run the implicit `flutter pub get`):
```
dependencies:
  tencentcloud_cos_sdk_plugin: ^1.0.2
```
3. In your Dart code, use `import` to import and start using:
```
import 'package:tencentcloud_cos_sdk_plugin/cos.dart';
```

## Step 3. Use the SDK

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://www.tencentcloud.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to limit the scope of permission on the permanent key.

### 1. Initialize the key

#### Obtaining a temporary key

Implement a `IFetchCredentials` class to request a temporary key and return the result.

```dart
import 'dart:convert';
import 'dart:io';

import 'package:tencentcloud_cos_sdk_plugin/fetch_credentials.dart';
import 'package:tencentcloud_cos_sdk_plugin/pigeon.dart';

class FetchCredentials implements IFetchCredentials{
  @override
  Future<SessionQCloudCredentials> fetchSessionCredentials() async {
    // First, obtain the response containing the key from your temporary key server, for example:
    var httpClient = HttpClient();
    try{
      // URL of the temporary key server
      var stsUrl = "http://stsservice.com/sts";
      var request = await httpClient.getUrl(Uri.parse(stsUrl));
      var response = await request.close();
      if (response.statusCode == HttpStatus.OK) {
        var json = await response.transform(utf8.decoder).join();
        print(json);

        // Then, parse the response to obtain the temporary key
        var data = jsonDecode(json);
        // Finally, return the temporary key object
        return SessionQCloudCredentials(
            secretId: data['credentials']['tmpSecretId'],// `SecretId` of the temporary key
            secretKey: data['credentials']['tmpSecretKey'],// `SecretKey` of the temporary key
            token: data['credentials']['sessionToken'],// `Token` of the temporary key
            startTime: data['startTime'],// Start timestamp (in seconds) of the effective period of the temporary key
            expiredTime: data['expiredTime']// End timestamp (in seconds) of the effective period of the temporary key
        );
      } else {
        throw ArgumentError();
      }
    } catch (exception) {
      throw ArgumentError();
    }
  }
}
```

The following takes `FetchCredentials` as an example class name to initialize an instance to provide a key for the SDK.

```dart
Cos().initWithSessionCredential(FetchCredentials());
```

#### Using a permanent key for local debugging

You can use your Tencent Cloud permanent key for local debugging during the development phase. **Since this method exposes the key to leakage risks, please be sure to replace it with a temporary key before launching your application.**

```dart
String SECRET_ID = "SECRETID"; // `secretId` of the permanent key
String SECRET_KEY = "SECRETKEY"; // `secretKey` of the permanent key

Cos().initWithPlainSecret(SECRET_ID, SECRET_KEY);
```

### 2. Register the COS service
```dart
// Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
String region = "COS_REGION";
// Create a `CosXmlServiceConfig` object and modify the configuration parameters as needed
CosXmlServiceConfig serviceConfig = CosXmlServiceConfig(
    region: region,
    isDebuggable: true,
    isHttps: true,
);
// Register the default COS service
Cos().registerDefaultService(serviceConfig);

// Create a `TransferConfig` object and modify the configuration parameters as needed
// You can set the object size threshold for multipart upload in `TransferConfig`. By default, the system automatically executes multipart upload for files whose sizes are greater than or equal to 2 MB. You can use the following code to change the threshold:
TransferConfig transferConfig = TransferConfig(
    forceSimpleUpload: false,
    enableVerification: true,
    divisionForUpload: 2097152, // Set multipart upload for files whose sizes are greater than or equal to 2 MB
    sliceSizeForUpload: 1048576, // Set the default part size to 1 MB
);
// Register the default COS TransferManger
Cos().registerDefaultTransferManger(serviceConfig, transferConfig);

// You can also register other instances through `registerService` and `registerTransferManger` for subsequent calls.
// Generally, use `region` as the registration key.
String newRegion = "NEW_COS_REGION";
Cos().registerService(newRegion, serviceConfig..region = newRegion);
Cos().registerTransferManger(newRegion, serviceConfig..region = newRegion, transferConfig);
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

The SDK supports uploading local files and binary data. The following uses uploading a local file as an example:

```dart
    // Get the `TransferManager`
    CosTransferManger transferManager = Cos().getDefaultTransferManger();
    //CosTransferManger transferManager = Cos().getTransferManger("newRegion");
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    String bucket = "examplebucket-1250000000";
    String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
    String srcPath = "Absolute path of the local file"; // Absolute path of the local file
    // If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. Otherwise, assign null
    String? _uploadId;

    // Callback for successful upload
    successCallBack(result) {
      // TODO: Logic after successful upload
    }
    // Callback for failed upload
    failCallBack(clientException, serviceException) {
      // TODO: Logic after failed upload
      if (clientException != null) {
        print(clientException);
      }
      if (serviceException != null) {
        print(serviceException);
      }
    }
    // Callback for the upload status, through which you can check the task process
    stateCallback(state) {
      // todo notify transfer state
    }
    // Callback for the upload progress
    progressCallBack(complete, target) {
      // todo Do something to update progress...
    }
    // Callback for the completion of multipart upload initialization
    initMultipleUploadCallback(
        String bucket, String cosKey, String uploadId) {
      //The uploadId required for the subsequent checkpoint restarts
      _uploadId = uploadId;
    }
    // Start the upload
    TransferTask transferTask = await transferManager.upload(bucket, cosPath,
        filePath: srcPath,
        uploadId: _uploadId,
        resultListener: ResultListener(successCallBack, failCallBack),
        stateCallback: stateCallback,
        progressCallBack: progressCallBack,
        initMultipleUploadCallback: initMultipleUploadCallback
    );
    // Pause the task
    transferTask.pause();
    // Resume the task
    transferTask.resume();
    // Cancel the task
    transferTask.cancel();
```

### Download an object

```dart
    // The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information.
    // If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes HeadObject.

    // `TransferManager` supports checkpoint restart for download. You only need to ensure the consistency of parameters `bucket`, `cosPath`, and `savePath`.
    // Then the SDK will resume the download from where interrupted.

    // Get the `TransferManager`
    CosTransferManger transferManager = Cos().getDefaultTransferManger();
    //CosTransferManger transferManager = Cos().getTransferManger("newRegion");
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    String bucket = "examplebucket-1250000000";
    String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
    String downliadPath = "Absolute path of the local file"; // Absolute path of the local file

    // Callback for successful download
    successCallBack(result) {
      // TODO: Logic after successful download
    }
    // Callback for failed download
    failCallBack(clientException, serviceException) {
      // TODO: Logic after failed download
      if (clientException != null) {
        print(clientException);
      }
      if (serviceException != null) {
        print(serviceException);
      }
    }
    // Callback for the download status, through which you can check the task process
    stateCallback(state) {
      // todo notify transfer state
    }
    // Callback for the download progress
    progressCallBack(complete, target) {
      // todo Do something to download progress...
    }
    // Start the download
    TransferTask transferTask = await transferManager.download(bucket, cosPath, downliadPath, 
        resultListener: ResultListener(successCallBack, failCallBack),
        stateCallback: stateCallback,
        progressCallBack: progressCallBack
    );
    // Pause the task
    transferTask.pause();
    // Resume the task
    transferTask.resume();
    // Cancel the task
    transferTask.cancel();
```
