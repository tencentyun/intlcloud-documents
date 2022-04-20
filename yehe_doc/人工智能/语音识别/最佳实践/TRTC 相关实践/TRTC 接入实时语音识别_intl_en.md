## Overview
After you connect to the TRTC service, you may need real-time speech recognition sometimes so as to implement real-time conference subtitling or voice on-screen commenting. This document describes how to connect to the ASR service after connecting to TRTC on an Android or iOS client.

## Connection Process on iOS
1. You need to [connect to TRTC](https://intl.cloud.tencent.com/document/product/647/35102) first.
2. Set the audio stream format according to ASR's [audio stream format requirements](https://cloud.tencent.com/document/product/1093/35799) and the [TRTC document](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html).
3. Set the audio source delegate in the [TRTC API protocol](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html) and configure ASR to read the audio source.

```objective-c
//1. `TRTCAudioFrameDelegate` is the protocol for TRTC to get the audio source. As ASR recognizes audio data with 8 or 16 kHz sample rate, you need to set `setAudioQuality` to TRTCCloudDef#TRTC_AUDIO_QUALITY_SPEECH (LD, 16 kHz sample rate, mono-channel, and 16 Kbps bitrate).

- (void) onCapturedRawAudioFrame:(TRTCAudioFrame *)frame {// This method is the callback of the original audio data collected by TRTC through the local mic:

  NSUInteger readLength = [frame.data length];
  void *pcmBytes = (void *)frame.data.bytes;
  [dataSource didRecordAudioData:pcmBytes length:readLength];
}
```
4. Set the ASR audio source as a third party and implement the specific logic.

4.1 Access to third-party audio sources requires implementing the `QCloudAudioDataSource` protocol in ASR. Below is the sample code:
```objective-c
#import<QCloudSDK/QCloudSDK.h>

//1. To use a third-party external custom data source to transfer audio data, you need to implement the `QCloudAudioDataSource` protocol for the data source.
QDAudioDataSource *dataSource = [[QDAudioDataSource alloc] init];

//2. Create a `QCloudRealTimeRecognizer` recognition instance.
QCloudRealTimeRecognizer *realTimeRecognizer = [[QCloudRealTimeRecognizer alloc] initWithConfig:config dataSource:dataSource];
```
4.2 The `QCloudAudioDataSource` protocol for connecting to ASR is as follows. For more information, see [Protocol Details](https://intl.cloud.tencent.com/document/product/1118/43383). You can refer to the code in the demo's `QDAudioDataSource.m` file.

```objc
@interface QDAudioDataSource : NSObject<QCloudAudioDataSource>
@end

@implementation QDAudioDataSource
@synthesize running = _running;

// The SDK will call this method to get the current status.
- (BOOL)running{
    return _recording;
}

// The SDK will call the `start` method. Implementing the class of this protocol requires initializing the data source.
- (void)start:(void(^)(BOOL didStart, NSError *error))completion{
  _data = [[NSMutableData alloc] init];
}

// The SDK will call the `stop` method. Implementing the class of this protocol requires stopping supplying data.
- (void)stop{
  _recording = NO;
  _data = nil;
}

// The SDK will call this method of the object that implements the protocol to read audio data.
- (nullable NSData *)readData:(NSInteger)expectLength{
  NSData *data = nil;
  if ([_data length] >= _offset + expectLength) {
      data = [_data subdataWithRange:NSMakeRange(_offset, expectLength)];
      [_data replaceBytesInRange:NSMakeRange(_offset, expectLength) withBytes:NULL length:0];
  }
  return data;
}

// This is only a demonstration. You should populate the audio data source with data on your own.
- (void)didRecordAudioData:(void * const )bytes length:(NSInteger)length{
  [_data appendBytes:bytes length:length];
}
@end
```


## Connection Process on Android

1. You need to [connect to TRTC](https://intl.cloud.tencent.com/document/product/647/35102) first.
2. Set the audio stream format according to ASR's [audio stream format requirements](https://cloud.tencent.com/document/product/1093/35799) and the [TRTC document](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html).
3. Set the audio source delegate in the [TRTC API protocol](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html) and configure ASR to read the audio source.
4. Set the ASR audio source as a third party and implement the specific logic.
 - Access to third-party audio sources requires implementing the `PcmAudioDataSource` API in ASR. Below is the sample code:
```java
//1. To use a third-party external custom data source to transfer audio data, you need to implement the `PcmAudioDataSource` API for the data source.
AudioDataSource dataSource = new AudioDataSource(); 
//2. Initialize the speech recognition request.
final AudioRecognizeRequest audioRecognizeRequest = new AudioRecognizeRequest.Builder()
.pcmAudioDataSource(dataSource)
.build(); 
```
 - The `PcmAudioDataSource` API for connecting to ASR is implemented as follows. For more information, see [Protocol Details](https://intl.cloud.tencent.com/document/product/1118/43388). You can refer to the code in the demo's `AudioDataSource.java` file.
```java
private ConcurrentLinkedDeque<Short> shortList = new ConcurrentLinkedDeque<>();
private static boolean first;

public class AudioDataSource implements PcmAudioDataSource { 
// Add data to the speech recognizer: copy the data with the length of `length` starting from subscript 0 to the `audioPcmData` array, and the actual length of the copied data will be returned. 
@Override
    public int read(short[] audioPcmData, int length) {
        short[] tempData = new short[length];
        try {
            if (!first) {
                first = true;
                SystemClock.sleep(1000);
            }
            ConcurrentLinkedDeque<Short> shorts;
            shorts = getDataList();
            if (shorts.size() < length) {
                SystemClock.sleep(300);
            }
            shorts = getDataList();
            for (int i = 0; i < tempData.length; i++) {
                tempData[i] = shorts.poll();
            }
            System.arraycopy(tempData, 0, audioPcmData, 0, tempData.length);
        } catch (Exception e) {
            return 0;
        }
        return tempData.length;
    } 
// Callback function when recognition is started, where you can perform initialization.
@Override
    public void start() {
    } 
// Callback function when recognition is ended, where you can perform clearing.
 @Override
    public void stop() {
    } 
// Set the maximum amount of data read by the speech recognizer each time. 
@Override
    public int maxLengthOnceRead() {
        return 640;
    } 
// This is only a demonstration. You should populate the audio data source with data on your own.
public void writeByte(short[] pcmData) {
        for (short pcmDatum : pcmData) {
            shortList.add(pcmDatum);
        }
    }  
private ConcurrentLinkedDeque<Short> getDataList() {
        return shortList;
    } 
```
 - The protocol for connecting the TRTC audio source to ASR is as follows. For more information, see [TRTC protocol details](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html).
```java
//1. `TRTCCloudListener.TRTCAudioFrameListener` is the callback for the audio data obtained by TRTC from the local mic. As ASR recognizes audio data with 8 or 16 kHz sample rate, you need to set `setAudioQuality` to TRTCCloudDef#TRTC_AUDIO_QUALITY_SPEECH (LD, 16 kHz sample rate, mono-channel, and 16 Kbps bitrate).
void onCapturedRawAudioFrame(TRTCCloudDef.TRTCAudioFrame trtcAudioFrame) {
dataSource.writeByte(bytesToShort(trtcAudioFrame.data));; 
} 
// The following method is to convert a `bytes` array into a `short` array:
public static short[] bytesToShort(byte[] bytes) {
    if (bytes == null) {
        return null;
    }
    short[] shorts = new short[bytes.length / 2];
ByteBuffer.wrap(bytes).order(ByteOrder.LITTLE_ENDIAN).asShortBuffer().get(shorts);
    return shorts;
}
```
