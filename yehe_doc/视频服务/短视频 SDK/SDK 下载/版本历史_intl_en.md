### v8.1 Released on December 3, 2020
- Android: improved the image quality and clarity of short videos.
- Android: changed the parameter type of beauty filter APIs from `int` to `float`.
- Android: fixed the issue where the returned value was exceptional after short video shoot was paused.
- Android: fixed some crash and compatibility issues.

### v8.0 Released on November 16, 2020
- iOS: fixed the issue where the application occasionally froze after multiple stickers were added.
- iOS: fixed the occasional crash caused by bubble subtitle editing.
- Android: made cover upload compatible with device models on Android 9.0 and above.
- Android: fixed the issue where the video was out of sync when three-screen trio was switched to the background and then back to the foreground.
- Android: fixed the occasional issue of `UGCKit` with black screen on the compressed video preview page.
- Android: fixed the issue of `UGCKit` where the volume set during video editing didn't take effect.
- Android: fixed the occasional issue of `UGCKit` where the undo button was not displayed on the action page.

### v7.9 Released on October 23, 2020
- iOS: fixed the issue where audio was missing at the end of edited short videos.
- iOS: fixed the issue where the added background music was not reset when a short video was shot again.
- Android: fixed several crashes of the UGSV SDK and enhanced the stability.
- Android: fixed the crash of the shooting feature on Android 5.0 and below.
- iOS and Android: optimized the delay control algorithm of the LVB player to avoid frequent acceleration and deceleration.

### v7.8 Released on September 27, 2020
- iOS: fixed the compatibility issue of superplayer on iOS 14.
- Android: updated `VideoUploadSDK` in UGCKit.
- Android: fixed the crash of advanced beauty filters on Android 4.4.
- Android: fixed the occasional issue where the audio and video were out of sync during shoot in the UGSV SDK.
- Android: fixed the issue with error log printing when the UGSV SDK was uninitialized.
- Android: fixed the issue with slow callback when shoot was ended in the UGSV SDK.
- Android: fixed multiple crashes reported in the UGSV SDK.

### v7.7 Released on September 8, 2020
- Android: optimized basic image polishing and beauty filters and added the brightening and natural filters.
- iOS: fixed the compatibility issue of UGSV on iOS 14.

### v7.6 Released on August 24, 2020
- iOS and Android: optimized AI beauty filters and profile face makeup effects, fixed the issue with covered lip gloss, and improved the face detection and tracking accuracy.
- iOS and Android: internationalized the SDK event and error callback messages.
- Android: moved the callback of custom short video preprocessing before sticker addition.
- Android: fixed the occasional crash caused by the release of bitmap in short videos.
- Android: fixed the issue where chorus in short videos kept loading on certain device models.

### v7.5 Released on July 31, 2020
iOS: fixed the issue where post-roll watermarks flickered during short video playback.

### v7.4 Released on July 3, 2020
- iOS and Android: fixed the issue where composing videos without audio track failed.
- Android: optimized the output effect of short video editing and fixed the issue where the image clarity was insufficient on certain device models.

### v7.2 Released on April 17, 2020
- iOS and Android: optimized visual effect APIs such as filter and green screen keying and aggregated them into the `TXBeautyManager` class for a unified call method.

### v7.1 Released on March 30, 2020
- Android: supported the HE-AAC audio format for short video editing, which is more compatible with third-party video editors.
- Android: fixed occasional issues of `UGCKit` where the cropping page was displayed exceptionally and shoot failed. 

### v7.0 Released on March 9, 2020
- Android: fixed the occasional crash of animated face effects.
- Android: fixed the occasional crash caused by stopping shoot while frequently switching cameras.
- iOS and Android: fixed several bugs.

### v6.9 Released on January 15, 2020
- iOS and Android: componentized the UI of `UGC TUIKit` and supported custom themes for easier integration and modification.
- iOS and Android: supported three-screen trio and volume adjustment.
- Android: supported Android 10.
- Android: supported hardware encoding to expedite short video preprocessing.
- iOS: optimized the chorus module and fixed issues such as out-of-sync audio/video.

