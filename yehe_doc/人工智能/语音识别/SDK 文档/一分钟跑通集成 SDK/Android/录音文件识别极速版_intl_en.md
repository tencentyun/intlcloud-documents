## Preparations for Development
### SDK download
The recording file recognition SDK and demo for Android can be downloaded [here](https://sdk-1300466766.cos.ap-shanghai.myqcloud.com/realtime/QCloudSDK_Android_v2.6.5.zip).

### Notes on connection
- Before using the ultrafast recording file recognition feature, you need to register an account in the [Tencent Cloud console](https://console.cloud.tencent.com/) and get the `AppID`, `SecretId`, and `SecretKey`.
- Your mobile phone must have an internet connection over GPRS, 3G, Wi-Fi, etc.
- Android 4.0 or above is supported.

### Operating environment configuration
1. Add the recording file recognition SDK's AAR file by putting **speech_release.aar** in the `libs` directory and adding the following code to the app's `build.gradle` file.
```
  implementation(name: 'speech_release', ext: 'aar')
```
2. Add other dependencies to the app's `build.gradle` file.
```
 implementation 'com.google.code.gson:gson:2.8.5'
 implementation 'com.squareup.okhttp3:okhttp:4.2.2'
 implementation 'com.squareup.okio:okio:1.11.0'
 implementation 'org.slf4j:slf4j-api:1.7.25'
```
3. Add the following permission to `AndroidManifest.xml`:
```
< uses-permission android:name="android.permission.INTERNET"/>
```

## Quick Connection
### Connection process and demo
1. Create a `QCloudFileRecognizer` instance.
```
QCloudFlashRecognizer fileFlashRecognizer = new QCloudFlashRecognizer(this, appid, secretId, secretKey);

/**
A temporary key can also be used for authentication.
1. Get temporary credentials (`secretId`, `secretKey`, and `token`) through STS. This step should be implemented on your server as instructed at https://cloud.tencent.com/document/product/598/33416
2. Call the API through temporary credentials
**/
QCloudFlashRecognizer fileFlashRecognizer = new QCloudFlashRecognizer(DemoConfig.apppId, "temporary secretId", "temporary secretKey","corresponding token");
```
2. Set the callback for recognition result.
```
fileFlashRecognizer.setCallback(this);
```
3. Sample calls:
```
  InputStream is = null;
  AssetManager am = getResources().getAssets();
  is = am.open("test1.mp3");
  int length = is.available();
  byte[] audioData = new byte[length];
  is.read(audioData);

  QCloudFlashRecognitionParams params = (QCloudFlashRecognitionParams)      	 	
  QCloudFlashRecognitionParams.defaultRequestParams();
   // You can pass in audio file data or audio file path. If both `setData` and `setPath` are called, the value of `setPath` will be ignored by the SDK
    params.setData(audioData);
//  params.setPath("/sdcard/test2.mp3"); // An audio file of less than 100 MB in size can be recognized
    params.setVoiceFormat("mp3"); // Audio format. Supported formats include WAV, PCM, Ogg-Opus, Speex, SILK, MP3, M4A, and AAC.

/**If the following parameters are not set, their default values will be used**/
    params.setEngineModelType("16k_zh");// Engine model type. 8k_zh: 8 kHz Mandarin for general fields; 16k_zh (default): 16 kHz Mandarin for general fields; 16k_zh_video: 16 kHz Mandarin for audiovisual fields
    params.setFilterDirty(0);// 0 (default): does not filter swear words; 1: filters swear words
    params.setFilterModal(0);// 0 (default): does not filter interjections; 1: filters some interjections; 2: filters interjections strictly
    params.setFilterPunc(0);// 0 (default): does not filter period at the end of sentence; 1: filters period at the end of sentence
    params.setConvertNumMode(1);// 1 (default): intelligently converts numbers into digits; 0: converts numbers to words
    params.setSpeakerDiarization(0); // Whether to enable speaker separation (currently, this feature is supported only for the Mandarin engine). 0 (default): does not enable; 1: enables
    params.setFirstChannelOnly(1); // Whether to recognize only the first channel. 0: recognizes all channels; 1 (default): recognizes the first channel
    params.setWordInfo(0); // Whether to display word-level timestamp. 0 (default): does not display; 1: displays timestamps without punctuation marks; 2: displays timestamps with punctuation marks.

    fileFlashRecognizer.recognize(params);
```

### Descriptions of key classes
**QCloudFlashRecognizer**: recording file recognition entry class
```
/**
 * Initialization method
 * @param activity app activity
 * @param appId Tencent Cloud `appid`
 * @param secretId Tencent Cloud `secretId`
 * @param secretKey Tencent Cloud `secretKey`
 */
public QCloudFlashRecognizer(String appId, String secretId, String secretKey);

 * Call recording file recognition through URL or audio data
 * @param params Request parameters
 * @return Returns the unique ID (requestId) of this request
 */
public long recognize(QCloudFlashRecognitionParams params) throws Exception;
```
**QCloudFlasheRecognizerListener**: callback for recognition result
```
public interface QCloudFileRecognizerListener {
    /**
     * Callback for recognition result
     * @param recognizer Recording file recognition instance
     * @param result Recognition result returned by the server. API document: https://cloud.tencent.com/document/product/1093/52097
     * @param exception Exception information
     *
     */
    void recognizeResult(QCloudFlashFileRecognizer recognizer,String result, int status,Exception exception);
}
```

