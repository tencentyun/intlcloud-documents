
## Overview

This document shows you how to encrypt videos using DRM solutions and use your own player or a third-party player to play the encrypted videos.

>? We expect to add support for DRM in our superplayer SDK (Android, iOS, and web) in mid-May.

## Prerequisites
Before you start, do the following:

### Activate VOD
Follow the steps below to activate VOD:

1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Purchase VOD services. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).
3. Go to the [VOD console](https://console.cloud.tencent.com/vod).

At this point, you have activated VOD. 

### Apply for a FairPlay certificate and submit the certificate information
For detailed directions, see [Applying for FairPlay Certificate and Submitting Certificate Information](https://intl.cloud.tencent.com/document/product/266/46643). After submitting the information, view and note the certificate URL in the console for later use.

## Step 1. Enable hotlink protection

The example below shows how to enable key hotlink protection for the default distribution domain under your account:
>? We do not recommend enabling hotlink protection for a domain name already in use, because it may result in playback failure.

1. Log in to the VOD console, select **Distribution and Playback** > **[Domain Name](https://console.cloud.tencent.com/vod/distribute-play/domain)**, find the default distribution domain, and click **Set** on the right.
2. Click **Access Control** and toggle **Key Hotlink Protection** on. In the pop-up window, click **Generate** to generate a random key (2WExxx48eW). Copy the key, which is needed to generate superplayer signature, and click **Confirm** to save the configuration.

## Step 2. Encrypt a video

1. In the VOD console, select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**, select the target video (file ID: 528xxx3757278095), and click **Process Video**.
2. On the video processing page:
 - Select **Task Flow** as the **Processing Type**.
 - Select **WidevineFairPlayPreset** as the **Task Flow Template**.
 
>?
>- `WidevineFairPlayPreset` is a preset task flow. It uses the adaptive bitrate streaming template 11 or 13, the time point screenshot template 10 (for thumbnail generation), and the image sprite template 10.
>- The adaptive bitrate streaming template 11 generates multi-bitrate streams encrypted by FairPlay, and the adaptive bitrate streaming template 13 generates multi-bitrate streams encrypted by Widevine.
3. Click **Confirm** and wait until the **Video Status** changes from "Processing" to "Normal", which indicates that video processing is completed.
4. Click **Manage** in the **Operation** column of the video to enter the management page:
 - Click the **Basic Info** tab to view the generated thumbnail and outputs of adaptive bitrate streaming (template ID: 11/13).
 - Click the **Screenshot Info** tab to view the generated image sprite (template ID: 10).


## Step 3. Get the playback information

The superplayer SDK does not yet support the playback of DRM-encrypted videos. To get the playback information, you can refer to the communication protocol between the superplayer SDK and the VOD backend. Once you have the information, you can use your own player or a third-party player to play the encrypted video.

### Communication protocol
The HTTP GET request method is used, and the URL is `https://{domain}/{interface}/{version}/{appId}/{fileId}?psign={psign}`.

#### Domain names
- Primary domain name: `playvideo.qcloud.com`
- Secondary domain name: `bkplayvideo.qcloud.com`

#### Request fields
##### Path fields

| Field  | Required | Value                                                     |
| --------- | -------- | ------------------------------------------------------------ |
| appId     | Yes       | The application ID (If you use a subapplication, pass in the [subapplication ID](https://intl.cloud.tencent.com/document/product/266/33987)). |
| fileId    | Yes       | The ID of the video file to play.                                        |
| version   | Yes       | Pass in `v4`.                                                |
| interface | Yes       | Pass in `getplayinfo`.                                       |

##### Query string fields

| Field  | Required | Value                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| psign    | No       | The superplayer signature. For how to generate it, see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099). In `PayLoad` of the signature, set `pcfg` to `advanceDrmPreset`. We also offer a quick [superplayer signature generation tool](https://vods.cloud.tencent.com/signature/super-player-sign.html). |
| context  | No       | The pass-through field, which is returned as it is in the response.                                   |

#### Response fields

| Field | Type | Description |
| -- | -- | -- |
| code | Integer | The error code. A value other than 0 indicates an error. |
| message | String | The error message, which is not empty if `code` is not 0. |
| version | Integer | The version type of the returned result, which is 4. |
| warning | String | The warning message. If the `psign` parameter is carried but hotlink protection is not enabled, a warning will be returned. |
| media | Object | The media information (type: `Media`). |

##### Media

| Field | Type | Description |
| -- | -- | -- |
| basicInfo | Object | The basic video information (type: `BasicInfo`). |
| streamingInfo | Object | The multi-bitrate encoding information (type: `StreamingInfo`). |
| imageSpriteInfo | Object | The image sprite information (type: `ImageSpriteInfo`), which is used for preview. |
| keyFrameDescInfo | Object | The timestamp information (type: `KeyFrameDescInfo`), which is used to add timestamps to the video. |

##### BasicInfo

| Field | Type | Description |
| -- | -- | -- |
| name | String | The video name. |
| size | Integer | The video size in bytes. |
| duration | Float | The video duration in seconds. |
| description | String | The video description. |
| coverUrl | String | The thumbnail URL. |

##### StreamingInfo

| Field | Type | Description |
| -- | -- | -- |
|drmOutput|Array| DRM-encrypted outputs (type: `StreamingOutput`). |
|drmToken|String|The DRM token used for encryption. |
|widevineLicenseUrl|String|The license URL for Widevine encryption. |
|fairplayLicenseUrl|String|The license URL for FairPlay encryption. |

##### StreamingOutput

| Field | Type | Description |
| -- | -- | -- |
| type | String | The encryption type for adaptive bitrate streaming. Valid values: `plain` (no encryption), `SimpleAES` (HLS encryption), `FairPlay` (DRM encryption), `Widevine` (DRM encryption). |
| url | String | The playback URL. |
| subStreams | Array | The information of output streams (type: `SubStreamInfo`). |

##### SubStreamInfo

| Field | Type | Description |
| -- | -- | -- |
| type | String | The stream type. Valid value: `video`. |
| width | Integer | The video width in pixels. |
| height | Integer | The video height in pixels. |
| resolutionName | String | The name of the stream shown in the player. |

##### ImageSpriteInfo

| Field | Type | Description |
| -- | -- | -- |
| imageUrls | Array | An array of the image sprite download URLs (type: `String`). |
| webVttUrl | String | The download URL of the image sprite VTT file. |

##### Sample

##### Sample request

The payload of the superplayer signature is as follows:

```json
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546340400,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

Suppose the key is `test`. The superplayer signature generated is as follows:

```json
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.aqH576UXfeUe90LlH6w1tt-N1UYrEoOtAYb1ljUT51M
```

The request URL is as follows:

```
https://playvideo.qcloud.com/getplayinfo/v4/1255566655/4564972818519602447?psign=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.s01u7fpYu0VkLBHG5e84JCgfnFGxRvrNHWQRCHWHhc0
```

##### Sample response

```json
{
  "code": 0,
  "message": "",
  "requestId": "87cc5b712d7c402c8bb255b3777f8bf5",
  "version": 4,
  "context": "",
  "warning": "",
  "media":{
    "basicInfo":{
      "name": "drm demo",
      "size": 428106411,
      "duration": 90,
      "coverUrl": "https://xxx.vod2.myqcloud.com/xxx/xxx/coverBySnapshot/coverBySnapshot_10_0.jpg?t=7fffffff&sign=ea3197f995dae16457397d9a3c0ebc1c",
      "description": ""
    },
    "streamingInfo":{
      "drmOutput":[
        {
          "type": "Widevine",
          "url": "https://1500012293.vod2.myqcloud.com/xxx/xxx/adp.13.m3u8?t=7fffffff&sign=75152a4b4d10f32f4315783edf9944ed",
          "subStreams":[
            {
              "type": "video",
              "width": 426,
              "height": 240,
              "resolutionName": "FLU"
            },
            {
              "type": "video",
              "width": 852,
              "height": 480,
              "resolutionName": "SD"
            },
            {
              "type": "video",
              "width": 1280,
              "height": 720,
              "resolutionName": "HD"
            },
            {
              "type": "video",
              "width": 1920,
              "height": 1080,
              "resolutionName": "FHD"
            }
          ]
        },
        {
          "type": "FairPlay",
          "url": "https://1500012293.vod2.myqcloud.com/xxx/xxx/adp.11.m3u8?t=7fffffff&sign=75152a4b4d10f32f4315783edf9944ed",
          "subStreams":[
            {
              "type": "video",
              "width": 426,
              "height": 240,
              "resolutionName": "FLU"
            },
            {
              "type": "video",
              "width": 852,
              "height": 480,
              "resolutionName": "SD"
            },
            {
              "type": "video",
              "width": 1280,
              "height": 720,
              "resolutionName": "HD"
            },
            {
              "type": "video",
              "width": 1920,
              "height": 1080,
              "resolutionName": "FHD"
            }
          ]
        }
      ],
      "drmToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE2NTA1NDM3ODUsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywicmFuZG9tIjo0NzUyNDQzMTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~ebaFyERTuT8QMMN5iQ-lnVLs60LCUt1J_RmADdRiE_8",
      "widevineLicenseUrl": "https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2",
      "fairplayLicenseUrl": "https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2"
    },
    "audioVideoType": "AdaptiveDynamicStream",
    "originalInfo": null,
    "transcodeInfo": null
  }
}
```
#### Playback information

From the above response, you can get the following playback information:

1. The URL of the DRM-encrypted video.

2. The license server URL for FairPlay/Widevine encryption, which is spliced using `drmToken` and `widevineLicenseUrl`/`fairplayLicenseUrl`.

Below is the playback information obtained from the above sample:

Widevine encryption:

- URL of the encrypted video: `https://1500012293.vod2.myqcloud.com/xxx/xxx/adp.13.m3u8?t=7fffffff&sign=75152a4b4d10f32f4315783edf9944ed`
- License server URL: `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE2NTA1NDM3ODUsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywicmFuZG9tIjo0NzUyNDQzMTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~ebaFyERTuT8QMMN5iQ-lnVLs60LCUt1J_RmADdRiE_8`

FairPlay encryption:

- URL of the encrypted video: `https://1500012293.vod2.myqcloud.com/xxx/xxx/adp.11.m3u8?t=7fffffff&sign=75152a4b4d10f32f4315783edf9944ed`
- License server URL: `https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE2NTA1NDM3ODUsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywicmFuZG9tIjo0NzUyNDQzMTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~ebaFyERTuT8QMMN5iQ-lnVLs60LCUt1J_RmADdRiE_8`


## Step 4. Play the DRM-encrypted video

### Solution 1: Playing in the VOD superplayer
The VOD superplayer can play DRM-encrypted videos. See below for detailed directions:


#### Step 1. Import files
Import the player style file and script file into the page.

```
 <link href="//imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.css" rel="stylesheet">
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/libs/hls.min.0.12.4.js"></script>
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/libs/dash.all.min.2.9.3.js"></script>
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.min.js"></script>
```

#### Step 2. Add a player container
Add a player container where you want to play videos. For example, you can add the following code to `index.html` (the container ID, width, and height are customizable).

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

#### Step 3. Add initialization code
Add the following script to your page initialization code and pass in the required initialization parameters.

```
var player = TCPlayer('player-container-id', {
  appID:  '', // The application ID of your VOD account, required.
  fileID: '', // The file ID of the video to play, required.
  psign: '', // Player signature.
  plugins: {
    DRM: {
      certificateUri: '', // FairPlay certificate URL, which is required if FairPlay-encrypted videos are played.
    }
  }``
});
```


>?
>- You need to pass in the FairPlay certificate as well to play FairPlay-encrypted videos.
>- `certificateUri` is the URL of the certificate required to play FairPlay-encrypted videos. You can get the URL of a certificate after it is generated and deployed to your server.
>- Content encrypted using established DRM solutions can only be played on HTTPS pages.


### Solution 2: Playing in a third-party player (Shaka Player)  

To play DRM-encrypted videos in a third-party player, you need to send a request to the VOD backend for the encryption information and then pass in the information when the player is initialized. For details, see [Shaka Player](https://github.com/shaka-project/shaka-player).


#### Step 1. Import files
Import the player script file into the page via [npm](https://www.npmjs.com/package/shaka-player) or CDN.

```
// CDN: 
<script src="path/to/shaka-player.compiled.js" ></script>
```

#### Step 2. Add a player container
Add a player container where you want to play videos. For example, you can add the following code to `index.html` (the container ID, width, and height are customizable).

```
  <video id="video" width="640" controls autoplay></video>
```

#### Step 3. Add initialization code
Add the following script to your page initialization code and pass in the required initialization parameters.

```
var manifestUri = 'https://1500003943.vod2.myqcloud.com/43832a63vodtranscq1500003943/06981c16387702298107746523/adp.1368258.m3u8';

function initPlayer() {
	// Create a player instance.
	var video = document.getElementById('video');
	var player = new shaka.Player(video);

	player.configure({
	    drm: {
	      servers: {
	        'com.widevine.alpha': 'https://drm.vod2.myqcloud.com/getlicense/v1?drmType=Widevine&token=bJ%2FE5%2Bmc5atzwHKci%2Fh2IPDoON9TZWNyZXRJZD1BS0lETmNmcnZwVURrQTNxVzVoNVJ0SWV2RlVoRXdjQ21FaDUmQ3VycmVudFRpbWVTdGFtcD0xNjQ4MTk2NzU5JkV4cGlyZVRpbWVTdGFtcD0yNjQ4MTk2NzU5JlJhbmRvbT0yMDIzOTEyOTMxJkZpbGVJZD0zODc3MDIyOTgxMDc3NDY1MjMmVm9kU3ViQXBwSWQ9MTUwMDAwMzk0Mw%3D%3D',
	      }
	    }
	});
	 	
	try {
		player.load(manifestUri);
		// This runs if the asynchronous load is successful.
		console.log('The video has now been loaded!');
	} catch (e) {
		// onError is executed if the asynchronous load fails.
	}	

}
        
initPlayer();


```

## Summary

Now, you have learned how to encrypt videos using DRM solutions and play the encrypted videos in a player.