### v6.8 Released on November 15, 2019
- iOS and Android: supported shoot in 4:3 aspect ratio.
- iOS and Android: added various image polishing features such as skin brightening, eye enlarging, teeth whitening, wrinkle removal, makeup, and gesture recognition.
- Android: improved the generation speed and efficiency during short video editing.
- Android: fixed the issue where the bottom-right border of the focus frame was thicker than the top-left border.
- Android: fixed the issue in the Enterprise Edition where eye enlarging, face slimming, and animated effects didn't work on certain device models.
- iOS: fixed the occasional issue with black screen during short video preview.

### v6.7 Released on September 29, 2019
- iOS and Android: supported shoot in 16:9 aspect ratio.
- iOS and Android: fixed the reported occasional crashes.
- Android: fixed the occasional noise during short video composition.
- iOS: fixed the compatibility issue with Arabic.
- iOS: fixed the occasional issue where saving edited videos in high quality failed.

### v6.6 Patch Released on September 10, 2019
- iOS and Android: fixed several bugs.
- Android: fixed the issues with memory usage and library conflict in the Enterprise Edition.
- iOS: added compatibility support for iOS 13.

### v6.6.7458 Released on August 6, 2019
- Android: supported 64-bit in the Enterprise Edition and dynamic download from the image polishing material library.
- Android: fixed the crash of the short video editing page.
- iOS: fixed the occasional issue where the returned value was incorrect during thumbnail acquisition by time point in `TXVideoEditer`.
- iOS: fixed the issue where the set animated effects didn't work after being switched to the background.

### v6.5.7272 Released on June 12, 2019
- iOS and Android: supported image upload.
- Android: fixed issues such as occasional OpenGL exceptions during short video generation.
- Android: fixed the issue where the rotation direction wouldn't refresh after pause during video editing.

### v6.4.7328 Released on May 15, 2019
Fixed recently reported bugs to further improve the stability.  

### v5.4 Released on January 4, 2019
- iOS and Android: improved the success rate of short video upload.
- iOS: fixed some crashes caused by the image transition composition feature.

### v5.3 Released on October 25, 2018
- iOS and Android: supported fade-in/fade-out in background music editing.
- iOS and Android: supported video shoot in 1080p.
- iOS and Android: supported splicing videos without audio.
- Android: fixed the issue where the shoot progress callback was not timely.
- Android: fixed the issue where the orientation of some video thumbnails was incorrect.
- Android: fixed the issue with lags during preprocessing.
- iOS: supported setting whether to loop the background music in video shoot.
- iOS: optimized short video upload.
- iOS: added the feature of generating GIFs of original videos in the demo.

### v5.2 Released on September 14, 2018
- iOS and Android: supported editing larger 4K videos and specifying the resolution for thumbnail extraction.
- iOS and Android: added the draft box feature demo. For more information, please see the UGSV app.
- iOS and Android: supported dynamic screen rotation in video editing.
- Android: added the quick thumbnail acquisition API in video editing.
- Android: fixed the issue where the angle setting of dynamic stickers didn't work.
- Android: fixed the occasional issue with out-of-sync audio/video during video composition and improved the image quality of the output videos.
- iOS: fixed the thread safety issue caused by quick and frequent background music switching.
- iOS: fixed the issue where the background music volume was inconsistent between video shoot and preview.
- iOS: fixed the issue where the post-roll watermark PTS was exceptional when special effects were repeatedly added in video editing.

