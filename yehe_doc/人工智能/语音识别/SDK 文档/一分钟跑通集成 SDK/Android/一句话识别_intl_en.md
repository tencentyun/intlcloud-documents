## Connection Preparations
### SDK acquisition
The one-sentence recognition SDK and demo for Android can be downloaded [here](https://sdk-1300466766.cos.ap-shanghai.myqcloud.com/realtime/QCloudSDK_Android_v2.6.5.zip).

### Notes on connection
- You need to view the [API description](https://intl.cloud.tencent.com/document/product/1118/43378) of one-sentence recognition to understand the use requirements and directions of the API before calling it.  
- The API requires the phone to have an internet connection over GPRS, 3G, Wi-Fi, etc. and requires the system to be **Android 4.0.3** or above.

### Development environment
1. **Add the one-sentence recognition SDK's AAR file.**
   Put **speech_release.aar** in the `libs` directory and add the following code to the app's `build.gradle` file.
```
  implementation(name: 'speech_release', ext: 'aar')
```
2. **Add other dependencies by adding the following code to the app's `build.gradle` file.**
```
 implementation 'com.google.code.gson:gson:2.8.5'
 implementation 'com.squareup.okhttp3:okhttp:4.2.2'
 implementation 'com.squareup.okio:okio:1.11.0'
 implementation 'org.slf4j:slf4j-api:1.7.25'
```
3. **Add the following permissions to `AndroidManifest.xml`:**
```
< uses-permission android:name="android.permission.RECORD_AUDIO"/>
< uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```
4. **Declare the following services in `AndroidManifest.xml`:**
```
<!--<service android:name=".service.MyIntentService"/>-->
<service android:name="com.tencent.cloud.qcloudasrsdk.recorder.service.QCloudAudioMp3RecoderService" />
```

## Quick Connection

### Connection process and demo

1. **Create a `QCloudOneSentenceRecognizer` instance.**
```
QCloudOneSentenceRecognizer recognizer = new QCloudOneSentenceRecognizer(this, appid, secretId, secretKey);
```
2. **Set the callback for recognition result.**
```
recognizer.setCallback(this);
```
3. **Sample call:**
 - **Call through audio URL**
```
String audioUrl = "https://img.soulapp.cn/audio/2019-07-22/9ed1a797-93b5-4268-be6d-5660cc3e894e.mp3";
recognizer.recognize(audioUrl, QCloudAudioFormat.QCloudAudioFormatMp3, QCloudAudioFrequence.QCloudAudioFrequence16k);
```
 - **Call through audio data**
```
AssetManager am = getResources().getAssets();
InputStream is = am.open("onesentence.mp3");
int length = is.available();
byte[] audioData = new byte[length];
is.read(audioData);
recognizer.recognize(audioData, QCloudAudioFormat.QCloudAudioFormatMp3, QCloudAudioFrequence.QCloudAudioFrequence16k);
```
 - **Call through the SDK's built-in recorder**
```
recognizer.recognizeWithRecorder();
```

### Descriptions of key classes
**QCloudOneSentenceRecognizer**: one-sentence recognition entry class
```
/**
 * Initialization method - direct authentication. For more information on how to get the `AppId`, `SecretId`, and `SecretKey`, see the steps in the one-sentence recognition API description
 * @param activity app activity
 * @param appId Tencent Cloud `appid`
 * @param secretId Tencent Cloud `secretId`
 * @param secretKey Tencent Cloud `secretKey`
 */
public QCloudOneSentenceRecognizer(AppCompatActivity activity, String appId, String secretId, String secretKey);


/**
 * Initialization method - authentication through STS temporary credentials. For more information, visit https://cloud.tencent.com/document/product/598/33416
 * @param activity app activity
 * @param appId Tencent Cloud `appid`
 * @param secretId Tencent Cloud temporary `secretId`
 * @param secretKey Tencent Cloud temporary `secretKey`
 * @param token Tencent Cloud `token`
 */
public QCloudOneSentenceRecognizer(Activity activity, String appId, String secretId, String secretKey, String token);

 /**
  * Quick entry for one-sentence recognition through audio URL. An exception will be thrown if local parameter verification fails
  * @param audioUrl Resource URL, such as http://www.qq.music/hello.mp3
  * @param audioFormat Audio data format: QCloudAudioFormat
  * @param frequence Audio data sample rate: QCloudAudioFrequence
  */
 public void recognize(String audioUrl, QCloudAudioFormat audioFormat, QCloudAudioFrequence frequence) throws Exception;
 
/**
  * Quick entry for one-sentence recognition through audio data. An exception will be thrown if local parameter verification fails
  * @param audioData Audio data
  * @param audioFormat Audio data format: QCloudAudioFormat
  * @param frequence Audio data sample rate: QCloudAudioFrequence
  */
 public void recognize(byte[] audioData, QCloudAudioFormat audioFormat, QCloudAudioFrequence frequence) throws Exception;
/**
 * To call one-sentence recognition through `QCloudOneSentenceRecognitionParams`, call the `[QCloudCommonParams defaultRequestParams]` method to get the default parameters.
 * Then, set the parameters as needed.
 * @param params Request parameters
 */
public void recognize(QCloudOneSentenceRecognitionParams params) throws Exception;
/**
 * Enable one-sentence recognition through the SDK's built-in recorder
 */
public void recognizeWithRecorder() throws Exception;
```

**QCloudOneSentenceRecognizerListener**: callbacks for recording start, recording end, and recognition result
```
public interface QCloudOneSentenceRecognizerListener {
 /**
  * Callback for recording start
  */
 public abstract void didStartRecord();
 /**
  * Callback for recording end
  */
 public abstract void didStopRecord();
 /**
  * Callback for recognition result
  */
 public abstract void recognizeResult(QCloudOneSentenceRecognizer recognizer, String result, Exception exception);
}
```

