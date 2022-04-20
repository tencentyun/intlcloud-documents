## Preparations for Development
### SDK download
The recording file recognition SDK and demo for Android can be downloaded [here](https://sdk-1300466766.cos.ap-shanghai.myqcloud.com/realtime/QCloudSDK_Android_v2.6.5.zip).

### Notes on connection
- Before using the recording file recognition feature, you need to register an account in the [Tencent Cloud console](https://console.cloud.tencent.com/) and get the `APPID`, `SecretId`, and `SecretKey`.
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
QCloudFileRecognizer recognizer = new QCloudFileRecognizer(this, appid, secretId, secretKey);
```
2. Set the callback for recognition result.
```
recognizer.setCallback(this);
```
3. Sample calls:
 - Call through audio URL
```  
     QCloudFileRecognitionParams params = (QCloudFileRecognitionParams) QCloudFileRecognitionParams.defaultRequestParams();
                    params.setUrl("http://client-sdk-1255628450.cossh.myqcloud.com/test%20audio/voice_WGVNG_800.mp3");
                    params.setSourceType(QCloudSourceType.QCloudSourceTypeUrl);
                    params.setFilterDirty(0);// 0 (default): does not filter swear words; 1: filters swear words
                    params.setFilterModal(0);// 0 (default): does not filter interjections; 1: filters some interjections; 2: filters interjections strictly
                    params.setConvertNumMode(1);// 1 (default): intelligently converts numbers into digits; 0: converts numbers to words
                    params.setHotwordId("");  // Keyword ID, which is used to call the corresponding keyword list. If you set a keyword ID when calling the ASR service, the set keyword will take effect; otherwise, the default keyword will take effect.
                    fileRecognizer.recognize(params);
```
 - Call through audio data
```
  AssetManager am = getResources().getAssets();
  is = am.open("test1.mp3");
  int length = is.available();
  byte[] audioData = new byte[length];
  is.read(audioData);

    QCloudFileRecognitionParams params = (QCloudFileRecognitionParams) QCloudFileRecognitionParams.defaultRequestParams();
                    params.setData(audioData);
                    params.setSourceType(QCloudSourceType.QCloudSourceTypeData);
                    params.setFilterDirty(0);// 0 (default): does not filter swear words; 1: filters swear words
                    params.setFilterModal(0);// 0 (default): does not filter interjections; 1: filters some interjections; 2: filters interjections strictly
                    params.setConvertNumMode(1);// 1 (default): intelligently converts numbers into digits; 0: converts numbers to words
                    params.setHotwordId(""); // Keyword ID, which is used to call the corresponding keyword list. If you set a keyword ID when calling the ASR service, the set keyword will take effect; otherwise, the default keyword will take effect.
                    fileRecognizer.recognize(params);
```

### Descriptions of key classes
**QCloudFileRecognizer**: recording file recognition entry class
```
/**
 * Initialization method - direct authentication
 * @param appId Tencent Cloud `appid`
 * @param secretId Tencent Cloud `secretId`
 * @param secretKey Tencent Cloud `secretKey`
 */
public QCloudFileRecognizer( String appId, String secretId, String secretKey);

/**
 * Initialization method - authentication through STS temporary credentials
 * 1. Get temporary credentials through STS. This step should be implemented on your server.
 * For more information, visit https://cloud.tencent.com/document/product/598/33416
 * 2. Call the API through temporary credentials
 * @param appId Tencent Cloud `appid`
 * @param secretId Tencent Cloud temporary `secretId`
 * @param secretKey Tencent Cloud temporary `secretKey`
 * @param secretKey Tencent Cloud `token`
 */
public QCloudFileRecognizer(String appId, String secretId, String secretKey, String token);

/**
 * Call recording file recognition through URL or audio data
 * @param params Request parameters
 * @return Returns the unique ID (requestId) of this request
 */
public long recognize(QCloudFileRecognitionParams params) throws Exception;
```

**QCloudFileRecognizerListener**: callback for recognition result
```
public interface QCloudFileRecognizerListener {
    /**
     * Callback for recognition result
     * @param recognizer Recording file recognition instance
     * @param requestId Unique request ID
     * @param result Recognized text
     * @param status Task status code. 0: waiting; 1: executing; 2: succeeded; 3: failed 
     * @param exception Exception information
     *
     */
    void recognizeResult(QCloudFileRecognizer recognizer, final long requestId, String result, int status,Exception exception);
}
```
