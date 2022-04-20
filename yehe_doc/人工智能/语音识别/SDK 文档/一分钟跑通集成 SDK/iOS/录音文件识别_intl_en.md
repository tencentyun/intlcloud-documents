## Preparations for Development  

### SDK acquisition

The recording file recognition SDK and demo for iOS (QCloudSDK) can be downloaded [here](https://sdk-1300466766.cos.ap-shanghai.myqcloud.com/realtime/QCloudSDK_IOS_v2.6.4.zip).

### Notes

- QCloudSDK supports **iOS 9.0** and above.
- Recording file recognition requires the phone to have an internet connection over GPRS, 3G, Wi-Fi, etc.
- `AppID`, `SecretID`, `SecretKey`, and `ProjectId` must be set to run the demo, which can be obtained in [API Key Management](https://console.cloud.tencent.com/cam/capi).

### SDK import

Download and decompress the compressed SDK for iOS package, which contains the sample code and QCloudSDK.

### Project configuration

Add the following settings in the `info.plist` project:

1. **Set the `NSAppTransportSecurity` policy by adding the following content:**

```objective-c
  <key>NSAppTransportSecurity</key>
  <dict>
	<key>NSExceptionDomains</key>
	<dict>
		<key>qcloud.com</key>
		<dict>
			<key>NSExceptionAllowsInsecureHTTPLoads</key>
			<true/>
			<key>NSExceptionMinimumTLSVersion</key>
			<string>TLSv1.2</string>
			<key>NSIncludesSubdomains</key>
			<true/>
			<key>NSRequiresCertificateTransparency</key>
			<false/>
		</dict>
	</dict>
    </dict>
```

2. **Request the system's mic permission and add the following content:**

```objective-c
   <key>NSMicrophoneUsageDescription</key>
   <string>Your mic is required to capture audios</string>
```

3. **Add dependent libraries in the project and add the following libraries in Build Phases' `Link Binary With Libraries`:**
   + AVFoundation.framework
   + AudioToolbox.framework
   + QCloudSDK.framework
   + CoreTelephony.framework
   + libWXVoiceSpeex.a

See the figure below:
![](https://main.qcloudimg.com/raw/17ff6f4f4a27e0843de528eb070c2f32.png)

### Class description

#### QCloudFileRecognizer initialization description

**QCloudFileRecognizer** is the recording file recognition entry class, which provides two initialization methods.

```objective-c
/**
 * Initialization method where the built-in recorder is used to capture audios
 * @param config Configuration parameter. For more information, see the definition of `QCloudConfig`.
 */
- (instancetype)initWithConfig:(QCloudConfig *)config;

/**
 * Direct authentication
 * Initialization through `appId`, `secretId`, and `secretKey`
 * @param appid     Tencent Cloud `appId`
 * @param secretId  Tencent Cloud `secretId`
 * @param secretKey Tencent Cloud `secretKey`
 */
- (instancetype)initWithAppId:(NSString *)appid secretId:(NSString *)secretId secretKey:(NSString *)secretKey;

/**
 * Authentication through STS temporary key. For more information, visit https://cloud.tencent.com/document/product/598/33416
 * @param appid     Tencent Cloud `appId` 
 * @param secretId  Tencent Cloud temporary `secretId`  
 * @param secretKey Tencent Cloud temporary `secretKey`
 * @param token     Token
 */
- (instancetype)initWithAppId:(NSString *)appid secretId:(NSString *)secretId secretKey:(NSString *)secretKey token:(NSString *)token;
```

[](id:QCloudFileRecognizerDelegate)

#### QCloudFileRecognizerDelegate protocol description

This delegate is the callback for recording file recognition. You need to implement this delegate to get the recognition result, recording start event, and recording end event.

```objective-c
@protocol QCloudFileRecognizerDelegate <NSObject>
@optional

/**
 Callback for recording file recognition success

 @param recognizer Recording file recognizer
 @param requestId Unique request ID `requestId` returned by the `recognize:` API
 @param text Recognized text
 @param resultData Raw data
 */
- (void)fileRecognizer:(QCloudFileRecognizer *_Nullable)recognizer requestId:(NSInteger)requestId text:(nullable NSString *)text resultData:(nullable NSDictionary *)resultData;
/**
 Callback for recording file recognition failure
 
 @param recognizer Recording file recognizer
 @param requestId Unique request ID `requestId` returned by the `recognize:` API
 @param error Recognition error. This field will be present in case of errors
 @param resultData Raw data
 */
- (void)fileRecognizer:(QCloudFileRecognizer *_Nullable)recognizer requestId:(NSInteger)requestId error:(nullable NSError *)error resultData:(nullable NSDictionary *)resultData;
@end
```

## Sample

### 1. Create a `QCloudFileRecognizer` instance 

```objective-c
  QCloudFileRecognizer *recognizer = [[QCloudFileRecognizer alloc] initWithAppId:appId 
  								        secretId:secretId 
								       secretKey:secretKey];
  // Set the delegate. For more information on the callback method, see the definition of `QCloudFileRecognizerDelegate`
 recognizer.delegate = self;
```

### 2. Implement the [QCloudFileRecognizerDelegate](#QCloudFileRecognizerDelegate) protocol method

### 3. Sample calls

+ #### Call through audio URL

```objective-c
 (void)recognizeWithUrl {
    QCloudFileRecognizeParams *params = [QCloudFileRecognizeParams defaultRequestParams];
    params.audioUrl = @"https://asr-audio-1256237915.cos.ap-shanghai.myqcloud.com/30s.wav";
    [_recognizer recognize:params];
}
```

+ #### Call through audio data

```objective-c
 (void)recognizeWithAudioData {
    QCloudFileRecognizeParams *params = [QCloudFileRecognizeParams defaultRequestParams];
    NSString *filePath = [[NSBundle mainBundle] pathForResource:@"recordedFile" ofType:@"wav"];
    NSData *audioData = [[NSData alloc] initWithContentsOfFile:filePath];
    params.audioData = audioData;
    params.sourceType = QCloudAudioSourceTypeAudioData;
    [_recognizer recognize:params];
}
```
