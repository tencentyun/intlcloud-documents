### Version 9.4 Released on December 9, 2021
- iOS: fixed the issue where, when animated effects are enabled, the effects are not applied to the videos shot.
- Android: fixed the issue where video editing does not support outputting 1080p videos.
- Android & iOS: added HTTPDNS request URLs for video upload.

### Version 9.3 Released on November 4, 2021
- iOS: fixed the issue of playback speed change when special effects are previewed during post-shooting editing.
- iOS: fixed crash of `TXCRenderView`.
- Android: fixed lag and crash during composition of triple split-screen videos on Xiaomi Mi 9.

### Version 9.2 Released on September 26, 2021
- Android: fixed the issue where only half of thumbnails are generated.
- Android: fixed lag during video composition on MediaTek Dimensity 1200.
- Android: improved compatibility with the 9:16 aspect ratio during video shooting.
- iOS: fixed audio exception when videos with 48000 Hz mono audio are spliced.

### Version 9.1 Released on September 2, 2021
- Android: fixed several stability issues.
- Android: improved the clarity of generated videos.
- Android: fixed crash during playback on certain Android 5.x devices.
- iOS: fixed the issue of color saturation distortion of exported videos on iPhone 12 and later models.

### Version 9.0 Released on August 6, 2021
- Android: fixed slow loading of the duet feature.
- Android: improved the performance of the UGC SDK.
- Android: improved stability.
- Android: fixed occasional video clipping inaccuracy.
- iOS: fixed the compression error during video upload after the application is switched to the background.

### Version 8.9 Released on July 15, 2021
- iOS: fixed the issue where, after users add a sticker, switch to static stickers, and return, dynamic stickers are displayed instead of static ones.
- iOS: fixed the issue where, after users change the order of selected videos/images and click to deselect a video/image, the video/image in the original position of the clicked video/image is deselected.
- Android: fixed the issue where images are rotated when the slideshow feature is used on Xiaomi phones.

### Version 8.8 Released on June 18, 2021
- iOS: fixed memory leaks caused by frequent starting and stopping of the VOD player.
- iOS & Android: fixed the issue where videos load slowly after users pause VOD playback and adjust the playback progress.

### Version 8.7 Released on May 24, 2021
iOS: fixed electrical noise of the shooting module on iOS 14.5.

### Version 8.6 Released on May 6, 2021
- iOS: fixed occasional surge in memory usage by the VOD player.
- iOS: fixed Swift compilation warnings.
- iOS & Android: fixed several stability issues of the UGC SDK.
- iOS & Android: optimized the upload path selection logic to reduce upload failure.

### Version 8.5 Released on March 18, 2021
- iOS & Android: improved the effects of advanced beauty filters including face slimming, eye enlarging, chin slimming, etc.
- iOS & Android: added an API for the advanced beauty filter of face narrowing.
- iOS & Android: enhanced the capability to detect facial features to improve the effects of advanced beauty filters.
- iOS & Android: added an API for the advanced beauty filter of face narrowing.
- iOS & Android: fixed the issue of slow seek operations of the superplayer for some network streams.
- Android: fixed the error that occurs when the superplayer plays videos by file ID.

### Version 8.4 Released on February 7, 2021
- iOS & Android: fixed the verification safety issue.
- Android: supported preview with multiple audio tracks.
- iOS: optimized pre-processing performance and enhanced stability.
- iOS: fixed the problem with the callback of facial feature coordinates for beauty filter application.

### Version 8.3 Released on January 15, 2021
- Android: fixed the problem of failure to splice together video segments if users delete segments during shooting.
- Android: fixed multiple crash issues.
- iOS: fixed the problem of the SDK crashing when playing back videos in slow motion.
- iOS: fixed the problem of black screens in certain steps of slideshow generation.
- iOS: fixed some crash issues caused by incompatibility.

