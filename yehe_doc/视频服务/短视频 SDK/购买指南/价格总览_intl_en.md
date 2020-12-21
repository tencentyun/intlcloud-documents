## Purchase Guide

Before using the UGSV SDK, you need to first activate the VOD service and get a **UGSV SDK license** (one-year license) by purchasing a VOD acceleration resource package:

| VOD Traffic Resource Package Specification | Description |
| ------------------ | ---------------------------- |
| 10 TB | With complimentary UGSV Lite Edition SDK license |
| 50 TB | With complimentary UGSV Basic Edition SDK license |
| 200 TB | With complimentary UGSV Basic Edition SDK license |

> ?  
> - Currently, only the Lite Edition and Basic Edition SDKs can be purchased online.
> - If you need to purchase the Enterprise Edition SDK, please contact your Tencent Cloud rep.

## VOD Service

We recommend you use the UGSV SDK together with Tencent Cloud VOD. This combination is more cost-effective and delivers a better compatibility and user experience. For more information on the billing of VOD, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).



## SDK Features and Corresponding License Editions<span id ="lic"></span>

To use the UGSV SDK, you need a corresponding license. Each SDK edition only requires one license. For more information, please see [License Application](https://intl.cloud.tencent.com/document/product/1069/38041). The details are shown in the table below:

<table>
   <tr>
      <th width="85px" style="text-align:center">Feature Module</td>
      <th width="85px" style="text-align:center">Feature</td>
      <th width="0px" >Description</td>
      <th width="70px" style="text-align:center">Lite Edition License</td>
      <th width="70px" style="text-align:center">Basic Edition License</td>
      <th width="70px" style="text-align:center">Enterprise Edition License</td>
      <th width="92px" style="text-align:center">Enterprise Pro Edition License</td>
   </tr>
   <tr>
      <td>UI</td>
      <td>Custom UI</td>
	    <td>The UI can be customized. The UGSV application provides a complete set of source code for UI interaction, which can be reused or customized</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
	    <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td rowspan='18'>Capturing and shoot</td>
      <td>Aspect ratio</td>
      <td>Video shoot supports multiple aspect ratios, including 16:9, 4:3, and 1:1</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
	    <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Definition</td>
      <td>SD, HD, and FHD are supported for shoot, and the bitrate, frame rate, and GOP can be customized</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
	    <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Shoot control</td>
      <td>The front/rear cameras can be switched and the flash can be controlled during shoot</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
	    <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
	 <tr>
	    <td>Duration configuration</td>
      <td>The minimum and maximum shoot durations can be customized</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
	    <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
	 <tr>
      <td>Watermarking</td>
      <td>Watermarks can be added during shoot</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
	    <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Focal length</td>
      <td>The focal length can be adjusted during shoot</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
	    <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Focus mode</td>
      <td>Manual focus and autofocus are supported</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Multi-segment shoot</td>
      <td>You can pause shoot to segment the video and delete existing segments</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Capturing</td>
      <td>Photos can be captured</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Adjustable-speed shoot</td>
      <td>Slow and fast shoot modes are supported</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Background music</td>
      <td>A local .mp3 file can be selected as the background music before shoot</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Voice changing and reverb</td>
      <td>The voice to be recorded can be changed to another type (such as the voice of a little girl or middle-aged man) and mixed with reverb effects (such as karaoke room and hall) before shoot</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Filters</td>
      <td>Filters can be switched by swipe and previewed in real time. The filter and filter level can be customized</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr><tr>
      <td>Basic beauty filters</td>
      <td>The skin smoothing, skin brightening, and rosy skin filters can be configured for shoot, and their effect levels can be adjusted</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Advanced beauty filters</td>
      <td>The eye enlarging, face slimming, chin slimming, chin adjustment, face shortening, and nose narrowing filters can be set for shoot, and their effect levels can be adjusted</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Animated stickers</td>
      <td>Faces can be detected, and effects such as face reshaping, stickers, and pendants can be added</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>AI-based keying</td>
      <td>A person's contour can be recognized, and the background can be removed and replaced with another element, such as animated background or PowerPoint slide</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Green screen keying</td>
      <td>Elements in green (such as pure green background) in the video image can be removed and replaced with another element such as animated background or PowerPoint slide</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
   </tr><tr>
      <td rowspan='12'>Special effects and editing</td>
      <td>Quick import</td>
      <td>Videos can be quickly imported on Android</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Video clipping</td>
      <td>Videos can be precisely clipped according to the specified time range</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Bitrate configuration</td>
      <td>The bitrate can be specified for video generation</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Cover generation</td>
      <td>The frame image at the specified time point can be obtained</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Preview by frame</td>
      <td>When the base cursor is slid along the timeline, the frame image where the cursor stays will be displayed in the preview window</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Filters</td>
      <td>Filters can be added for videos, and the filter level can be adjusted</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Time-base special effects</td>
      <td>Time-based special effects such as reverse, loop, and slow motion can be added for videos</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Special effect filters</td>
      <td>Special effects such as soul out, dynamic light-wave, cracked screen, and darkness and phantom can be added for videos</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Background music</td>
      <td>An embedded audio file or local .mp3 file in the phone can be used as the background music. The background music can be clipped, and the volume level can be adjusted</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Animated or static stickers</td>
      <td>Animated or static stickers can be added. Their positions in the video image and the start and end points in time for display are customizable</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Subtitles</td>
      <td>Subtitles can be added, and the style of the subtitles frame background (such as bubble) can be selected. Their positions in the video image and the start and end points in time for display are customizable</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Image transition</td>
      <td>Multiple images can be imported, and transition effects such as rotation, fade-in, and fade-out can be selected for video generation</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td rowspan='2'>Video splicing</td>
      <td>Multi-video splicing</td>
      <td>Multiple videos can be spliced into one video</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td>Co-shoot</td>
      <td>A video can be shot when another video is played back to generate a dual-image video</td>
      <td style="text-align:center">×</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr> <tr>
      <td rowspan='1'>Video upload</td>
      <td>Upload to VOD</td>
      <td>VOD supports features such as media asset management and content audit</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr><tr>
      <td rowspan='1'>VOD playback</td>
      <td>Superplayer</td>
      <td>A one-stop solution implemented based on the VOD player is provided, which has features such as video information pull, portrait/landscape mode switch, definition selection, on-screen commenting, and LVB time shifting and is completely open-source</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
      <td style="text-align:center">&#10003;</td>
   </tr>
   <tr>
      <td rowspan='2'>SDK download</td>
      <td>Android</td>
	  <td>UGSV SDK (LiteAVSDK) + basic feature demo source code</td>
      <td colspan="2" style="text-align:center"> <a onclick=MtaH5.clickStat("ugc_sdk_download_android_basic") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/5.4/LiteAVSDK_UGC_Android_5.4.6097.zip">Download the Basic Edition SDK</a> </td>
      <td colspan="2" style="text-align:center"> <a onclick=MtaH5.clickStat("ugc_sdk_download_android_enterprise") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/5.4/LiteAVSDK_Enterprise_Android_5.4.6097.zip">Download the Enterprise Edition SDK</a> </td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>UGSV SDK (LiteAVSDK) + basic feature demo source code</td>
      <td colspan="2" style="text-align:center"> <a onclick=MtaH5.clickStat("ugc_sdk_download_ios_basic") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/5.4/TXLiteAVSDK_UGC_iOS_5.4.6097.zip">Download the Basic Edition SDK</a> </td>
      <td colspan="2" style="text-align:center"> <a onclick=MtaH5.clickStat("ugc_sdk_download_ios_enterprise_smart") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/5.4/TXLiteAVSDK_Enterprise_iOS_5.4.6097.zip">Download the Enterprise Edition SDK</a> </td>
   </tr><tr>
      <td rowspan='2'>License</td>
      <td>License application</td>
      <td>An SDK edition can be used only with its corresponding license</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/1069/38041#.E8.B4.AD.E4.B9.B0.E6.AD.A3.E5.BC.8F.E7.89.88-license">Lite Edition license</a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/1069/38041#.E8.B4.AD.E4.B9.B0.E6.AD.A3.E5.BC.8F.E7.89.88-license">Basic Edition license</a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/1069/38041#.E5.85.B3.E4.BA.8E.E4.BC.81.E4.B8.9A.E7.89.88.E6.9C.AC-license">Enterprise Edition license</a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/1069/38041#.E5.85.B3.E4.BA.8E.E4.BC.81.E4.B8.9A.E7.89.88.E6.9C.AC-license">Enterprise Pro Edition license</a></td>
   </tr>
</table>


## Beauty Filter and Animated Effect Materials<span id="p1"></span>

The Enterprise Edition SDK has advanced features such as beauty filter, AI animated effect, and green screen keying. If you need to use makeup effects, gestures, and additional animated stickers, please purchase additional materials:

| Material Type | Description |
| -------- | -------------------------------------------- |
| Animated sticker| Faces can be detected, and effects such as stickers and pendants can be added |
| AI-based keying | A person's contour can be recognized, and the background can be removed and replaced with another element |
| Makeup effect | Trendy makeup effects can be quickly added for natural beautification |
| Gesture effect | Faces and gestures can be recognized to trigger specified animated effects for interaction |

#### Billing description

- Beauty filter and animated effect materials need to be used in conjunction with a UGSV Enterprise Pro Edition license. **UGSV Lite, Basic, and Enterprise Edition licenses do not support material purchase.**
- One UGSV Enterprise Edition license comes with 10 complimentary designated animated stickers. One UGSV Enterprise Pro Edition license comes with 20 complimentary animated stickers or AI-based keying materials (valid for one year). If needed, please [contact sales](https://cloud.tencent.com/apply/p/h1qsz5vhvko) for application. Makeup and gesture effects need to be purchased separately.
- **Materials are valid for one year after purchase. After you renew a license, you can continue to use the complimentary materials. If you need additional materials, you should purchase another license.**
- For more information on how to use materials, please see [Eye Enlarging, Face Slimming, and Pendants (iOS)](https://intl.cloud.tencent.com/document/product/1069/38030) and [Eye Enlarging, Face Slimming, and Pendants (Android)](https://intl.cloud.tencent.com/document/product/1069/38031).
- **The purchased materials can only be used under the license used to purchase them. Any form of material exchange is prohibited, including but not limited to gifting, resale, and renting. Tencent Cloud reserves all legal rights to hold violators accountable.**
- **For purchase, please contact sales.**

<script>
    var _mtac = {"senseHash":0};
    (function() {
      var mta = document.createElement("script");
      mta.src = "//pingjs.qq.com/h5/stats.js";
      mta.setAttribute("name", "MTAH5");
      mta.setAttribute("sid", "500538821");
      mta.setAttribute("cid", "500538834");
      var s = document.getElementsByTagName("script")[0];
      s.parentNode.insertBefore(mta, s);
    })();
</script>
