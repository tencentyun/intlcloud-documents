## Connection Preparations
### SDK acquisition
The one-sentence recognition SDK and demo for iOS can be downloaded [here](https://sdk-1300466766.cos.ap-shanghai.myqcloud.com/realtime/QCloudSDK_IOS_v2.6.4.zip).

### Notes on connection
- You need to view the [API description](https://intl.cloud.tencent.com/document/product/1118/43378) of real-time speech recognition to understand the **use requirements** and **directions** of the API before calling it.
- The API requires the phone to have an internet connection over GPRS, 3G, Wi-Fi, etc. and requires the system to be **iOS 9.0** or above.

### Development environment
Add the following settings in the `info.plist` project:
+ **Set the `NSAppTransportSecurity` policy by adding the following content:**
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
+ **Request the system's mic permission and add the following content:**
```objective-c
   <key>NSMicrophoneUsageDescription</key>
   <string>Your mic is required to capture audios</string>
```
+ **Add dependent libraries in the project and add the following libraries in Build Phases' `Link Binary With Libraries`:**
  + AVFoundation.framework
  + AudioToolbox.framework
  + QCloudSDK.framework
  + CoreTelephony.framework
  + libWXVoiceSpeex.a

The libraries are added as shown below:
![](https://main.qcloudimg.com/raw/17ff6f4f4a27e0843de528eb070c2f32.png)

## Quick Connection
### Connection process and demo
1. **Create a `QCloudSentenceRecognizer` instance.** 
```objective-c
  QCloudSentenceRecognizer *recognizer = [[QCloudSentenceRecognizer alloc] initWithAppId:appId 
  									        secretId:secretId 
									       secretKey:secretKey];
  // Set the delegate. For more information on the callback method, see the definition of `QCloudOneSentenceRecognizerDelegate`
 recognizer.delegate = self;
```
2. **Implement the `[QCloudSentenceRecognizerDelegate](#QCloudSentenceRecognizerDelegate)` protocol method.**
3. **Sample call:**
 + **Call through audio URL**
```objective-c
- (void)recognizeWithUrl {
// Audio data URL
NSString *url = @"https://asr-audio-1256237915.cos.ap-shanghai.myqcloud.com/30s.wav";
  // Specify the format and sample rate of the audio data at the URL
  [_recognizer recoginizeWithUrl:url voiceFormat:kQCloudVoiceFormatWAV frequence:kQCloudEngSerViceType16k];
}
```
 + **Call through audio data**
```objective-c
- (void)recognizeWithAudioData {
   // Audio data
   NSString *filePath = [[NSBundle mainBundle] pathForResource:@"recordedFile" ofType:@"wav"];
   NSData *audioData = [[NSData alloc] initWithContentsOfFile:filePath];
   // Specify the format and sample rate of the audio data
   [_recognizer recoginizeWithData:audioData voiceFormat:kQCloudVoiceFormatWAV frequence:kQCloudEngSerViceType16k];
}
```
 + **Call through specified parameters**
```objective-c
- (void)recognizeWithParams {
   NSString *url = @"https://asr-audio-1256237915.cos.ap-shanghai.myqcloud.com/30s.wav";
   // Get the set default parameter `params`
   QCloudOneSentenceRecognitionParams *params = [_recognizer defaultRecognitionParams];    
   // Request through audio URL. These 4 parameters must be set
   params.url = url;                           
   // Set the audio data format. For more information, see the definition of `kQCloudVoiceFormat`
   params.voiceFormat = kQCloudVoiceFormatWAV;
   // Set the audio data source. For more information, see the definition of `QCloudAudioSourceType`
   params.sourceType = QCloudAudioSourceTypeUrl;
   // Set the sample rate. For more information, see the definition of `kQCloudEngSerViceType`
   params.engSerViceType = kQCloudEngSerViceType16k; 
   [_recognizer recognizeWithParams:params];
}
```
 - **Call through the SDK's built-in recorder**
```objective-c
- (void)recognizeWithRecorder {
   [_recognizer startRecognizeWithRecorder];
}
```

### Descriptions of main API classes
#### QCloudSentenceRecognizer initialization description
`QCloudSentenceRecognizer` is the one-sentence recognition entry class, which provides two initialization methods.
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

[](id:QCloudSentenceRecognizerDelegate)
#### QCloudSentenceRecognizerDelegate protocol description
This delegate is the callback for one-sentence recognition. You need to implement this delegate to get the recognition result, recording start event, and recording end event.
```objective-c
@protocol QCloudSentenceRecognizerDelegate <NSObject>
@required
/**
 * Callback delegate for one-sentence recognition
 * @param result Recognition result text. This field has a value only if `error` is `nil`
 * @param error Error message. For more information, see the `error.domain` and `error.userInfo` fields
 * @param rawData Raw data to be recognized
 */
- (void)oneSentenceRecognizerDidRecognize:(QCloudSentenceRecognizer *)recognizer text:(nullable NSString *)text error:(nullable NSError *)error resultData:(nullable NSDictionary *)resultData;
@optional
/**
 * Callback for recording start
 */
- (void)oneSentenceRecognizerDidStartRecord:(QCloudSentenceRecognizer *)recognizer error:(nullable NSError *)error;
/**
 * Callback for recording end. After the SDK calls back through this method, it will report audio data internally for recognition
 */
- (void)oneSentenceRecognizerDidEndRecord:(QCloudSentenceRecognizer *)recognizer;
/**
 * Real-Time callback for recording volume
 * @param recognizer Recognizer instance
 * @param volume Audio volume level in the range of -40 to 0
 */
- (void)oneSentenceRecognizerDidUpdateVolume:(QCloudSentenceRecognizer *)recognizer volume:(float)volume;
@end
```