### Version 8.2 Released on December 24, 2020
- Android: fixed the bug of the green screen feature no longer functioning after camera switch.
- Android: fixed the occasional instability of UGSV.
- iOS: fixed the bug of occasional incorrect aspect ratio after users rotate or flip a video.
- iOS: fixed the bug of video composition failure after the landscape mode is enabled during shooting.
- iOS: fixed the occasional instability of the superplayer.

### Version 8.1 Released on December 3, 2020
- Android: improved the image quality and clarity of UGSV.
- Android: changed the type of beauty filter APIs from `int` to `float`.
- Android: fixed the problem of a value indicating failure being returned after shooting pauses.
- Android: fixed some crash and compatibility issues.

### Version 8.0 Released on November 16, 2020
- iOS: fixed the problem of apps occasionally freezing after multiple stickers are added.
- iOS: fixed the problem of apps quitting unexpectedly during bubble subtitle editing.
- Android: supported the uploading of thumbnails on Android 9.0 and above.
- Android: fixed the issue where triple split-screen videos are out of sync after users switch the app to the background and back again.
- Android: fixed the UGCKit problem of occasional black screens when users preview compressed videos.
- Android: fixed the problem of failure to set volume with UGCKit in video editing.
- Android: fixed the UGCKit problem of the Undo button occasionally not showing on the actions UI.

### Version 7.9 Released on October 23, 2020
- iOS: fixed the problem of audio missing towards the end of edited UGSV.
- iOS: fixed the problem of background music used for one shooting being applied to all shootings afterwards.
- Android: fixed multiple crash issues of the UGSV SDK and improved its stability.
- Android: fixed the crash when users shoot videos on Android whose version is below 5.0.
- iOS & Android: optimized the delay control algorithm of the live streaming player to avoid frequent acceleration and deceleration.

### Version 7.8 Released on September 27, 2020
- iOS: fixed the superplayer’s compatibility issue with iOS 14.
- Android: upgraded the video upload SDK in UGCKit.
- Android: fixed the problem of system crash when advanced beauty filters are used on Android 4.4.
- Android: fixed the problem of occasional lip-sync errors during shooting.
- Android: fixed the problem of the error log being printed during deinitialization of the UGSV SDK.
- Android: fixed the problem of slow callback of end to a shooting.
- Android: fixed multiple crash issues of the UGSV SDK reported recently.</td>

### Version 7.7 Released on September 8, 2020
- Android: optimized the basic beauty filters, and added the “skin lightening” and “natural” filters.
- iOS: fixed the compatibility issue with iOS 14.

### Version 7.6 Released on August 24, 2020
- iOS & Android: optimized AI-based beauty filters: fixed wrong lipstick application, enhanced the accuracy of facial feature location, and improved the make-up effect for face profiles.
- iOS & Android: internationalized the SDK event and error callback messages.
- Android: moved the callback of custom pre-processing of UGSV before the adding of stickers.
- Android: fixed the occasional crash caused by the release of bitmap memory.
- Android: fixed the problem of the karaoke page stuck on loading on some devices.

### Version 7.5 Released on July 31, 2020
iOS: fixed the problem of watermarks flashing towards the end of UGSV playback.

### Version 7.4 Released on July 3, 2020
- iOS & Android: fixed the problem of failure to splice videos with no audio tracks.
- Android: optimized the quality of edited UGSV and fixed the lack of image clarity on some devices.

### Version 7.2 Released on April 17, 2020
iOS & Android: optimized visual effect APIs such as filters and green screen keying, and integrated them into the `TXCBeautyManager` class to facilitate calling.

### Version 7.1 Released on March 30, 2020
- Android: supported audio files in the HE-AAC format in video editing, providing better compatibility with third-party videos.
- Android: fixed UGCKit problems including occasional abnormal display of the video clipping page and occasional errors during shooting. 

### Version 7.0 Released on March 9, 2020
- Android: fixed occasional crash when beauty filters or animated effects are used.
- Android: fixed the occasional crash when users end a shooting after frequent camera switch.
- iOS & Android: fixed a number of bugs.

