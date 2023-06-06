### Development Preparations

1. Sign up for a Tencent Cloud account and log in to the eKYC console to activate the service.
2. Download the required version of SDK via the eKYC SDK download link and integrate it locally.
3. Contact the business or customer service to get the license file of your version.



### Integrating the eKYC SDK for iOS

#### Environment requirements

1. Xcode 12.0 or later is required. We recommend you use the latest version.
2. The eKYCID SDK for iOS is only supported by iOS 11.0 or later.

#### Directions

Importing required libraries and files

1. Click `Link Binary With Libraries` to add required frameworks (libraries) that the SDK depends on as below:

```
├──HuiYanEKYCVerification.framework
├──tnn.framework
├──tnnliveness.framework
├──YTCommonLiveness.framework
├──YTeKYCAlignmentTinyLiveness.framework
├──YTeKYCDetectorLiveness.framework
├──YTeKYCLiveReflect.framework
├──YTeKYCTrackerLiveness.framework
├──YTPoseDetector.framework
├──YtSDKKitActionLiveness.framework
├──YtSDKKitFramework.framework
├──YtSDKKitOcrVideoIdent.framework
├──YtSDKKitReflectLiveness.framework
└──YtSDKKitSilentLiveness.framework
├── HKOCRSDK.framework
├── tiny_opencv2.framework
└── YtSDKKitOcrVideoIdent.framework
```

2. Click `Link Binary With Libraries` to add system frameworks.

```
└── Accelerate.framework
└── CoreML.framework
```

3. Click `Copy Bundle Resources` to add bundle files.

```
└── eKYC-tracker-v001.bundle
└── huiyan_verification.bundle
└── ytsdkviidres.bundle
```

4. Set `Build Phases`.

   1. Click `Other Linker Flags` to add **-ObjC**.

   2. Integrate .m files. It is necessary to set the file extension as `.mm`, or change the file type to `Objective-C++ Source`.

      <img src="https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/EKYC/%E5%9B%BE%E5%BA%8A/setOC%2B%2B.png" style="zoom:50%;" />

5. Set permissions

As the SDK requires a camera permission, include the following key-value pair in `info.plist` of the main project to add the corresponding permission declaration.

```XML
<key>Privacy - Camera Usage Description</key>
<string>eKYC SDK needs to access your camera</string>
```



#### SDK APIs Use Instructions

##### Initialization API

This API is called when you initialize your app. It is mainly used for some SDK initialization operations.

```objective-c
#import <HuiYanEKYCVerification/VerificationKit.h>
- (void)viewDidLoad {
    [[VerificationKit sharedInstance] initWithViewController:self];
}
```

##### API for starting the eKYC process

When you need to start the eKYC process, you just need to call the `startVerifiWithConfig` method and set `ekycToken` and some other custom fields.

```objective-c
- (IBAction)startVerificationEvent:(id)sender {
    NSLog(@"startVerificationEvent");
    VerificationConfig *config = [[VerificationConfig alloc] init];
    config.licPath = [[NSBundle mainBundle] pathForResource:@"eKYC_license.lic" ofType:nil];
    config.languageType = (LanguageType)(selectTag + 1);
    config.verAutoTimeOut = 30000;// Set the authentication timeout period
    config.hyeKYCTimeOut = 15000;// Set the timeout period of a single eKYC authentication operation
    config.ekycToken = self.eKYCTokenTextField.text;
    [[VerificationKit sharedInstance] startVerifiWithConfig:config withSuccCallback:^(int errorCode, id  _Nonnull resultInfo, id  _Nullable reserved) {
        NSLog(@"ErrCode:%d msg:%@",errorCode,resultInfo);
        NSString *showMsg = [NSString stringWithFormat:@"ErrCode:%d msg:%@",errorCode,resultInfo];
        [self showAlertViewWithMsg:showMsg];
    } withFialCallback:^(int errorCode, NSString * _Nonnull errorMsg, id  _Nullable reserved) {
        NSLog(@"ErrCode:%d msg:%@ extra:%@",errorCode,errorMsg,reserved);
        NSString *showMsg = [NSString stringWithFormat:@"ErrCode:%d msg:%@ extra:%@",errorCode,errorMsg,reserved];
        [self showAlertViewWithMsg:showMsg];
    }];
}
```

**ekycToken** is the unique credential obtained from the server for this eKYC process.

**Note:** The file **"eKYC_license.lic"** is the license file obtained from the business or customer service, and you need to place the license file into `Copy Bundle Resources`.

<img src="https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/EKYC/%E5%9B%BE%E5%BA%8A/eKYCLicResources.png" style="zoom:50%;" />



##### API for releasing SDK resources

You can call this API after you finish operations and no longer need the SDK.

```objective-c
- (void)dealloc {
    [VerificationKit clearInstance];
}
```



### FAQs

1. For errors similar to the following ones:
   <img src="https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/EKYC/%E5%9B%BE%E5%BA%8A/iOS_OC%2B%2Bset.png" style="zoom:50%;" />

   Change the property of the SDK file to `Objective-C++ Source`.

2. For the absence of image in the SDK intereKYC:

   Select TARGETS -> Build Settings -> Other Linker Flags to configure **-ObjC**. 

3. For following errors:

   <img src="https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/EKYC/%E5%9B%BE%E5%BA%8A/AccelerateLose.png" style="zoom:50%;" />

Select TARGETS -> Build Phases -> Link Binary With Libraries to add the system library **Accelerate.framework**.
