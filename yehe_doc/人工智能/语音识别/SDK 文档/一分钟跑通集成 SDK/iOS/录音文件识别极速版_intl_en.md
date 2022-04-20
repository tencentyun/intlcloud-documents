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
#### QCloudFlashFileRecognizer initialization description
**QCloudFlashFileRecognizer** is the entry class for ultrafast recording file recognition.
```objective-c
/**
  Initialization through `appId`, `secretId`, and `secretKey`
  @param appid     Tencent Cloud `appId`
  @param secretId  Tencent Cloud `secretId`
  @param secretKey Tencent Cloud `secretKey`
 **/
- (instancetype)initWithAppId:(NSString *)appid secretId:(NSString *)secretId secretKey:(NSString *)secretKey;

/** 
  Initialization through `appId`, temporary `secretId`, temporary `secretKey`, and `token` 
  For more information, visit https://cloud.tencent.com/document/product/598/33416
  @param appid     Tencent Cloud `appId`
  @param secretId  Tencent Cloud temporary `secretId`
  @param secretKey Tencent Cloud temporary `secretKey`
  @param token Tencent Cloud `token`
 **/
- (instancetype)initWithAppId:(NSString *)appid secretId:(NSString *)secretId secretKey:(NSString *)secretKey token:(NSString *)token;
```

[](id:QCloudFlashFileRecognizerDelegate)
#### QCloudFlashFileRecognizerDelegate protocol description
This delegate is the callback for recording file recognition. You need to implement this delegate to get the recognition result event.
```objective-c
@protocol QCloudFlashFileRecognizerDelegate <NSObject>
@optional

/**
 Callback for recording file recognition success with the result obtained from the server

@param recognizer Recording file recognizer
 @param status If the status is not 0, recognition failed
 @param text Recognized text. When the status is not 0, this is the error message returned by the server
 @param resultData Raw data
 */
- (void)FlashFileRecognizer:(QCloudFlashFileRecognizer *_Nullable)recognizer status:(nullable NSInteger *) status text:(nullable NSString *)text resultData:(nullable NSDictionary *)resultData;

/**
 Callback for recording file recognition failure
 @param recognizer Recording file recognizer
 @param error Recognition error. This field will be present in case of errors
 @param resultData Raw data
 */
- (void)FlashFileRecognizer:(QCloudFlashFileRecognizer *_Nullable)recognizer error:(nullable NSError *)error resultData:(nullable NSDictionary *)resultData;
@end
```

## Sample
1. **Create a `QCloudFlashFileRecognizer` instance.** 
```objective-c
  QCloudFlashFileRecognizer *recognizer = [[QCloudFlashFileRecognizer alloc] initWithAppId:appId 
  								        secretId:secretId secretKey:secretKey];
  // Set the delegate. For more information on the callback method, see the definition of `QCloudFlashFileRecognizerDelegate`
 recognizer.delegate = self;
```
2. **Implement the `[QCloudFlashFileRecognizerDelegate](#QCloudFlashFileRecognizerDelegate)` protocol method.**
3. **Sample call:**
```objective-c
 (void)recognizeWithAudioData {
    QCloudFlashFileRecognizeParams *params = [QCloudFlashFileRecognizeParams defaultRequestParams];
    NSString *filePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"mp3"];
    NSData *audioData = [[NSData alloc] initWithContentsOfFile:filePath];
    params.audioData = audioData;
    // Audio format. Supported formats include WAV, PCM, Ogg-Opus, Speex, SILK, MP3, M4A, and AAC.
    params.voiceFormat = @"mp3";
    
    // If the following parameters are not set, their default values will be used
    params.engineModelType = @"16k_zh";// Engine model type. 8k_zh: 8 kHz Mandarin for general fields; 16k_zh (default): 16 kHz Mandarin for general fields; 16k_zh_video: 16 kHz Mandarin for audiovisual fields
    params.filterDirty = 0;;// 0 (default): does not filter swear words; 1: filters swear words
    params.filterModal = 0;// 0 (default): does not filter interjections; 1: filters some interjections; 2: filters interjections strictly
    params.filterPunc = 0;// 0 (default): does not filter period at the end of sentence; 1: filters period at the end of sentence
    params.convertNumMode = 1;;// 1 (default): intelligently converts numbers into digits; 0: converts numbers to words
    params.speakerDiarization = 0; // Whether to enable speaker separation (currently, this feature is supported only for the Mandarin engine). 0 (default): does not enable; 1: enables
    params.firstChannelOnly = 1; // Whether to recognize only the first channel. 0: recognizes all channels; 1 (default): recognizes the first channel
    params.wordInfo = 0; // Whether to display word-level timestamp. 0 (default): does not display; 1: displays timestamps without punctuation marks; 2: displays timestamps with punctuation marks.
    
    
    [_recognizer recognize:params];
}
```