### Version 6.9 Released on January 15, 2020
- iOS & Android: introduced UGC TUIKit to enable modular UI design and theme customization, facilitating integration and modification.
- iOS & Android: supported shooting of triple split-screen videos and volume adjustment.
- Android: made the SDK supported on Android 10.
- Android: started using hardware encoders for UGC to speed up pre-processing.
- iOS: optimized the karaoke module and fixed problems including lip-sync errors.

### Version 6.8 Released on November 15, 2019
- iOS & Android: supported shooting videos in the aspect ratio of 4:3.
- iOS & Android: incorporated new image retouching features into the Enterprise Edition, including skin airbrushing, eye lightening, teeth whitening, wrinkle removing, make-up application, and gesture recognition.
- Android: sped up the generation of UGSV, including post-editing generation.
- Android: fixed the problem of the bottom-right lines of the focus frame being thicker than the top-left lines.
- Android: fixed the problem of the big eye and face slimming filters and animated effects in the Enterprise Edition SDK not working on some devices.
- iOS: fixed the problem of occasional black screens when users preview UGSV.

### Version 6.7 Released on September 29, 2019
- iOS & Android: supported shooting videos in the aspect ratio of 16:9.
- iOS & Android: fixed the occasional crash issues reported.
- Android: fixed the occasional noise in videos after composition.
- iOS: supported Arabic.
- iOS: fixed the problem of users occasionally failing to save high-quality videos during editing.

### Version 6.6 Patch Released on September 10, 2019
- iOS & Android: fixed a number of bugs.
- Android: fixed the memory usage and library conflict problems of the Enterprise Edition SDK.
- iOS: made the SDK supported on iOS 13.

### Version 6.6.7458 Released on August 6, 2019
- Android: made the Enterprise Edition SDK supported on 64- bit operating systems and supported dynamic downloading from the library of image retouching materials.
- Android: fixed the crash of the UGSV editing page.
- iOS: fixed the problem of TXVideoEditer returning incorrect data when trying to get the thumbnail of a time point.
- iOS: fixed the problem of animated effects not working after users switch apps to the background.

### Version 6.5.7272 Released on June 12, 2019
- iOS & Android: supported uploading images.
- Android: fixed the problem of occasional OpenGL errors during the generation of UGSV.
- Android: fixed the problem of image updating failure when users pause and rotate a video during editing.

### Version 6.4.7328 Released on May 15, 2019
Fixed a number of bugs reported recently and enhanced the stability of the SDK.  

### Version 5.4 Released on January 4, 2019
-iOS & Android: improved the success rate of UGSV uploading.
- iOS: fixed some crash issues during the use of the slideshow feature.

### Version 5.3 Released on October 25, 2018
- iOS & Android: supported fade-in and fade-out for background music.
- iOS & Android: supported shooting 1080p videos.
- iOS & Android: supported splicing videos without audio.
- Android: fixed the delay in the callback of the shooting progress.
- Android: fixed the problem of wrong rotation degrees for some video thumbnails.
- Android: fixed stutter for pre-processing.
- iOS: allowed users to choose whether to loop background music.
- iOS: optimized the uploading of UGSV.
- iOS: added the feature of generating GIFs of original videos to the demo.

### Version 5.2 Released on September 14, 2018
- iOS & Android: supported editing long 4K videos and getting thumbnails in specified resolution.
- iOS & Android: added an example on how to use the shooting draft feature. For details, see the document about UGSV apps.
- iOS & Android: supported dynamically rotating video images during editing.
- Android: added a quick thumbnail getting API for video editing.
- Android: fixed the problem of rotation degree settings not working for animated effects.
- Android: fixed occasional lip-sync errors of videos composed from multiple clips and improved the image quality of the composed videos.
- iOS: fixed the thread safety issue caused by frequent switching of background music.
- iOS: fixed the problem of inconsistent background music volume for shooting and preview.
- iOS: fixed the problem of watermark PTS exception towards the end of videos after users add the same special effects multiple times during video editing.

