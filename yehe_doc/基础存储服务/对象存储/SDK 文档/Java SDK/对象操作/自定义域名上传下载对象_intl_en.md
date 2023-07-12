## Overview

This document describes how to upload and download objects at a custom domain name. Advanced APIs are used in the samples in this document for uploading and downloading objects. For more information, see [Uploading Object](https://intl.cloud.tencent.com/document/product/436/44015) and [Downloading Object](https://intl.cloud.tencent.com/document/product/436/44016).

Before using a custom domain name to upload and download objects, you first need to set the custom origin domain name for the bucket as instructed in [Enabling Custom Origin Domain Name](https://intl.cloud.tencent.com/document/product/436/31507).

## Uploading Object at Custom Domain Name

#### Method prototype

```java
// `UserSpecifiedEndpointBuilder` constructor
com.qcloud.cos.endpoint.UserSpecifiedEndpointBuilder(String generalApiEndpoint, String getServiceApiEndpoint);
```

#### Sample request

```java
import java.io.File;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import com.qcloud.cos.COSClient;
import com.qcloud.cos.ClientConfig;
import com.qcloud.cos.auth.BasicCOSCredentials;
import com.qcloud.cos.auth.COSCredentials;
import com.qcloud.cos.endpoint.UserSpecifiedEndpointBuilder;
import com.qcloud.cos.exception.CosClientException;
import com.qcloud.cos.exception.CosServiceException;
import com.qcloud.cos.http.HttpProtocol;
import com.qcloud.cos.model.PutObjectRequest;
import com.qcloud.cos.model.UploadResult;
import com.qcloud.cos.region.Region;
import com.qcloud.cos.transfer.TransferManager;
import com.qcloud.cos.transfer.Upload;
 
public static void uploadFile() {
 // 1. Initialize the authentication information (`secretId` and `secretKey`).
    COSCredentials cred = new BasicCOSCredentials("secretId", "secretKey");
 // 2. Set the bucket region (COS_REGION). For valid values, visit https://www.qcloud.com/document/product/436/6224.
    ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));
 // Set the request protocol. HTTPS is recommended.
    clientConfig.setHttpProtocol(HttpProtocol.https);
    // If no HTTPS certificate is uploaded when the custom origin domain name is configured, change this line to `clientConfig.setHttpProtocol(HttpProtocol.http);`.
 // Set a custom domain name.
    UserSpecifiedEndpointBuilder endpointBuilder = new UserSpecifiedEndpointBuilder("generalApiEndpoint", "getServiceApiEndpoint");
    clientConfig.setEndpointBuilder(endpointBuilder);
 // 3. Generate a COS client.
    COSClient cosclient = new COSClient(cred, clientConfig);
 // The bucket name must contain `appid`.
    String bucketName = "BucketName-APPID";

    ExecutorService threadPool = Executors.newFixedThreadPool(32);
 // Pass a `threadpool`; otherwise, a single-thread pool will be generated in `TransferManager` by default.
    TransferManager transferManager = new TransferManager(cosclient, threadPool);
 // Set the object key
    String key = "exampleobject";
 // Local file path  
    File localFile = new File("/path/to/localFile");

    PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
    try {
      // Return an async result `Upload`. You can synchronously call `waitForUploadResult` to wait for the upload to complete. If the upload is successful, `UploadResult` will be returned; otherwise, an exception will be reported.
        Upload upload = transferManager.upload(putObjectRequest);
        UploadResult uploadResult = upload.waitForUploadResult();
        System.out.printf("RequestId : %s\n",uploadResult.getRequestId());
        System.out.println(uploadResult.getETag());
        System.out.println(uploadResult.getCrc64Ecma());
    } catch (CosServiceException e) {
        e.printStackTrace();
    } catch (CosClientException e) {
        e.printStackTrace();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }

	  transferManager.shutdownNow();
}
```

##### Parameter descriptions

| Parameter | Description | Type |
| :-------------------: | :-----------------------------------------------------: | :----: |
|  generalApiEndpoint   |                     Custom origin domain name                      | String |
| getServiceApiEndpoint | The domain name used to get the bucket list. We recommend you enter `service.cos.myqcloud.com`. | String |

## Downloading Object at Custom Domain Name

#### Method prototype

```java
// `UserSpecifiedEndpointBuilder` constructor
com.qcloud.cos.endpoint.UserSpecifiedEndpointBuilder(String generalApiEndpoint, String getServiceApiEndpoint);
```

#### Sample request

```java
import java.io.File;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import com.qcloud.cos.COSClient;
import com.qcloud.cos.ClientConfig;
import com.qcloud.cos.auth.BasicCOSCredentials;
import com.qcloud.cos.auth.COSCredentials;
import com.qcloud.cos.endpoint.UserSpecifiedEndpointBuilder;
import com.qcloud.cos.exception.CosClientException;
import com.qcloud.cos.exception.CosServiceException;
import com.qcloud.cos.http.HttpProtocol;
import com.qcloud.cos.model.GetObjectRequest;
import com.qcloud.cos.region.Region;
import com.qcloud.cos.transfer.Download;
import com.qcloud.cos.transfer.TransferManager;
 
public static void downLoadFile() {
 // 1. Initialize user authentication information (`secretId`, `secretKey`).
    COSCredentials cred = new BasicCOSCredentials("secretId", "secretKey");
 // 2. Set the bucket region (COS_REGION). For valid values, visit https://www.qcloud.com/document/product/436/6224.
    ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));
 // Set the request protocol. HTTPS is recommended.
    clientConfig.setHttpProtocol(HttpProtocol.https);
    // If no HTTPS certificate is uploaded when the custom origin domain name is configured, change this line to `clientConfig.setHttpProtocol(HttpProtocol.http);`.
 // Set a custom domain name.
    UserSpecifiedEndpointBuilder endpointBuilder = new UserSpecifiedEndpointBuilder("generalApiEndpoint", "getServiceApiEndpoint");
    clientConfig.setEndpointBuilder(endpointBuilder);
 // 3. Generate a COS client.
    COSClient cosclient = new COSClient(cred, clientConfig);
 // The bucket name must contain `appid`.
    String bucketName = "BucketName-APPID";

    ExecutorService threadPool = Executors.newFixedThreadPool(32);
 // Pass a `threadpool`; otherwise, a single-thread pool will be generated in `TransferManager` by default.
    TransferManager transferManager = new TransferManager(cosclient, threadPool);
 // Set the object key
    String key = "exampleobject";
 // Local file path  
		File downloadFile = new File("/path/to/localFile");
    GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
    try {
      // Return an async result `download`. You can synchronously call `waitForCompletion` to wait for the download to complete. If the download is successful, `void` will be returned; otherwise, an exception will be reported.
        Download download = transferManager.download(getObjectRequest, downloadFile);
        download.waitForCompletion();
        System.out.printf("RequestId : %s\n",download.getObjectMetadata().getRequestId());
    } catch (CosServiceException e) {
        e.printStackTrace();
    } catch (CosClientException e) {
        e.printStackTrace();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }

    transferManager.shutdownNow();
}
```

##### Parameter descriptions

| Parameter | Description | Type |
| :-------------------: | :-----------------------------------------------------: | :----: |
|  generalApiEndpoint   |                     Custom origin domain name                      | String |
| getServiceApiEndpoint | The domain name used to get the bucket list. We recommend you enter `service.cos.myqcloud.com`. | String |

