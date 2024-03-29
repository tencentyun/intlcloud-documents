## Feature Description
- You can specify the expiration time in a video URL to prevent malicious users from transferring the URL to other websites for long-term unauthorized viewing.
- You can specify the maximum number of IPs allowed to playback a video from a URL to prevent malicious users from distributing the video to a large number of viewers.
- You can specify the preview duration in a video URL to implement a video preview.
- You can use a key (`KEY`) to create a signature and put it into a video URL. As long as the key is not disclosed, the video URL cannot be forged.
- A CDN node controls video playback requests by checking the parameters and signature in the video URL. If a request fails to pass the check, a 403 response code will be returned.
- Supported file formats include MP4, TS, M3U8, FLV, AAC, MOV, WMV, AVI, MP3, RMVB, MKV, MPG, 3GP, WEBM, M4V, ASF, F4V, WAV, MPEG, VOB, RM, WMA, DAT, M4A, MPD, and M4S.

>?For more information on how to enable key hotlink protection, see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/14060).

## Generating a Hotlink Protection URL
- All your videos in VOD have an **original video URL**. If hotlink protection is not enabled, the original video URL can be used to play back the video.
- After key hotlink protection is enabled, the original video URL can no longer be used for video playback, and a **hotlink protection URL** of the video needs to be generated.

You can generate a hotlink protection URL for a video by adding the hotlink protection parameters at the end of the original URL in the form of `QueryString`, such as:
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=[t]&exper=[exper]&rlimit=[rlimit]&us=[us]&sign=[sign]
```
Below are descriptions and values of the parameters in a hotlink protection URL.

#### Hotlink protection parameters
| Parameter Name | Required | Description |
| ------ | ---- | ------------------------------------------------------------ |
| `KEY` | Yes | The key entered when key hotlink protection is enabled. It must contain 8–20 letters (a–Z) or digits (0–9). We recommend you click **Generate KEY** in the console to generate a key. For detailed directions, see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/14060). |
| `Dir` | Yes | The remaining part of the path in an original video URL after the filename is removed. For example, if the original URL is `http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4`, then the playback path is `/dir1/dir2/`. |
| `t` | Yes | <li>The expiration timestamp of a playback address in the form of hexadecimal lowercase Unix time. <br><li>Once expired, the URL will become invalid, and a 403 error will be returned. Due to possible time difference between servers, the actual expiration time of a hotlink protection URL is generally 5 minutes longer than the specified expiration time, that is, an additional 300-second tolerance time is allowed. <br><li>The expiration timestamp should be large enough for full video playback to complete. |
| `exper` | No | <li>The preview duration in decimal seconds. If this parameter is left empty or 0, preview mode is disabled (i.e., the complete video will be returned). <br><li>The preview duration must be shorter than the original video duration; otherwise, playback may fail. |
| `rlimit` | No | <li>The maximum decimal number of device IPs allowed for playback. The maximum value is 9. If this parameter is left empty, there is no restriction. <br><li>When you restrict a video URL to be played back by only one user, we recommend you do not set `rlimit` to 1 (instead, set it to 3, for example), as a mobile device's IP may change if a reconnection occurs. |
| `us` | No | <li>The link ID. It is used to randomize a hotlink protection URL in order to improve the uniqueness of the link. <br><li>We recommend you specify a random `us` value when generating a hotlink protection URL each time. |
| `sign` | Yes | <li>The hotlink protection signature. It is a hexadecimal number with a length of 32 characters and used to check the validity of a hotlink protection URL. <br><li>A 403 error will be returned if a URL fails to pass the signature check. Below is the [signature calculation formula](#formula). |


#### [](id:formula)Signature calculation formula
```
sign = md5(KEY + Dir + t + exper + rlimit + us)
```

`+` in the formula is used to concatenate two strings. Optional parameters can be empty strings.

## Examples of Hotlink Protection URL Generation
Assume that you have a video in VOD and its original playback URL is `http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4`. You have enabled key hotlink protection. The generated key is `24FEQmTzro4V5u3D5epW`, and the generated random string is `72d4cd1101`, and now you want to:
1. Generate a hotlink protection URL for this video and set the expiration time of the URL to 20:00 on January 31, 2018 (1517400000 in Unix time).
2. Generate a preview URL and set the preview duration to the first five minutes of the video (the original video duration is longer than five minutes).
3. Allow up to 3 devices with different IPs to play back the video at the URL.

The following describes how to generate hotlink protection URLs for three different example scenarios.

### Example 1. Validity period control of a video playback address
#### Step 1. Determine the hotlink protection parameters

| Parameter | Value | Description |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | The key you selected when enabling key hotlink protection. |
| `Dir` | `/dir1/dir2/` | The remaining part of the path in the original video URL after `myVideo.mp4` is removed. |
| `t`      | `5a71afc0`             | Hexadecimal result of the expiration timestamp `1517400000`.          |
| `us`     | `72d4cd1101`           | The generated random string.                                   |


#### Step 2. Calculate a signature

```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc072d4cd1101") = "3d8488faeb37d52d6bf63b63c1b171c3"
```

#### Step 3. Generate a hotlink protection URL
Concatenate the hotlink protection parameters into the `QueryString` of the original video URL to generate the hotlink protection URL of the video:
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&us=72d4cd1101&sign=3d8488faeb37d52d6bf63b63c1b171c3
```