### Version 5.1 Released on August 18, 2018
- iOS & Android: launched multiple editions of the UGSV SDK (Lite, Basic, Enterprise, Enterprise Pro) to cater to the varying needs of clients. Different editions require different licenses.
- iOS & Android: optimized and redesigned beauty filters and added a number of filters.
- iOS & Android: allowed users to swipe to apply different filters during shooting and editing.
- iOS & Android: optimized the duet karaoke feature.
- iOS & Android: added gestures including “press and hold to shoot”, “click to shoot”, and “click to capture” to UGSV apps, added the countdown feature to the karaoke mode, and allowed reverb adding and voice changing during shooting.
- iOS & Android: made UGSV apps available in both Chinese and English.
- iOS & Android: redesigned the main UI of the demo for enhanced clarity and usability.
- Android: allowed quick importing of long videos.
- Android: added a filter intensity setting API for video editing.
- iOS: supported two-pass encoding in video editing to generate videos of higher quality.
- iOS: fixed the problem of high CPU usage when users open the editing page again after apps quit unexpectedly during shooting.
- iOS: fixed the problem of blurry screens during shooting on iOS 12.

### Version 5.0 Released on July 18, 2018
- iOS & Android: supported duet karaoke in dual (left/right) split screens.
- iOS & Android: supported generating videos with two audio tracks in video editing.
- iOS & Android: allowed setting of the audio sampling rate and rendering mode for shooting.
- Android: optimized the image quality of videos generated after shooting and editing and reduced the size of the files generated.
- Android: sped up video pre-processing and generation.
- Android: fixed the problem of black screens during shooting after landscape/portrait mode switch.
-Android: fixed the problem of error reporting when users click to start and end shootings at short intervals.
- iOS: reduced the loading time for video editing.
- iOS: fixed the problem of occasional ripped images in edited videos.
-iOS: fixed the problem of occasional black frames towards the end of an edited video.
-iOS: fixed the problem of audio ending prematurely if users set the playback mode to slow motion when previewing edited videos.
- iOS: made the demo compatible with iPhone X.
- iOS: fixed memory leaks, enhanced stability, and added module definitions to better support Swift integration.

### Version 4.9 Released on June 14, 2018
- Android & iOS: optimized the license integration method and supported auto-renewal.
- Android: incorporated the image-to-video conversion capability and allowed the selection of image transition effects such as pan, zoom, zoom rotation, and fade.
- Android: sped up the generation of UGSV after editing and fixed memory leaks.
- iOS: sped up the loading of local background music and thumbnails, as well as the acquisition of video information.
- iOS: optimized the image quality of post-editing UGSV.
- iOS: fixed problems including occasional stutter and black frames during shooting, occasional flashing of watermarks towards the end of videos, memory leaks, etc.

### Version 4.7 Released on May 25, 2018
- iOS & Android: added filters for UGSV, including blinds, phantom, lightning, mirror, illusion, etc.
- Android: supported texture for custom data.
- Android: reduced peak memory usage during UGSV editing and generation.
- iOS: added the image-to-video conversion capability and allowed the selection of image transition effects such as pan, zoom, zoom rotation, and fade.
- iOS: fixed the problem of callbacks possible only after background music ends.

### Version 4.6 Released on May 4, 2018
- iOS & Android: added reverb effects such as hall and deep vocal, and voice changing effects such as girl and middle-aged man for UGSV shooting.
- iOS & Android: added an external API for setting the directory to save video segments.
-iOS & Android: supported adding background music to videos without audio in UGSV editing.
- iOS & Android: added a split screen API for UGSV composition.
- iOS & Android: lifted the upper limit on bitrate during UGSV shooting.
- Android: optimized the uploading of small files and increased the success rate.
- Android: fixed the crash caused by incorrect path for animated effects.
- iOS: supported Bitcode.

### Version 4.5 Released on April 13, 2018
- iOS & Android: added the demo code of the uploading feature and integrated the SDK with the VOD service so that it provides a comprehensive solution that covers video shooting, special effect adding, uploading, transcoding, porn detection, distribution and playback.
-iOS & Android: supported uploading GIFs to be used as thumbnails and added the video segment splicing feature.
- iOS & Android: added two actions for special effects: removing the background music of animated effects and removing all filters with one click.
- Android: optimized the UGSV production process and fixed problems including playback failure after uploading of large files, occasional black frames in acquired thumbnails, lip-sync errors in some videos, etc.
- Android: allowed users to set the bitrate when editing UGSV.
- Android: allowed the editing of videos without audio.</td>

