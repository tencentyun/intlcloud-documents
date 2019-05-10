## Background

This document describes how to quickly implement file direct transfer for App development based on Tencent Cloud's COS. All file data is stored in Tencent Cloud's COS, so you only need to generate and manage access keys on your server.

## Architecture

For an application on client, putting a permanent key in the client code may cause the leakage of your key and makes it difficult to control user access permissions. It is recommend to temporarily authorize your App to access your resources in storage by including temporary keys into the request to prevent the leakage of your permanent key. You can specify the temporary keys' validity period, beyond which the keys expire automatically.

The COS Mobile SDK (Android/IOS) supports the authorization of requests through temporary keys. You only need to set up a temporary key service at backend to seamlessly authorize the requests sent from terminal to COS.

### Workflow
The workflow is as follows:
![cos接入cam框架图](http://mc.qcloudimg.com/static/img/b1e187a9ec129ffc766c07a733ef4dd6/image.jpg)

Where:

- User's client: User's mobile App.
- COS：[Cloud Object Storage](https://cloud.tencent.com/product/cos), which stores the data uploaded from App.
- CAM：[Cloud Access Management](https://cloud.tencent.com/product/cam), which is used to generate temporary keys for COS.
- App's server: user's backend server, which is used to obtain the temporary keys and return them to the App.

## Preparations

### Create a bucket

Create a bucket on the [COS Console](https://console.cloud.tencent.com/cos/bucket). Set the bucket permission to "Private Read/Write" or "Public Read/Private Write" as needed.

### Obtain the permanent key

Permanent keys are required to generate temporary keys. Log in to [API Key Management](https://console.cloud.tencent.com/cam/capi) to get the permanent keys, including:

- SecretId
- SecretKey
- AppID
  
## Setting Up Temporary Key Service

For security reasons, temporary key service needs to be set up at the server before temporary keys can be used for signatures. For more information, see [Temporary Key Generation and Usage Guide](https://cloud.tencent.com/document/product/436/14048).

>! During deployment, configure a permission verification mechanism additionally for your website at the server.

### Select appropriate permissions

It is recommended to control the permission scope of temporary keys through Policy as needed based on the principle of "least privilege". If the server delivers a key with full read and write permissions, an attack may cause data leakage of other users. For more information, see [Temporary Key Generation and Usage Guide](https://cloud.tencent.com/document/product/436/14048).

## Integrating SDK with Authorization Service

### Android

After setting up the temporary key service, you need to integrate the SDK with the authorization service. The SDK controls the number of concurrent requests, cache the valid keys locally, and request the keys again after they expire. You do not need to manage the acquired keys yourself.

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
>?For this method, the start time of the signature is your mobile phone's local time. Therefore, in case of a large deviation of the phone's local time from standard time (more than 10 minutes), the signature error may occur. In this case, you can use the following custom response body for authorization.

#### Authorization with custom response body

If you want more flexibility to, for example, customize the HTTP response body of the temporary key service to return the server time to the terminal as the start time of signature, thus avoiding incorrect signature caused by large deviation of mobile phone's local time from the standard time, or realize communication between the terminal and server using other protocols, you can inherit the `BasicLifecycleCredentialProvider` class and implement its `fetchNewCredentials()`:

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

For more information on how files are uploaded and downloaded between an Android device and COS, see [Getting Started With Android SDK](https://cloud.tencent.com/document/product/436/12159).

### iOS

We provide QCloudCredentailFenceQueue to make it easier for you to obtain and manage temporary signatures. QCloudCredentailFenceQueue comes with a fencing mechanism, which means that if you obtain the signature using QCloudCredentailFenceQueue, any request for a signature will be performed only after the signature process is completed. This can eliminate the need to manage the asynchronous process.

To use QCloudCredentailFenceQueue, generate an instance first.

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

When you obtain the signature using QCloudCredentailFenceQueue, all the requests in the SDK that need signatures will not be performed until the parameters required for the signature are obtained via the method defined by the protocol and a valid signature is generated. See the example below:

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

For more information on how files are uploaded and downloaded between an iOS device and COS, see [Getting Started With iOS SDK]().


## Try Out with Demo Code

### Android 

<<<<<<< HEAD
Download the Demo by clicking [here](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk), or scanning QR code with your Android phone:
=======
Download the Demo by clicking [here](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk), or scanning QR code with your Android phone:
>>>>>>> parent of b3f10c0cd1... Revert "Merge branch 'master' of https://github.com/tencentyun/qcloud-documents"

![](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice-download.png)
 
For complete code, see [COS Android Demo](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice).

### iOS

For complete sample project for iOS, see [COS iOS Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/OOTB-XML).

Modify the file QCloudCOSXMLDemo/QCloudCOSXMLDemo/TestCommonDefine.h, enter the AppID and the address deployed in the previous step for getting the temporary keys, and then run the following command:

```sh
pod install
```

After executing the command, open QCloudCOSXMLDemo.xcworkspace to view the Demo.

