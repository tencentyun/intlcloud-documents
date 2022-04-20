## Connection Preparations
### SDK acquisition
The real-time speech recognition SDK and demo for Android can be downloaded [here](https://sdk-1300466766.cos.ap-shanghai.myqcloud.com/realtime/QCloudSDK_Android_v2.6.5.zip).

### Notes on connection
- You need to view the [API description](https://intl.cloud.tencent.com/document/product/1118/43378) of real-time speech recognition to understand the **use requirements** and **directions** of the API before calling it.
- The API requires the phone to have an internet connection over GPRS, 3G, Wi-Fi, etc. and requires the system to be **Android 4.0** or above.

### Development environment
- Import the AAR package
  speech_release.aar: ASR SDK.
```
implementation(name: 'speech_release', ext: 'aar')
```
- Add dependencies
  Add the OkHttp3, Okio, GSON, and SLF4J dependencies in the `build.gradle` file:
```
	implementation 'com.squareup.okhttp3:okhttp:4.2.2' 
	implementation 'com.squareup.okio:okio:1.11.0'
	implementation 'com.google.code.gson:gson:2.8.5'
	implementation 'org.slf4j:slf4j-api:1.7.25'
```
- Add the following permissions in `AndroidManifest.xml`:
```
	< uses-permission android:name="android.permission.RECORD_AUDIO"/>
	< uses-permission android:name="android.permission.INTERNET"/>
	< uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

## Quick Connection
[](id:documen)
### Starting real-time speech recognition
```
int appid = XXX;
int projectid = XXX;
String secretId = "XXX";

// The SDK provides a local signature for testing purposes. However, for the security of `secretKey`, we recommend you generate a signature on your own server in the production environment.
AbsCredentialProvider credentialProvider = new LocalCredentialProvider("your secretKey");

final AAIClient aaiClient;
try {
    // 1. Initialize the AAIClient object.
    aaiClient = new AAIClient(this, appid, projectid, secretId, credentialProvider);

/**You can also use temporary credentials for authentication
* * 1. Get temporary credentials through STS. This step should be implemented on your server as instructed at https://cloud.tencent.com/document/product/598/33416
*   2. Call the API through temporary credentials
* **/
  // aaiClient = new AAIClient(MainActivity.this, appid, projectId,"temporary secretId", "temporary secretKey","corresponding token" ,credentialProvider);


    // 2. Initialize the speech recognition request.
    final AudioRecognizeRequest audioRecognizeRequest = new AudioRecognizeRequest.Builder()
            .pcmAudioDataSource(new AudioRecordDataSource()) // Set the audio source to mic input
            .build();

    // 3. Initialize the speech recognition result listener.
    final AudioRecognizeResultListener audioRecognizeResultListener = new AudioRecognizeResultListener() {
        @Override
        public void onSliceSuccess(AudioRecognizeRequest audioRecognizeRequest, AudioRecognizeResult audioRecognizeResult, int i) {
			// Return the recognition result of the audio segment
        }

        @Override
        public void onSegmentSuccess(AudioRecognizeRequest audioRecognizeRequest, AudioRecognizeResult audioRecognizeResult, int i) {
			// Return the recognition result of the audio stream
        }

        @Override
        public void onSuccess(AudioRecognizeRequest audioRecognizeRequest, String s) {
			// Return all recognition results
        }

        @Override
        public void onFailure(AudioRecognizeRequest audioRecognizeRequest, ClientException e, ServerException e1) {
			// Recognition failed
        }
    };

    // 4. Start speech recognition.
    new Thread(new Runnable() {
        @Override
        public void run() {
            if (aaiClient!=null) {
                aaiClient.startAudioRecognize(audioRecognizeRequest, audioRecognizeResultListener);
            }
        }
    }).start();

} catch (ClientException e) {
    e.printStackTrace();
}
```

### Stopping real-time speech recognition

```
// 1. Get the request ID
final int requestId = audioRecognizeRequest.getRequestId();
// 2. Call the `stop` method
new Thread(new Runnable() {
    @Override
    public void run() {
        if (aaiClient!=null){
	    // Stop speech recognition and wait for the current task to end
            aaiClient.stopAudioRecognize(requestId);
        }
    }
}).start();
```

### Canceling real-time speech recognition

```
// 1. Get the request ID
final int requestId = audioRecognizeRequest.getRequestId();
// 2. Call the `cancel` method
new Thread(new Runnable() {
    @Override
    public void run() {
        if (aaiClient!=null){
	    // Cancel speech recognition to discard the current task
            aaiClient.cancelAudioRecognize(requestId);
        }
    }
}).start();
```

## Descriptions of Main API Classes and Methods
### Calculating signature
You need to implement the `AbsCredentialProvider` API on your own to calculate the signature. This method is called inside the SDK, and the upper layer doesn't need to care about the `source`.

**The signature calculation function is as follows:**
```
/**
* Signature function: encrypts the original string with the encryption algorithm as described below.
* @param source Original string
* @return Ciphertext returned after encryption
*/
String getAudioRecognizeSign(String source);
```

**Signature algorithm**   
`SecretKey` is used to encrypt the `source` with HMAC-SHA1 first, and then the ciphertext is Base64-encoded to get the final signature string, i.e., `sign=Base64Encode(HmacSha1(source,secretKey))`.

The SDK provides an implementation class **LocalCredentialProvider** for testing purposes, but we recommend you use it only in the test environment to guarantee the security of `secretKey` and implement the method in the **AbsCredentialProvider** API in the upper layer in the production environment.

### Initializing AAIClient
`AAIClient` is a core class of ASR, which you can call to start, stop, and cancel speech recognition.
```
public AAIClient(Context context, int appid, int projectId, String secreteId, AbsCredentialProvider credentialProvider) throws ClientException
```

| Parameter           | Type                  | Required | Description           |
| ------------------ | --------------------- | -------- | ------------------ |
| context            | Context               | Yes       | Context             |
| appid              | Int                   | Yes       | `AppID` registered with Tencent Cloud |
| projectId          | Int                   | No       | Your `projectId`   |
| secreteId          | String                | Yes       | Your `SecreteId`   |
| credentialProvider | AbsCredentialProvider | Yes       | Authentication class             |

**Sample:**
```
try {
    AaiClient aaiClient = new AAIClient(context, appid, projectId, secretId, credentialProvider);
} catch (ClientException e) {
    e.printStackTrace();
}
```
If `AAIClient` is no longer needed, you need to call the `release()` method to release resources:
```
aaiClient.release();
```

### Configuring global parameters
You need to call the static methods of the `ClientConfiguration` class to modify the global configuration.

| Method                                 | Description               | Default Value | Valid Range      |
| ------------------------------------ | ---------------------- | ------ | ------------- |
| setMaxAudioRecognizeConcurrentNumber | Maximum number of concurrent speech recognition requests | 2      | 1–5         |
| setMaxRecognizeSliceConcurrentNumber | Maximum number of concurrent segments for speech recognition | 5      | 1–5         |
| setAudioRecognizeSliceTimeout        | HTTP read timeout period        | 5000 ms | 500–10000 ms |
| setAudioRecognizeConnectTimeout      | HTTP connection timeout period      | 5000 ms | 500–10000 ms |
| setAudioRecognizeWriteTimeout        | HTTP write timeout period        | 5000 ms | 500–10000 ms |

**Sample:**
```
ClientConfiguration.setMaxAudioRecognizeConcurrentNumber(2)
ClientConfiguration.setMaxRecognizeSliceConcurrentNumber(5)
ClientConfiguration.setAudioRecognizeSliceTimeout(2000)
ClientConfiguration.setAudioRecognizeConnectTimeout(2000)
ClientConfiguration.setAudioRecognizeWriteTimeout(2000)
```

### Setting result listener
`AudioRecognizeResultListener` can be used to listen on speech recognition results. It has the following four APIs:
- Speech recognition result callback API for audio segment
```
void onSliceSuccess(AudioRecognizeRequest request, AudioRecognizeResult result, int order);
```
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>request</td>
<td>AudioRecognizeRequest</td>
<td>Speech recognition request</td>
</tr>
<tr>
<td>result</td>
<td>AudioRecognizeResult</td>
<td>Speech recognition result of the audio segment</td>
</tr>
<tr>
<td>order</td>
<td>Int</td>
<td>Sequence of the audio stream of the audio segment</td>
</tr>
</tbody></table>
- Speech recognition result callback API for audio stream
```
void onSegmentSuccess(AudioRecognizeRequest request, AudioRecognizeResult result, int order);
```
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>request</td>
<td>AudioRecognizeRequest</td>
<td>Speech recognition request</td>
</tr>
<tr>
<td>result</td>
<td>AudioRecognizeResult</td>
<td>Speech recognition result of the audio segment</td>
</tr>
<tr>
<td>order</td>
<td>Int</td>
<td>Sequence of the audio stream</td>
</tr>
</tbody></table>
- Return of all recognition results
```
void onSuccess(AudioRecognizeRequest request, String result);
```
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>request</td>
<td>AudioRecognizeRequest</td>
<td>Speech recognition request</td>
</tr>
<tr>
<td>result</td>
<td>String</td>
<td>All recognition results</td>
</tr>
</tbody></table>
- Callback function for speech recognition request failure
```
void onFailure(AudioRecognizeRequest request, final ClientException clientException, final ServerException serverException,String response);
```
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>request</td>
<td>AudioRecognizeRequest</td>
<td>Speech recognition request</td>
</tr>
<tr>
<td>clientException</td>
<td>ClientException</td>
<td>Client exception</td>
</tr>
<tr>
<td>serverException</td>
<td>ServerException</td>
<td>Server exception</td>
</tr>
<tr>
<td>response</td>
<td>String</td>
<td>	JSON string returned by the server</td>
</tr>
</tbody></table>

For the sample code, see [Demo](#documen).

### Setting speech recognition parameters
By constructing the `AudioRecognizeConfiguration` class, you can set the speech recognition configuration:

| Parameter                | Type    | Required | Description                                           | Default Value |
| ----------------------- | ------- | -------- | -------------------------------------------------- | ------ |
| setSilentDetectTimeOut  | Boolean | No       | Specifies whether to enable silence detection. After it is enabled, the silence part before the actual speech starts will not be recognized | true   |
| audioFlowSilenceTimeOut | Int     | No       | Specifies whether to enable speech start detection timeout. After it is enabled, recording will automatically stop after the timeout period elapses     | 5000 ms |
| minAudioFlowSilenceTime | Int     | No       | Minimum period for segmenting two audio streams                             | 2000 ms |
| minVolumeCallbackTime   | Int     | No       | Volume callback time                                       | 80 ms   |

**Sample:**
```
AudioRecognizeConfiguration audioRecognizeConfiguration = new AudioRecognizeConfiguration.Builder()
	.setSilentDetectTimeOut(true)// Specifies whether to enable silence detection. `false` indicates not to check the silence part
        .audioFlowSilenceTimeOut(5000) // Stop recording after the silence detection timeout period elapses
        .minAudioFlowSilenceTime(2000) // Interval for audio stream segmentation
    	.minVolumeCallbackTime(80) // Volume callback time
    	.build();

// Start speech recognition
new Thread(new Runnable() {
    @Override
    public void run() {
        if (aaiClient!=null) {
            aaiClient.startAudioRecognize(audioRecognizeRequest, audioRecognizeResultListener, audioRecognizeConfiguration);
        }
    }
}).start();
```

### Setting status listener
`AudioRecognizeStateListener` can be used to listen on speech recognition status. It has the following APIs:

| Method                       | Description                                                     |
| -------------------------- | ------------------------------------------------------------ |
| onStartRecord              | Start of recording  |
| onStopRecord               | Stop of recording |
| onVoiceFlowStart           | Start of audio stream                                           |
| onVoiceFlowStartRecognize  | Start of audio stream recognition                                               |
| onVoiceFlowFinishRecognize | End of audio stream recognition                                               |
| onVoiceVolume              | Volume                                                         |
| onNextAudioData            | Returns the audio stream to the host layer for recording caching. It will take effect when `true` is passed in for `new AudioRecordDataSource(true)`  |

### Setting timeout listener
`AudioRecognizeTimeoutListener` can be used to listen on speech recognition timeout. It has the following two APIs:

| Method                       | Description                                                     |
| ----------------------- | -------------------- |
| onFirstVoiceFlowTimeout | Detects the timeout of the first audio stream |
| onNextVoiceFlowTimeout  | Detects the timeout of the next audio stream |

**Sample:**
```
AudioRecognizeStateListener audioRecognizeStateListener = new AudioRecognizeStateListener() {
  @Override
  public void onStartRecord(AudioRecognizeRequest audioRecognizeRequest) {
      // Start recording
  }
    @Override
  public void onStopRecord(AudioRecognizeRequest audioRecognizeRequest) {
// End recording
  }
    @Override
  public void onVoiceFlowStart(AudioRecognizeRequest audioRecognizeRequest, int i) {
// Start the audio stream
  }
    @Override
  public void onVoiceFlowFinish(AudioRecognizeRequest audioRecognizeRequest, int i) {
// End the audio stream
  }
    @Override
  public void onVoiceFlowStartRecognize(AudioRecognizeRequest audioRecognizeRequest, int i) {
// Start recognizing the audio stream
  }
    @Override
  public void onVoiceFlowFinishRecognize(AudioRecognizeRequest audioRecognizeRequest, int i) {
// End recognizing the audio stream
  }
    @Override
  public void onVoiceVolume(AudioRecognizeRequest audioRecognizeRequest, int i) {
// Call back the volume
  }
};
/**
    * Return the audio stream
    * to the host layer for recording caching.
    * As the method runs on the SDK thread, it is generally used for file operations here, and the host needs to open a new thread for implementing the business logic
    * `new AudioRecordDataSource(true)` must be valid; otherwise, the function will not be called back
    * @param audioDatas
  */
    @Override
    public void onNextAudioData(final short[] audioDatas, final int readBufferLength){
    }
```

### Descriptions of other important classes
#### **AudioRecognizeRequest**
If both `templateName` and `customTemplate` are set, `templateName` will be used preferably.

| Parameter                | Type    | Required | Description                                           | Default Value |
| ------------------ | ---------------------- | -------- | ------------------------ | ------------- |
| pcmAudioDataSource | PcmAudioDataSource     | Yes       | Audio data source               | None            |
| templateName       | String                 | No       | Template name set in the console | None            |
| customTemplate     | AudioRecognizeTemplate | No       | Custom template         | ("16k_zh", 1) |

#### **AudioRecognizeResult**
Speech recognition result object, which corresponds to the `AudioRecognizeRequest` object and is used to return the speech recognition result.

| Parameter | Type   | Description                  |
| -------- | ------ | ------------------------- |
| code     | Int    | Recognition status code                |
| message  | String | Recognition prompt message              |
| text     | String | Recognition result                  |
| seq      | Int    | Sequence number of the audio segment          |
| voiceId  | String | ID of the audio stream of the audio segment |
| cookie   | String | Cookie value                 |

#### **AudioRecognizeTemplate**
Custom audio template, for which you need to set the following parameters:

| Parameter           | Type                  | Required | Description           |
| --------------- | ------ | -------- | ------------ |
| engineModelType | String | Yes       | Engine model type |
| resType         | Int    | Yes       | Result return method |

**Sample:**
```
AudioRecognizeTemplate audioRecognizeTemplate = new AudioRecognizeTemplate("16k_zh",1);
```

#### **PcmAudioDataSource**
This API class can be implemented to recognize mono-channel PCM audio data with a sample rate of 16 kHz. It mainly includes the following APIs:
- Add data to the speech recognizer: copy the data with the length of `length` starting from subscript 0 to the `audioPcmData` array, and the actual length of the copied data will be returned.
```
int read(short[] audioPcmData, int length);
```
- Callback function when recognition is started, where you can perform initialization.
```
void start() throws AudioRecognizerException;
```
- Callback function when recognition is ended, where you can perform clearing.
```
void stop();
```
- Get the path of the SDK recording source file in PCM format.
```
void savePcmFileCallBack(String filePath);
```
- Get the path of the SDK recording source file in WAV format.
```
void saveWaveFileCallBack(String filePath);
```
- Set the maximum amount of data read by the speech recognizer each time.
```
int maxLengthOnceRead();
```


#### **AudioRecordDataSource**
Implementation class of the `PcmAudioDataSource` API, which can directly read the audio data input by the mic for real-time recognition.

#### **AudioFileDataSource**
Implementation class of the `PcmAudioDataSource` API, which can directly read mono-channel PCM audio data files with a sample rate of 16 kHz.

>!Data in other formats cannot be recognized accurately.

#### **AAILogger**
You can use `AAILogger` to choose to output logs at the DEBUG, INFO, WARN, or ERROR level.

```
public static void disableDebug();
public static void disableInfo();
public static void disableWarn();
public static void disableError();
public static void enableDebug();
public static void enableInfo();
public static void enableWarn();
public static void enableError();
```

## Guide for Local Audio Data Caching
You can choose to save audios in the host layer locally by following the steps below:
1. Set `isSaveAudioRecordFiles` to `true` during the initialization of `new AudioRecordDataSource(isSaveAudioRecordFiles)`.
2. Add the file logic for creating the recording in the `AudioRecognizeStateListener.onStartRecord` callback function. You can customize the path and filename.
3. Add the stream closing logic in the `AudioRecognizeStateListener.onStopRecord` callback function and optionally save PCM files as WAV files.
4. Add the logic for writing audio streams to local files in the `AudioRecognizeStateListener.onNextAudioData` callback function.
5. As the callback functions all run on the SDK thread, to avoid slow writes that may affect the internal running smoothness of the SDK, we recommend you complete the above steps in a single thread pool. For more information, see the sample code in the `MainActivity` class in the demo project.