### v5.1 Released on August 18, 2018
- iOS and Android: added multiple UGSV editions of Lite, Basic, Enterprise, and Enterprise Pro to meet the needs of different customers. Different editions require application for corresponding licenses.
- iOS and Android: optimized beauty filters and redesigned and added multiple filter effects.
- iOS and Android: added the gesture effects for shoot and editing filters.
- iOS and Android: optimized the duet chorus feature.
- iOS and Android: added the features of hold-and-press to shoot, click to shoot, and click to capture in the UGSV app, added the countdown feature in chorus, and added the reverb and voice changing effect selectors on the shoot page.
- iOS and Android: internationalized the UGSV app to support Chinese and English.
- iOS and Android: redesigned the demo's main UI for better ease of use.
- Android: added the quick import capability which is suitable for fast import of large videos.
- Android: added the filter level setting API in video editing.
- iOS: supported two-pass encoding in video editing to generate higher image quality.
- iOS: fixed the issue where the CPU utilization was high when editing was started after shoot exited exceptionally.
- iOS: fixed the issue with blurred screen during short video shoot on iOS 12.

### v5.0 Released on July 18, 2018
- iOS and Android: supported duet chorus for left-right video composition.
- iOS and Android: supported dual-channel for edited videos.
- iOS and Android: supported setting audio sample rate and rendering mode for shoot.
- Android: optimized the image quality of shot and edited videos to make the output files smaller.
- Android: improved the video preprocessing and generation speed in short video editing.
- Android: fixed the issue with black screen caused by portrait/landscape mode switching during shoot.
- Android: fixed the issue where an error would be reported when shoot start or end was quickly clicked.
- iOS: improved the loading speed of edited videos.
- iOS: fixed the occasional issue whether the video image of edited videos was split.
- iOS: fixed the occasional issue whether black frames were displayed at the end of edited videos.
- iOS: fixed the issue where audio playback would end prematurely when the edited preview video was set to slow playback.
- iOS: adapted the iOS demo to iPhone X.
- iOS: fixed memory leaks to improve the stability and added module definitions to better support Swift integration.

### v4.9 Released on June 14, 2018
- iOS and Android: optimized the UGSV license integration method and supported auto-renewal.
- Android: added the capability to convert images to videos, supported multiple transition animations for image switching, such as sliding up/down/left/right, zooming in, zooming out, rotating-zooming, and fade-in/fade-out.
- Android: optimized the generation speed of edited short videos and fixed issues such as memory leaks.
- iOS: improved the loading speed of local background music and thumbnails in short videos and the acquisition speed of `videoInfo`.
- iOS: optimized the image quality of edited short videos.
- iOS: fixed occasional issues with lags and black frames in short video shoot, post-roll watermark flickering, and memory leaks.

### v4.7 Released on May 25, 2018
- iOS and Android: added new filter effects in short videos, such as blinds, phantom, lightning, mirror, and illusion.
- Android: added texture support for custom data.
- Android: optimized the memory usage of short video editing and composition and reduced the peak memory usage during editing and generation.
- iOS: added the capability to convert images to videos, supported multiple transition animations for image switching, such as sliding up/down/left/right, zooming in, zooming out, rotating-zooming, and fade-in/fade-out.
- iOS: fixed the issue where the short video background music needed to be completely played back before it could be called back.

### v4.6 Released on May 4, 2018
- iOS and Android: added the reverb effects such as hall and husky and voice changing effects such as little girl and middle-aged man in short video shoot.
- iOS and Android: added the external segment storage directory setting API in short video shoot.
- iOS and Android: supported adding pure video streams as background music in short video editing.
- iOS and Android: added the split-screen composition API in short video composition.
- iOS and Android: removed the upper limit of bitrate in short video shoot.
- Android: optimized small file upload to increase the success rate.
- Android: fixed the crash caused by incorrect animated effect paths.
- iOS: supported Bitcode in short videos.

