## Connection Preparations
### SDK acquisition
The real-time speech recognition SDK and demo for iOS can be downloaded [here](https://sdk-1300466766.cos.ap-shanghai.myqcloud.com/realtime/QCloudSDK_IOS_v2.6.4.zip).

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
The following describes the connection processes and demos for **capturing audio for recognition with the built-in recorder** and **providing audio data** respectively.

#### Demo for capturing audio for recognition with built-in recorder
1. **Import the header file of `QCloudSDK` and change the filename extension from `.m` to `.mm`.**
```objective-c
#import<QCloudSDK/QCloudSDK.h>
```
2. **Create a `QCloudConfig` instance.**
```objective-c
 //1. Create a `QCloudConfig` instance
 QCloudConfig *config = [[QCloudConfig alloc] initWithAppId:kQDAppId 
  						   secretId:kQDSecretId 
					          secretKey:kQDSecretKey 
					          projectId:kQDProjectId];
 config.sliceTime = 600;                        // The length of the audio segment is 600 ms
 config.enableDetectVolume = YES;               // Specify whether to detect the volume
 config.endRecognizeWhenDetectSilence = YES;    // Specify whether to stop recognition when silence is detected
```
3. **Create a `QCloudRealTimeRecognizer` instance.** 
```objective-c
 QCloudRealTimeRecognizer *recognizer = [[QCloudRealTimeRecognizer alloc] initWithConfig:config];
```
4. **Set the delegate and implement the [QCloudRealTimeRecognizerDelegate](#QCloudRealTimeRecognizerDelegate) method.**
```objective-c
recognizer.delegate = self;
```
5. **Start recognition.**
```objective-c
 [recognizer start];
```
6. **End recognition.**
```objective-c
 [recognizer stop];
```

#### Sample for providing audio data
1. **Import the header file of `QCloudSDK` and change the filename extension from `.m` to `.mm`.**
```objective-c
#import<QCloudSDK/QCloudSDK.h>
```
2. **Create a `QCloudConfig` instance.** 
```objective-c
 //1. Create a `QCloudConfig` instance
 QCloudConfig *config = [[QCloudConfig alloc] initWithAppId:kQDAppId 
  						  secretId:kQDSecretId 
					         secretKey:kQDSecretKey 
					         projectId:kQDProjectId];
 config.sliceTime = 600;                        // The length of the audio segment is 600 ms
 config.enableDetectVolume = YES;               // Specify whether to detect the volume
 config.endRecognizeWhenDetectSilence = YES;    // Specify whether to stop recognition when silence is detected
```
3. **Customize `QCloudDemoAudioDataSource` and implement the [QCloudAudioDataSource](#QCloudAudioDataSource) protocol.**
```objective-c
 QCloudDemoAudioDataSource *dataSource = [[QCloudDemoAudioDataSource alloc] init];
```
4. **Create a `QCloudRealTimeRecognizer` instance.**
```objective-c
 QCloudRealTimeRecognizer *recognizer = [[QCloudRealTimeRecognizer alloc] initWithConfig:config dataSource:dataSource];
```
5. **Set the delegate and implement the [QCloudRealTimeRecognizerDelegate](#QCloudRealTimeRecognizerDelegate) method.**
```objective-c
 recognizer.delegate = self;
```
6. **Start recognition.** 
```objective-c
 [recognizer start];
```
7. **End recognition.**
```objective-c
 [recognizer stop];
```

### Descriptions of main API classes
#### QCloudRealTimeRecognizer initialization description
`QCloudRealTimeRecognizer` is the real-time speech recognition class, which provides two initialization methods.
```objective-c
/**
 * Initialization method where the built-in recorder is used to capture audios
 * @param config Configuration parameter. For more information, see the definition of `QCloudConfig`.
 */
- (instancetype)initWithConfig:(QCloudConfig *)config;

/**
 * Initialization method which will be called to pass in audio data
 * @param config Configuration parameter. For more information, see the definition of `QCloudConfig`.
 * @param dataSource Data source of audio data. You must implement the `QCloudAudioDataSource` protocol.
 */
- (instancetype)initWithConfig:(QCloudConfig *)config dataSource:(id<QCloudAudioDataSource>)dataSource;
```

#### QCloudConfig initialization method description
```objective-c
/**
 * Initialization method - direct authentication
 * @param appid     Tencent Cloud `appId` 
 * @param secretId  Tencent Cloud `secretId`
 * @param secretKey Tencent Cloud `secretKey`
 * @param projectId Tencent Cloud `projectId`
 */
- (instancetype)initWithAppId:(NSString *)appid
                     secretId:(NSString *)secretId
                    secretKey:(NSString *)secretKey
                    projectId:(NSString *)projectId;

/**
 * Initialization method - authentication through STS temporary credentials. For more information, visit https://cloud.tencent.com/document/product/598/33416
 * @param appid     Tencent Cloud `appId` 
 * @param secretId  Tencent Cloud temporary `secretId`  
 * @param secretKey Tencent Cloud temporary `secretKey`
 * @param token     Token
 */
- (instancetype)initWithAppId:(NSString *)appid
    				    secretId:(NSString *)secretId
       					secretKey:(NSString *)secretKey
            			token:(NSString *)token;
```

[](id:QCloudRealTimeRecognizerDelegate)
#### QCloudRealTimeRecognizerDelegate method description
```objective-c
/**
 * One real-time speech recognition is divided into multiple flows, each of which can be understood as a sentence, and multiple sentences can be included in one recognition.
  * Each flow contains multiple `seq` audio data packets, and the `seq` of each flow starts from 0.
 */
@protocol QCloudRealTimeRecognizerDelegate <NSObject>

@required
/**
 * Recognition result of each audio package segment
 * @param response Recognition result of the audio segment
 */
- (void)realTimeRecognizerOnSliceRecognize:(QCloudRealTimeRecognizer *)recognizer response:(QCloudRealTimeResponse *)response;

@optional
/**
 * Callback for recognition success
 @param recognizer Real-Time speech recognition instance
 @param result Total text recognized at one time
 */
- (void)realTimeRecognizerDidFinish:(QCloudRealTimeRecognizer *)recognizer result:(NSString *)result;
/**
 * Callback for recognition failure
 * @param recognizer Real-Time speech recognition instance
 * @param error Error message
 * @param voiceId  The `voiceId` attached to the error returned by the backend
 */

- (void)realTimeRecognizerDidError:(QCloudRealTimeRecognizer *)recognizer error:(NSError *)error  voiceId:(NSString * _Nullable) voiceId;

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/**
 * Callback for recording start
 * @param recognizer Real-Time speech recognition instance
 * @param error Error message for recording start failure
 */
- (void)realTimeRecognizerDidStartRecord:(QCloudRealTimeRecognizer *)recognizer error:(NSError *)error;
/**
 * Callback for recording end
 * @param recognizer Real-Time speech recognition instance
 */
- (void)realTimeRecognizerDidStopRecord:(QCloudRealTimeRecognizer *)recognizer;
/**
 * Real-Time callback for recording volume
 * @param recognizer Real-Time speech recognition instance
 * @param volume Audio volume level in the range of -40 to 0
 */
- (void)realTimeRecognizerDidUpdateVolume:(QCloudRealTimeRecognizer *)recognizer volume:(float)volume;


//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/**
 * Audio stream recognition start
 * @param recognizer Real-Time speech recognition instance
 * @param voiceId `voiceId` of the audio stream, which is the unique identifier
 * @param seq Sequence number of the flow
 */
- (void)realTimeRecognizerOnFlowRecognizeStart:(QCloudRealTimeRecognizer *)recognizer voiceId:(NSString *)voiceId seq:(NSInteger)seq;
/**
 * Audio stream recognition end
 * @param recognizer Real-Time speech recognition instance
 * @param voiceId `voiceId` of the audio stream, which is the unique identifier
 * @param seq Sequence number of the flow
 */
- (void)realTimeRecognizerOnFlowRecognizeEnd:(QCloudRealTimeRecognizer *)recognizer voiceId:(NSString *)voiceId seq:(NSInteger)seq;

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/**
 * Audio stream recognition start
 * @param recognizer Real-Time speech recognition instance
 * @param voiceId `voiceId` of the audio stream, which is the unique identifier
 * @param seq Sequence number of the flow
 */
- (void)realTimeRecognizerOnFlowStart:(QCloudRealTimeRecognizer *)recognizer voiceId:(NSString *)voiceId seq:(NSInteger)seq;
/**
 * Audio stream recognition end
 * @param recognizer Real-Time speech recognition instance
 * @param voiceId `voiceId` of the audio stream, which is the unique identifier
 * @param seq Sequence number of the flow
 */
- (void)realTimeRecognizerOnFlowEnd:(QCloudRealTimeRecognizer *)recognizer voiceId:(NSString *)voiceId seq:(NSInteger)seq;

@end
```

[](id:QCloudAudioDataSource)
#### QCloudAudioDataSource protocol description
If you provide audio data instead of capturing audio data with the recorder built in the SDK, you need to implement all methods in this protocol in the same way as used for the implementation of `QDAudioDataSource` in the demo project.
```objective-c
/**
 * Data source of audio data. If you want to provide audio data on your own, you need to implement all methods in this protocol.
 * Provide audio data that meets the following requirements:
 * Sample rate: 16 kHz
 * Audio format: PCM
 * Encoding: 16-bit mono-channel
 */
@protocol QCloudAudioDataSource <NSObject>

@required

/**
 * It identifies whether the data source has started to work and needs to be set to `YES` after `start` is executed and to `NO` after `stop` is executed.
 */
@property (nonatomic, assign) BOOL running;

/**
 * The SDK will call the `start` method. Implementing the class of this protocol requires initializing the data source.
 */
- (void)start:(void(^)(BOOL didStart, NSError *error))completion;
/**
 * The SDK will call the `stop` method. Implementing the class of this protocol requires stopping supplying data.
 */
- (void)stop;
/**
 * The SDK will call this method of the object that implements the protocol to read audio data. If the audio data is less than `expectLength`, `nil` will be returned directly.
 * @param expectLength The number of bytes expected to be read. If the returned `NSData` is less than `expectLength` bytes, the SDK will throw an exception.
 */
- (nullable NSData *)readData:(NSInteger)expectLength;

@end
```