### Version 4.2
iOS & Android: improved the performance of the Enterprise SDK: enabled image retouching and animated effects, significantly improved video frame rates on iOS, and reduced GPU usage.

### Version 4.1
- iOS & Android: added a bitrate and resolution switching API in UGSV shooting.
- iOS & Android: added a photo taking API in UGSV shooting.
- iOS & Android: allowed users to specify the playback start time and whether to loop playback during UGSV editing.

### Version 3.9
- iOS & Android: added HDR and high-resolution animated stickers.
- iOS & Android: added the AI-based background keying feature.
- iOS & Android: added three speed modifying effects: slow motion, loop, and rewind.
- iOS & Android: added multiple filters, providing users with more options.
- iOS & Android: added multiple animated and static stickers and supported customizing stickers.
- iOS & Android: allowed users to add bubble subtitles to videos.
- iOS & Android: supported shooting videos without audio to make post-shooting editing easier.
- iOS & Android: allowed users to switch between the landscape and portrait modes during shooting.
- iOS & Android: fixed a number of bugs.
- Android: optimized the UGSV uploading process by integrating COS into UGCPublish.

### Version 3.4
- iOS & Android: added actions such as deleting existing video segments, changing aspect ratio, and adjusting focal length in UGSV shooting.
- iOS & Android: supported adding watermarks at the end of videos.
- iOS: fixed the compatibility issue with iOS 11.

### Version 3.3
- iOS & Android: fixed some of the bugs reported by clients last week.
- Android: fixed the problem of green screens during shooting and black screens during playback on some Android devices.

### Version 3.1
- iOS &Android: added features such as face slimming, nose slimming and chin slimming to the Enterprise Edition.
- iOS & Android: optimized the beauty filter algorithm and added multiple filters including rosy complexion.
- Android: added three filters: smooth, natural, and hazy.
- Android: allowed speed modifying, background music adding and subtitle adding in UGSV editing.
- iOS: added two beauty filers: smooth and natural.

### Version 3.0
- iOS & Android: restructured the beauty filter module, enhanced the effects of beauty filters, and reduced GPU usage.
- iOS & Android: added the `pauseRecord` and `resumeRecord` APIs to `TXUGCRecord` to enable multi-segment shooting.
- iOS: added fast clipping and editing APIs.

### Version 2.0.5
- Android: allowed adding watermarks in UGSV editing.
- Android: allowed multi-segment shooting.
- iOS & Android: fixed a number of bugs.

### Version 2.0.4
- iOS & Android: added a pre-processing callback API for beauty filters in UGSV shooting.
- iOS & Android: added the breakpoint resume feature for UGSV uploading.
- Android: optimized the video clipping and splicing features and added the filter editing feature.
- iOS: allowed filter applying, watermarking, background music adding, subtitle adding, and speed modifying in UGSV editing.

### Version 2.0.3
- iOS & Android: optimized the directory and code structure for the demos to reduce the integration cost, and added simple and easy-to-use demos for UGSV shooting, clipping, and splicing.
- Android: added the UGSV cropping and splicing features.
- iOS: fixed the overexposure issue on iOS, enabling more natural exposure.

### Version 2.0.2
- iOS & Android: optimized the UGC uploading protocol.
- Android: added the big eye and face slimming filters to the VIP edition.
- Android: optimized hardware encoding and increased encoding quality.
- iOS: added the UGSV cropping and splicing features.
- iOS: supported Bitcode in the Lite Edition.

### Version 2.0.1
- iOS & Android: allowed adding background music to UGSV.
- Android: added the green screen feature to the VIP edition.

### Version 2.0.0
- iOS & Android: allowed the capturing and publishing of UGSV.