### Example 2. Maximum number of IPs allowed for playback at a playback address
#### Step 1. Determine the hotlink protection parameters

| Parameter | Value | Description |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | The key you selected when enabling key hotlink protection. |
| `Dir` | `/dir1/dir2/` | The remaining part of the path in the original video URL after `myVideo.mp4` is removed. |
| `t`      | `5a71afc0`             | Hexadecimal result of the expiration timestamp `1517400000`.          |
| `rlimit` | `3`                    | Allow up to 3 different IPs to play back the video at the URL.                   |
| `us`     | `72d4cd1101`           | The generated random string.                                   |

#### Step 2. Calculate a signature
```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc0372d4cd1101") = "c5214f0d5961b13acd558b4957c4dfc5"
```

#### Step 3. Generate a hotlink protection URL
Concatenate the hotlink protection parameters into the `QueryString` of the original video URL to generate the hotlink protection URL of the video:
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&rlimit=3&us=72d4cd1101&sign=c5214f0d5961b13acd558b4957c4dfc5
```

### Example 3. Allowed video playback duration control
#### Step 1. Determine the hotlink protection parameters

| Parameter | Value | Description |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | The key you selected when enabling key hotlink protection. |
| `Dir` | `/dir1/dir2/` | The remaining part of the path in the original video URL after `myVideo.mp4` is removed. |
| `t`      | `5a71afc0`             | Hexadecimal result of the expiration timestamp `1517400000`.          |
| `exper`  | `300`                  | Preview the first 5 minutes (i.e., 300 seconds).                                 |
| `us`     | `72d4cd1101`           | The generated random string.                                   |

#### Step 2. Calculate a signature

```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc030072d4cd1101") = "547d98c4b91e81b5ea55c95cef63223f"
```

#### Step 3. Generate a hotlink protection URL
Concatenate the hotlink protection parameters into the `QueryString` of the original video URL to generate the hotlink protection URL of the video:
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&exper=300&us=72d4cd1101&sign=547d98c4b91e81b5ea55c95cef63223f
```

## Key Hotlink Protection URL Generator and Checker
VOD provides key hotlink protection URL generator and checker for you to quickly and accurately generate and check hotlink protection URLs.

- [Key hotlink protection URL generator](https://vods.cloud.tencent.com/referer/gen_video_url.html)
- [Key hotlink protection URL checker](https://vods.cloud.tencent.com/referer/check_sign.html)

## Must-knows
- This feature is optional and disabled by default.
- After key hotlink protection is enabled, an original video URL can no longer be used for video playback, and a valid hotlink protection URL needs to be generated according to the rules.
- The key (`KEY`) must contain 8–20 letters or digits.
- If the hotlink protection URL expires or the signature fails to pass the check, the video cannot be played back and a 403 response code will be returned.
- The parameters in `QueryString` of a hotlink protection URL must be in the order of `t`, `exper`, `rlimit`, `us`, and `sign`; otherwise, the video cannot be played back.
- If you use the preview feature, make sure that the preview duration is shorter than the video duration; otherwise, the video cannot be played back.
- There are strict restrictions on video formats available for preview mode (for example, only H.264 is supported, and the video metadata must be in the header of the video file). An exception will occur when an original video that does not meet the format requirements is played back in preview mode. We recommend you transcode such videos by using the VOD transcoding feature before setting preview mode for them (all the output formats meet the preview format requirements).
