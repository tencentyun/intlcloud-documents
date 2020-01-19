### What are the purposes of "HTML" and "IFRAME" displayed in "Web Player Code Generation" in "Media Assets"?

"HTML" and "IFRAME" are ways to release custom code for the following purposes:

**HTML** is HTML code used to embed a video player in a webpage, so that the player will be displayed for video playback when a user browses the webpage. The code may require minor modifications for customization and thus is suitable for those who have some knowledge of the HTML programming language. The code can be automatically adapted to mobile devices and PCs and also supports web SDK features for highly flexible secondary development. For more information, please see [Development Guide for Web SDK](http://video.qcloud.com/download/docs/QVOD_Player_Web_SDK_Developer_Guide.pdf).

**IFRAME** makes it easy for you to release your player code directly without any modification. You do not need to know the content of the code; instead, you just need to copy and paste the code in the corresponding place in the HTML page. The IFRAME tag is highly compatible with mainstream browsers such as Chrome, IE, Safari, and Firefox.
 
>If the user visits the webpage from an iOS or Android mobile device, only HTML5 will be used for playback; if from a PC, Flash will be used preferentially; if the browser does not support Flash, HTML5 will be used; and if HTML5 is not supported, the player will directly display a prompt to download a newer browser.

### Does a web player support dynamic watermarking?

No for the time being. After this feature is available, you can upload the viewer's ID through an API and make it dynamically and randomly appear in the video for the purpose of video content protection.


### Does the web player code support mobile devices?

The web player code supports playback on various types of mobile devices.

### Does a web player support rolling?

Currently, a roll image can be added at the beginning of a video.

### What is the relationship between a web player and a video file? How many web players can be created?

A web player contains the playback parameter settings for a video file when it is played back by using the web player code, such as player appearance and roll. For video files that are not played back by using a web player (such as by directly accessing a URL in a browser, or using a third-party or proprietary player instead), the player parameter settings on the management page will not take effect.

Currently, a maximum of 10 web players can be created.


### Can I customize the appearance of a player?

Currently, you can customize the logo and player size on the management page, and you can also set the iOS or Android player size through SDKs.



### What is the difference between a watermark and a logo?

A watermark is a fixed logo completely embedded in a video file during the transcoding process. Once the transcoding is completed, it cannot be canceled.
A logo is a display icon added onto a player during video playback. It can be moved or canceled at any time.

