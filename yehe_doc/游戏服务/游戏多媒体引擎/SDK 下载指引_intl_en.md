This document describes how to download the SDKs for Tencent Cloud GME.

## Release History

Check the [Product Updates](https://intl.cloud.tencent.com/document/product/607/35323) first before downloading the SDK.

## Getting Started

If it is your first time to use the SDK, please refer to [User Tutorial](https://intl.cloud.tencent.com/document/product/607/39696).

## Guide for Sample Project

### Sample Project usage

For any problems encountered when using the downloaded SDK or Demo, please see [Demo Usage](https://intl.cloud.tencent.com/document/product/607/39521), or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

> ?To compile and run the downloaded demo, you need to replace relevant strings with the SDK AppID and key you have applied for. For example, the code file **UserConfig.cs** needs modification for using the Unity demo. For more information on the service application, please see [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/10782).

### Sample Project debugging

You can refer to the following documents when performing debugging.

- For issues of room entering failure, see [Room Entering Failed](https://intl.cloud.tencent.com/document/product/607/39523).
- For issues of no sound, see [Sound and Audio Problems](https://intl.cloud.tencent.com/document/product/607/39524).
- For service calling errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).
- If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.



### Demo export

For any problems encountered when exporting the demo as an executable file, please see [Program Export](https://intl.cloud.tencent.com/document/product/607/39522).



## Version Updates

The v2.9.6 is updated as follows:

<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
 <th width="15%">Release Date</th>  
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>SDK v2.9.6 is released</td>
<td ><ul style="margin:0;">
<li >Added role setting feature for Voice Chat, increasing support for wargame, SLG games.</li>
<li >Two accompaniment streams now can be played simultaneously.</li>
<li >Supported setting the progress of accompaniment when using an online MP3 file as an accompaniment.</li>
<li >Language detection results can be returned in the text translation feature.</li>
<li >Translation is supported for Speech-to-Text APIs.</li>
<li >Added the API for inputting the local 3D location for better adaption to VR scenarios.</li>
<li >Added the API for 3D voice blocklist, which is used to eliminate 3D sound effects of other gamer’s voice.</li>
<li >Optimized 3D voice feature. With 3D audio models built into the SDK, developers don’t need to call <li >APIs to pass in model path. </li>
<li >The GME SDK supports Unity WebGL, Xbox gamescore and Unreal Engine 5.</li>
<li >The GME SDK is compatible with the latest version of PlayStation 5.</li>
<li >The GME SDK for macOS supports M1 ARM64.</li>
<li >The GME SDK is compatible with the Bluetooth permission of Android 12.</li>
<li >Fixed compatibility issues on Android 5.1.</li>
<li >Fixed memory issue caused by looping voice messages.</li>
<li >Memory consumption by the SDK is reduced.</li>
<li >Optimized the startup time of hardware devices to shorten the room entry time.</li>
</ul ></td>
<td>2023-01-18</td> 
<td><li ><a href="https://www.tencentcloud.com/zh/document/product/607/18218">3D Sound Effect</a></li>
<li ><a href="https://www.tencentcloud.com/zh/document/product/607/51114">Commanding
</a></li>
</tr>
</tbody></table>



<dx-alert infotype="notice" title="Note on Updates">
To upgrade to v2.9.x, see [SDK Version Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/32363).
</dx-alert>



## SDK v2.9.6 GA Download

| OS/Engine | Update Time | SDK Download | Sample Project Download | Documents |
| ------------- | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Unity         | January 18, 2023 | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unity_Audio_SDK_2.9.6.09d06620.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unity_Audio_Demo_2.9.6.09d06620.zip) | [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544) |
| Unreal Engine 4.x| January 18, 2023| [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal422_Audio_SDK_2.9.6.09d06620.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal422_Audio_Demo_2.9.6.09d06620.zip) | [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545) |
| Unreal Engine 5.x| January 18, 2023| [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal5_Audio_SDK_2.9.6.97b107ed.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal5_Audio_Demo_2.9.6.97b107ed.zip) | [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545) |
| Cocos2D       | January 18, 2023 | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Cocos_Audio_SDK_2.9.6.09d06620.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Cocos_Audio_Demo_2.9.6.09d06620.zip)| [Getting Started](https://intl.cloud.tencent.com/document/product/607/18292) |
| Windows       | January 18, 2023 | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Windows/GME_Windows_audio_sdk_2.9.6.92a797e4.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Windows/GME_Windows_audio_example_project_2.9.6.92a797e4.zip) | [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858) |
| iOS           | January 18, 2023| [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/iOS/GME_ios_audio_sdk_2.9.6.92a797e4.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/iOS/GME_ios_audio_example_2.9.6.92a797e4.zip) | [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858) |
| Android       | January 18, 2023 | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Android/GME_android_audio_sdk_2.9.6.92a797e4.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Android/GME_android_audio_example_2.9.6.92a797e4.zip) | [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858) |
| macOS         | January 18, 2023| [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Mac/GME_mac_audio_sdk_2.9.6.92a797e4.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Mac/GME_mac_audio_demo_2.9.6.92a797e4.zip) | [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858) |
| Web       | 2022-06-20 | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/H5/intl/GME_intl_Web_SDK_2.8.1.53.zip) | [Download](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/H5/intl/GME_intl_Web_Demo_2.8.1.53.zip) 

> ?
>
> - GME SDK also supports game consoles (PlayStation, Xbox and Nintendo Switch). [Submit a ticket](https://console.cloud.tencent.com/workorder/category) if needed.
> - For SDK compilation toolchains on all platforms, see [Toolchain](https://intl.cloud.tencent.com/document/product/607/46711).
> - Currently, only the ITMG_ROOM_TYPE_FLUENCY audio quality type is provided by default. To use other audio quality types, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

