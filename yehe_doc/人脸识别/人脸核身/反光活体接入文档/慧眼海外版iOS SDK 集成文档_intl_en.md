### I. Preparations for Development

1. Sign up for a Tencent Cloud account and log in to the eKYC console to activate the service.
2. Download the eKYC SDK at the SDK download address and integrate it locally.
3. Apply for the license file.



### II. eKYC SDK for iOS Integration Process

#### 1. Dependent environment

1. Development environment: Xcode 11.0 or above.

2. The eKYC SDK for iOS is applicable to iOS 9.0 and above.

   

#### 2. Manual integration

1. Import relevant libraries and files.

Import relevant frameworks in `Link Binary With Libraries`.

2. The SDK depends on the following libraries:

```
├──HuiYanSDK.framework
├──TXYComm.framework
├──YtSDKKitSilentLiveness.framework
├──YtSDKKitReflectLiveness.framework
├──YtSDKKitActionLiveness.framework
├──YtSDKKitFramework.framework
├──tnnliveness.framework
├──YTFaceAlignmentTinyLiveness.framework
├──YTFaceTrackerLiveness.framework
├──YTFaceDetectorLiveness.framework
├──YTPoseDetector.framework
├──YTCommonLiveness.framework
└──YTFaceLiveReflect.framework
```

3. Import system frameworks in `Link Binary With Libraries`.

```
├── AVFoundation.framework
└── Accelerate.framework
```

4. Import the model in `Copy Bundle Resources`.

```
└── face-tracker-v001.bundle
```

5. Import the resource file in `Copy Bundle Resources`.

```
└── HuiYanSDKUI.bundle
```



#### 3. Integration by using pod

1. Copy the `CloudHuiYanSDK_FW` folder to a directory at the same level as that of the project's `Podfile`.

   

2. Set the following in `Podfile`:

```ruby
target 'HuiYanAuthDemo' do
  use_frameworks! 
  pod 'CloudHuiYanSDK_FW', :path => './CloudHuiYanSDK_FW'
end
```

3. Update by running `pod install`.

>Note: the relative paths of `vendored_frameworks` and `resource` in `CloudHuiYanSDK_FW.podspec` can be changed according to the actual path of the SDK directory.



#### 3. `Build Phases` configuration

1. Add **-ObjC** in `Other Linker Flags`.
2. Change the extension of `ViewController.m` to `.mm`.



#### 4. Permission configuration

As the SDK requires a mobile network and camera permission, add the corresponding permission declarations and add the following `key-value` to the project's `info.plist` configuration.

```xml
<key>Privacy - Camera Usage Description</key>
<string>eKYC requires to use your camera for face recognition</string>
```



#### 5. Overall flowchart

The following diagram shows the overall logic of interaction between the SDK, client, and server.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%B5%B7%E5%A4%96%E7%89%88%E4%BA%A4%E4%BA%92%E5%9B%BEv2.png)





#### 6. SDK API use instructions

##### 6.1 Initializing configuration and pulling configuration parameters

Before using the eKYC SDK, you need to call this method to pass in basic configuration parameters and pull the local configuration parameters through the callback to get the light sequence as detailed below:

1. Configure the SDK configuration information **HuiYanOsConfig** (set the path of the `lic` file, local detection timeout period, whether to clear the local video cache, etc.).

2. Call **startGetAuthConfigData:** to get the local configuration parameter **result**.

3. Call the TencentCloud API **GenerateReflectSequence** to get the light sequence by using the local parameter obtained in the previous step.

```objective-c
// `HuiYanOs` parameters
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
// Path of the license file in the bundle
config.authLicense = [[NSBundle mainBundle] pathForResource:@"YTFaceSDK.license" ofType:@""];
// Local liveness detection timeout period in ms
config.authTimeOutMs = 20000;
// Pull the local configuration parameter information before starting identity verification
[HuiYanOsApi startGetAuthConfigData:config withSuccCallback:^(NSString * _Nonnull result) {
  	// The configuration information is obtained successfully and sent to the server to get the verification start configuration and the light sequence delivered by the server (implemented on your own)
  	NSString *reflectSequence = [self getLiveDataWith:result];
} withFailCallback:^(int errCode, NSString * _Nonnull errMsg) {
  	// Failed to get configuration parameters (implemented on your own)
    NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```



##### 6.2 Performing remaining liveness detection steps

​	After you obtain the configuration information from the server, you need to call this API to pass in the **reflectSequence** delivered by the server, i.e., the light sequence for identity verification, so as to complete the local identity verification process as detailed below:

1. Call **startAuthByLightData:** to pass in **reflectSequence** and enter the SDK liveness detection page.

2. After liveness detection is completed, the result **data** will be returned in **SuccCallback**.

3. Finally, call the **DetectReflectLivenessAndCompare** API to compare the identity verification **data** and get the final comparison result.

```objective-c
[HuiYanOsApi startAuthByLightData:reflectSequence withSuccCallback:^(NSData * _Nonnull data, NSString * _Nonnull videoPath) {
     	// Data of successful liveness detection result
  		// 1. Send the local verification data to the server for comparison and verification to get the final result (implemented on your own)
		 	[self checkAuthResultByData:data];
			// 2. Process the local identity verification video `videoPath` (implemented on your own)
			[self dealWithAuthVideo:videoPath];
} withFailCallback:^(int errCode, NSString * _Nonnull errMsg) {
  		// Get the local identity verification failure when an error occurs
      NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```

>**Note**: if an exception occurs with `getLightData`, you need to exit the SDK by calling the `[HuiYanOsApi startAuthByLightData:nil withSuccCallback:nil withFailCallback:nil]` method to end the current SDK session, and the error will be returned in `FailCallback` of `startGetAuthConfigData`.



##### 6.3 Releasing SDK resources

	Before your app exits, you can call the SDK resource release API.

```objective-c
// Release the resources upon exit
- (void)dealloc {
    [HuiYanOsApi release];
}
```



### III. Common Errors

1. **errCode:210, errMsg:HuiYanOsConfig param error**: check whether the license file path is configured correctly and added to **Copy Bundle Resource**.

2. **[HuiYanOsApi startAuthByLightData:@"" withSuccCallback:nil withFailCallback:nil];**: **errCode:215, errMsg:User voluntarily Stop** is returned, which actively stops the SDK's identity verification process.

3. **errCode:210, errMsg:lightData is err**: the format of `lightData` is incorrect.
4. Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '\**\* -[__NSDictionaryM setObject:forKey:]: key cannot be nil': add **`-ObjC` in `Other Linker Flags`**.

