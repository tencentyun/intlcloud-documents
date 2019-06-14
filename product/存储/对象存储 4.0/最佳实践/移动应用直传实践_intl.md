## Overview

This document describes how to set up file direct transfer with Tencent Cloud COS for your mobile applications. COS (Cloud Object Storages) makes it easy for you to store files and data as you only need to generate and manage the access key on your server. 

## Product Architecture

For client applications,  storing permanent keys in the code increases the risk that your credentials could leak and makes it difficult to control access permissions. We recommend that your applications use temporary keys with a specified validity period to access your COS resources to prevent credential leakage.

The COS Mobile SDK (Android/IOS) allows you to apply temporary keys on COS access request authorization. You only need to set up the temporary key service at the backend to authorize the requests.

### Workflow
The graph below illustrates how to enable CAM for the COS:
![cos接入cam框架图](https://main.qcloudimg.com/raw/cf0a69ff91770578f70b05873bb1b348.png)

Where:

- User's client: User's mobile App.
- COS：[Cloud Object Storage](https://intl.cloud.tencent.com/product/cos), which stores the data uploaded from App.
- CAM：[Cloud Access Management](https://intl.cloud.tencent.com/product/cam), which is used to generate temporary keys for COS.
- App's server: user's backend server, which is used to obtain the temporary keys and return them to the App.

## Preparations

### Create a bucket

Create a bucket on the [COS Console](https://console.cloud.tencent.com/cos/bucket). Set the bucket permission to "Private Read/Write" or "Public Read/Private Write" as needed.

### Obtain the permanent key

You need to get the permanent key to generate temporary keys. Log in to [API Key Management](https://console.cloud.tencent.com/cam/capi) to get the permanent keys, including:

- SecretId
- SecretKey
- AppID
  
## Setting Up Temporary Key Service

For security purposes, we recommend you to use temporary keys to calculate a signature. To create and use temporary keys, you need to set up the temporary key service on your server and an API for your application.

> For higher security, when deploying the temporary key service, add an additional layer of website authentication on the server side.

### Select appropriate permissions

We recommended that you define a scope for the permission granted to temporary keys through Policy based on the principle of "least privilege". A key that has all permissions to read and write the data increases the risk that other users’ data could leak. For more information, see [Temporary Key Generation and Usage Guide](https://intl.cloud.tencent.com/document/product/436/14048).

## Integrating SDK with Authorization Service

### Android

After the temporary key service is set up, you integrate the SDK with the authorization service. Instead of you managing the temporary keys, the SDK controls the number of concurrent requests to process, cache the valid keys on your local devices, and request new keys to replace the expired ones.

#### Authorization with standard response body

If you use the JSON data obtained from the STS SDK as a response body for the temporary key service (similar to cossign), you can create an authorization class in the COS SDK using the following code:

```
CosXmlServiceConfig cosXmlServiceConfig = ...;

/**
 * Get the URL of the authorization service
 */
URL url = null; //URL of the authorization service in the application server
try {
    url = new URL("your_auth_server_url");
} catch (MalformedURLException e) {
    e.printStackTrace();
}

/**
 * Initialize the {@link QCloudCredentialProvider} object to provide temporary keys to the SDK. 
 */
QCloudCredentialProvider credentialProvider = new SessionCredentialProvider(new HttpRequest.Builder<String>()
                .url(url)
                .method("GET")
                .build());
                
CosXmlService cosXmlService = new CosXmlService(this, cosXmlServiceConfig, credentialProvider);                
```
> Because this method requires that the signature start time matches the local time on your mobile phone.  The large difference (more than 10 minutes) between the time on your phone and the correct local time may cause a signature error. In this case, you can use the custom response body for authorization as discussed below:

#### Authorization with custom response body

This method gives you higher flexibility. For example, you can customize the HTTP response body for your temporary key service so that the signature start time can change as the time the endpoint response changes, thus preventing signature errors due to the large time difference.  Or you can adopt other protocols for the client and the server communicating with each other, then you can use `fetchNewCredentials()` in class `BasicLifecycleCredentialProvider`:

Define a `MyCredentialProvider` class first:

```java
public class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {
       
        // Get a response containing the signature information from your temporary key server;
        ....
        
        // Parse the response to acquire the key information;
        String tmpSecretId = ...;
        String tmpSecretKey = ...;
        String sessionToken = ...;
        long expiredTime = ...;
        
        // Return the server time as the start time of the signature;
        long beginTime = ...;
         
        // todo something you want
         
        // Return the temporary key information object. 
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey, sessionToken, beginTime, expiredTime);
    }
}
```
Authorize the request with the your defined `MyCredentialProvider` instance:

```
CosXmlServiceConfig cosXmlServiceConfig = ...;
        
/**
 * Initialize the {@link QCloudCredentialProvider} object to provide temporary keys to the SDK. 
 */
QCloudCredentialProvider credentialProvider = new MyCredentialProvider();

CosXmlService cosXmlService = new CosXmlService(this, cosXmlServiceConfig, credentialProvider);   
```

For complete sample code, see [Android COS Transfer](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransfer).

For more information on how files are uploaded and downloaded between an Android device and COS, see [Getting Started With Android SDK](https://intl.cloud.tencent.com/document/product/436/12159).

### iOS

We provide QCloudCredentailFenceQueue to make it easier for you to obtain and manage temporary signatures. With QCloudCredentailFenceQueue, a request for signature will be processed only after the signature is calculated. 

To use QCloudCredentailFenceQueue, you first need to create an instance.

```
 //AppDelegate.m
//AppDelegate must follow QCloudCredentailFenceQueueDelegate protocol
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}

```

Next, the class that calls QCloudCredentailFenceQueue must follow QCloudCredentailFenceQueueDelegate and implement the method defined in the protocol:

```
 - (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

When you obtain the signature using QCloudCredentailFenceQueue, all the requests in the SDK that need to sign will not be performed until you acquires required parameters using the protocal-defined method and a valid signature is created. See the example below:

```
- (void)fenceQueue:(QCloudCredentailFenceQueue *)queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock {
    QCloudHTTPRequest* request = [QCloudHTTPRequest new];
    request.requestData.serverURL = @“your sign service url”;//Requested URL
    
    [request setConfigureBlock:^(QCloudRequestSerializer *requestSerializer, QCloudResponseSerializer *responseSerializer) {
        requestSerializer.serializerBlocks = @[QCloudURLFuseWithURLEncodeParamters];
        responseSerializer.serializerBlocks = @[QCloudAcceptRespnseCodeBlock([NSSet setWithObjects:@(200), nil],nil),//Specifies that an error is returned if the return code is a code other than 200.
                                                QCloudResponseJSONSerilizerBlock];//Parse the returned data in JSON format
    }];
    
    [request setFinishBlock:^(id response, NSError *error) {
        if (error) {
            error = [NSError errorWithDomain:@"com.tac.test" code:-1111 userInfo:@{NSLocalizedDescriptionKey:@"No temporary key is obtained"}];
            continueBlock(nil, error);
        } else {
            QCloudCredential* crendential = [[QCloudCredential alloc] init];
            crendential.secretID = response[@"data"][@"credentials"][@"tmpSecretId"];
            crendential.secretKey = response[@"data"][@"credentials"][@"tmpSecretKey"];
            credential.startDate =[NSDate dateWithTimeIntervalSince1970:@"Returned server time"]
            crendential.experationDate = [NSDate dateWithTimeIntervalSinceNow:[response[@"data"][@"expiredTime"] intValue]];
            crendential.token = response[@"data"][@"credentials"][@"sessionToken"];;
            QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:crendential];
            continueBlock(creator, nil);
            
        }
    }];
    [[QCloudHTTPSessionManager shareClient] performRequest:request];
}
```

For more information about how to directly transfer files between COS and iOS applications, see [Getting Started With iOS SDK](https://intl.cloud.tencent.com/document/product/436/11280).


## Demo Code

### Android 

Download the Demo by clicking [here](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk), or scanning QR code with your Android phone:

Download the Demo by clicking [here](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk), or scanning QR code with your Android phone:
> parent of b3f10c0cd1... Revert "Merge branch 'master' of https://github.com/tencentyun/qcloud-documents"

![](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice-download.png)

For complete code, see [COS Android Demo](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice).

### iOS

For complete sample project for iOS, see [COS iOS Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/OOTB-XML).

Modify the file QCloudCOSXMLDemo/QCloudCOSXMLDemo/TestCommonDefine.h, enter the AppID and the address deployed in the previous step for getting the temporary keys, and then run the following command:

```sh
pod install
```

After executing the command, open QCloudCOSXMLDemo.xcworkspace to view the Demo.

