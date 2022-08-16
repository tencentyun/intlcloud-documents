
[](id:que2)
### What should I know about `TXUGCPublish.h`?
Since v4.5, we have moved `TXUGCPublish` classes from the SDK to the demo. To use the classes, just drag the `VideoUpload` directory to your project.

[](id:que3)
### What should I do if an error was reported when I directly ran the demo in Xcode?
- Error message:
![](https://main.qcloudimg.com/raw/4c429ae5017c7990e7bf332a4b8de0ab.png)

- Solution: Run `pod install`.

[](id:que4)
### What should I do if a short video shoot error was reported when I connected to Xcode for debugging?
Error message: `Main Thread Checker: UI API called on a background thread`
![](https://main.qcloudimg.com/raw/04b272c456b0e69239c0867a8e964d7a.jpg)

- Cause: Some APIs (usually those related to UI) need to be called in the main thread. If they are not called in the main thread and **Main Thread Checker** is selected, this error will occur.
- Solution: Select **Product > Scheme > Edit Scheme > Run > Diagnostics** and unselect **Main Thread Checker**.
>? This issue has been fixed in v4.9.


[](id:que5)
### What should I do if I could not find the header file when using the SDK?
Run `pod install`.


[](id:que6)
### What should I do if a crash occurs or an error is reported saying that class methods could not be found when I run the project?
The SDK uses certain class methods. To load them, you need to add `-ObjC` to **Build Settings > Linking > Other Linker Flags** in the project.

[](id:que7)
### What should I do if the background music set for short video shooting is not played?

1. Check whether the file exists in the background music path passed in and whether the file can be played back normally.
2. Check whether the APIs are called in the following sequence: `startCameraSimple:preview:` > `setBGM:` > `startRecord`.

>! Many APIs need to be called in a certain sequence in order to work. Such requirements are often specified in code comments.
For example, `setVideoResolution:`, `setVideoBitrate:`, and `setAspectRatio:` must all be called before `startRecord` in order to work.


[](id:que8)
### Can I loop the background music during video shooting?
Currently, loop playback is not supported.

[](id:que9)
### I didn’t receive a completion callback when the background music for video shooting ended (`endTime`). Why?
If the `endTime` is smaller than the total music file duration, in SDK 4.6 or earlier, the completion callback will be triggered only after the playback of the background music is completed. In SDK 4.7 or later, the completion callback will be triggered at the time specified by `endTime`.


[](id:que10)
### Why is it slow the first time I turn on the camera to shoot videos?
iPhone’s camera tends to take a long time to start (cold start). This is also the case if you start the camera using a system API.

It’s not practical to start the camera in a child thread. Tests show that it will take even longer to start the camera in a child thread. If the camera is started and closed frequently in the main thread, the response delay of the child thread will also increase.


[](id:que11)
### How do I implement shooting resumption?
When shooting is interrupted, do not call `stopRecord` or `stopCameraPreview` (if you do, the shooting will stop, and you can only start a new shooting). Instead, call `pauseRecord`, use `TXUGCPartsManager.getVideoPathList` to get the video segment already shot, and call `TXVideoJoiner.joinVideo` to merge it into the final video. This method works in versions earlier than 4.5. In 4.5 and later versions, just call `TXUGCPartsManager.joinAllParts` to splice the final video, which is quicker.


[](id:que12)
### What should I do if I do not receive a callback when video shooting is completed?
- Check whether `stopRecord` is called. Only after `stopRecord` is called can the completion callback be returned.
- Check whether the APIs are called in the main thread.



[](id:que13)
### During shooting, I played a video using another player. When I switched back to continue shooting, no audio is recorded. Why?
The `AudioSession` on iOS is shared by all audio/video applications. When you switch to another player during shooting, the `AudioSession` will be occupied by the player. If it is not released in a timely manner, after you switch back, `AudioSession` may not work for the shooting module. The SDK provides two APIs: `-(void) pauseAudioSession` and `-(void) resumeAudioSession`. You can call `pauseAudioSession` before you switch to another player and then call `resumeAudioSession` before you switch back to resume shooting.



[](id:que14)
### Why are the videos shot blurry?
Videos may be blurry if the bitrate and resolution do not match. You can try increasing the bitrate moderately or enable B-frame encoding.



[](id:que15)
### During video editing, I switched the application to the background and then switched back. The system failed to generate the editing result. What should I do?
Hardware encoding (featuring higher encoding efficiency and image quality) is used by default for video generation. However, the hardware encoder will stop running if the application is switched to the background, resulting in video generation failure. The SDK provides two APIs: `pauseGenerate` and `resumeGenerate`. When the application is switched to the background, you can call `pauseGenerate` to pause video generation. When the application returns to the foreground, you can call `resumeGenerate` to resume video generation.

>! After `resumeGenerate` is called, the SDK will try to restart the hardware encoder. This may not always succeed, or the hardware encoder may fail to encode the first few frames after restart. In such cases, the SDK will throw the `TXVideoGenerateListener` error event internally, and the video will need to be generated again.



[](id:que16)
### What should I do if I fail to upload a video?
Status code:
![](https://main.qcloudimg.com/raw/fd39ad5be960bc3988b4801181e37bf3.png)
1. Check whether the file is in the local sandbox. To upload a file in the media library, you need to copy it to the local sandbox first.
2. The error code 1002 indicates that there is an issue with the signature, the timestamp has expired, or the VOD service is not activated.
3. The error code 1003 indicates that a request parameter is invalid or the format of the file is not supported.

[](id:que17)
### Does the SDK support picture taking?
The UGSV SDK supports photo capturing. You can simply call the `snapshot` API of the `TXUGCRecord` class to get an image after the preview starts.


[](id:que18)
### What should I do if the error “Use of undeclared identifier 'TXVideoInfo'” occurs when I integrate the SDK?
The error indicates that the compiler failed to find the `TXVideoInfo` class. Please check whether the SDK (frameworks) is imported correctly. For details, see [SDK Integration (Xcode)](https://intl.cloud.tencent.com/document/product/1069/38012).

[](id:que19)
### What should I do if the error “-1，Failed to enable encoder” occurs when I call the video generation API?
1. Try different devices and see if the problem always occurs.
2. Download the latest version of the demo. If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) and send us the complete log.