### v4.5 Released on April 13, 2018
- iOS and Android: added demo code for file upload and integrated the VOD service to provide an all-in-one solution from shoot, special effect production, upload, and transcoding to porn detection, distribution, and playback.
- iOS and Android: supported the GIF format for cover upload and added the segment composition feature.
- iOS and Android: added two special effects, supported removing background music from animated effects, and supported quickly canceling all filter effects.
- Android: optimized the short video production process and fixed issues with inability to play back uploaded large files, occasional black frames during thumbnail acquisition, and occasional out-of-sync audio/video.
- Android: supported customizing the bitrate when editing short videos.
- Android: supported editing video files without audio track.

### v4.2
iOS and Android: improved the performance of the Enterprise Edition SDK, supported image polishing and animated effects, greatly increased the frame rate on iOS, and reduced the GPU usage on Android.

### v4.1
- iOS and Android: added the resolution and bitrate switching APIs in short video shoot.
- iOS and Android: added the capturing API in short video shoot.
- iOS and Android: supported setting the start time and loop of background music in short video editing.

### v3.9
- iOS and Android: greatly upgraded the animated stickers and added the HDR and HD sticker effects to make stickers more appealing.
- iOS and Android: added the AI-based keying capability.
- iOS and Android: added three time-based special effects of slow motion, loop, and reverse.
- iOS and Android: added a variety of filter effects for better choice.
- iOS and Android: added a variety of dynamic and static stickers and supported customizing more stickers.
- iOS and Android: supported adding bubble subtitles to videos.
- iOS and Android: supported muted shoot for convenient post-production.
- iOS and Android: supported switching portrait/landscape mode during shoot.
- iOS and Android: fixed several bugs.
- Android: integrated a new COS architecture with `UGCPublish` to optimize the short video upload flow.

### v3.4
- iOS and Android: added the existing segment deleting, multi-aspect ratio switching, and focus adjustment features in short video shoot.
- iOS and Android: added the post-roll watermark feature in short video editing.
- iOS: fixed the compatibility issue with iOS 11.

### v3.3
- iOS and Android: fixed some bugs reported by users in the last week.
- Android: fixed the issues with green screen during shoot and black screen during playback on certain device models.

### v3.1
- iOS and Android: added the chin slimming and nose narrowing features in the Enterprise Edition.
- iOS and Android: optimized the beauty filter algorithm and added the rosy skin filter and multiple beauty filter styles.
- Android: added three beauty filter styles of smooth, natural, and misty.
- Android: added the speed adjustment, background music adding, and subtitling features in short video editing.
- iOS: added the smooth and natural beauty filter styles.

### v3.0
- iOS and Android: reconstructed the beauty filter module to improve the beauty filter effect while reducing GPU utilization.
- iOS and Android: added the `pauseRecord` and `resumeRecord` APIs to `TXUGCRecord` to support multi-segment shoot.
- iOS: added APIs for quick cropping and editing.

### v2.0.5
- Android: added the watermark feature in short video editing.
- Android: added the multi-segment short video shoot feature.
- iOS and Android: fixed several bugs.

### v2.0.4
- iOS and Android: added the callback preprocessing API for beauty filters during short video shoot.
- iOS and Android: added the checkpoint restart capability in short video upload.
- Android: optimized the short video cropping and splicing features and added the filter editing feature.
- iOS: added various features in short video editing, such as filter, watermark, background music, subtitling, and speed adjustment.

### v2.0.3
- iOS and Android: optimized the demo directory and code structure to reduce integration costs and added easy-to-use demos for short video shoot, cropping, and splicing.
- Android: added the short video cropping and splicing features.
- iOS: fixed the issue with overexposure on iOS to make exposure more natural.

### v2.0.2
- iOS and Android: optimized the short video upload protocol.
- Android: added the eye enlarging and face slimming features in the Pro Edition.
- Android: optimized the hardware encoding effect to improve the encoding quality.
- iOS: added the short video cropping and splicing features.
- iOS: supported Bitcode in the Lite Edition.

### v2.0.1
- iOS and Android: added the feature of adding background music to short videos.
- Android: added the green screen keying feature in the Pro Edition.

### v2.0.0
iOS and Android: added the short video capturing and release features.

