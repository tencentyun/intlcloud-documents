## Overview
- You can specify the expiration time in a video URL to prevent malicious users from transferring the URL to other websites for long-term unauthorized viewing.
- You can specify the maximum number of IPs allowed to play a video from a URL to prevent malicious users from distributing the video to a large number of viewers.
- You can specify the preview duration in a video URL to implement a video preview.
- You can add a region allowlist/blocklist to a video URL.
- You can add a referer allowlist/blocklist to a video URL.
- You can use a key (`KEY`) to create a signature and put it into a video URL. As long as the key is not disclosed, the video URL cannot be forged.
- A CDN node controls video playback requests by checking the parameters and signature in the video URL. If a request fails to pass the check, a 403 response code will be returned.
- Supported file formats include MP4, TS, M3U8, FLV, AAC, MOV, WMV, AVI, MP3, RMVB, MKV, MPG, 3GP, WEBM, M4V, ASF, F4V, WAV, MPEG, VOB, RM, WMA, DAT, M4A, MPD, and M4S.

>? For more information, see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/14060).

## Generating a Hotlink Protection URL
- All your videos in VOD have an **original video URL**. If hotlink protection is not enabled, the original video URL can be used to play back the video.
- After key hotlink protection is enabled, the original video URL can no longer be used for video playback, and a **hotlink protection URL** of the video needs to be generated.

You can generate a hotlink protection URL for a video by adding hotlink protection parameters at the end of the original URL in the form of a query string. Below is an example:
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=[t]&exper=[exper]&rlimit=[rlimit]&us=[us]&whreg=[whreg]&whref=[whref]&sign=[sign]
```
Below are descriptions and values of the parameters in a hotlink protection URL.

#### Hotlink protection parameters
| Parameter Name | Required | Description |
| ------ | ---- | ------------------------------------------------------------ |
| `KEY` | Yes | The key used when key hotlink protection is enabled. It can contain 8–20 letters (a–Z) or digits (0–9). We recommend you generate this key in the console. For detailed directions, see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/14060). |
| `Dir` | Yes | The part of the original video URL with the filename removed. For example, if the original URL is `http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4`, then the playback path is `/dir1/dir2/`. |
| `t` | Yes | <li>The expiration time of the playback URL, which is expressed as a Unix hexadecimal timestamp in lowercase. <br><li>Once expired, the URL will become invalid, and a 403 error will be returned. Given the potential time differences between devices, we recommend you set the expiration time five minutes (300 seconds) later than the actual time you want the URL to expire. <br><li>The validity period of the URL should be longer than the video length so that the full video can be played. |
| `exper` | No | <li>The preview duration in decimal seconds. If this parameter is left empty or set to 0, preview is disabled (the full video will be returned). <br><li>The preview duration must be shorter than the original video duration; otherwise, playback may fail. |
| `rlimit` | No | <li>The maximum decimal number of IPs allowed for playback. The maximum value is 9. If this parameter is left empty, there is no restriction. <br><li>Suppose you want your video to be played by only one user. We do not recommend setting `rlimit` to 1 (instead, set it to 3, for example). This is because the IP of a mobile device may change after a reconnection. |
| `us` | No | <li>The link ID. This is used to randomize a hotlink protection URL to improve its uniqueness. <br><li>We recommend you specify a random `us` value every time you generate a hotlink protection URL. |
| `whreg`  | No   | <li>A list of regions allowed to play the video. You can specify 1-10 [three-letter region codes](https://www.iso.org/obp/ui/#search/code/). Separate the codes with commas. |
| `bkreg`  | No   | <li>A list of regions banned from playing the video. You can specify 1-10 [three-letter region codes](https://www.iso.org/obp/ui/#search/code/). Separate the codes with commas. |
| `whref`  | No   | <li>A list of domains allowed to play the video. You can specify 1-10 domains. Leave out the `http://` and `https://` prefix, and separate the domains with commas. If you enter `abc.com`, it will cover lower-level domains such as `abc.com/123` and `abc.com.cn`. Wildcards are supported. For example, you can enter `*.abc.com`. |
| `whref`  | No   | <li>A list of domains banned from playing the video. You can specify 1-10 domains. Leave out the `http://` and `https://` prefix, and separate the domains with commas. If you enter `abc.com`, it will cover lower-level domains such as `abc.com/123` and `abc.com.cn`. Wildcards are supported. For example, you can enter `*.abc.com`. |
| `sign` | Yes | <li>The hotlink protection signature. It is a hexadecimal number with a length of 32 characters and is used to check the validity of a hotlink protection URL. <br><li>A 403 error will be returned if a URL fails to pass the signature check. For how to generate the signature, see [below](#formula). |

#### [](id:formula)Signature calculation formula
```
sign = md5(KEY + Dir + t + exper + rlimit + us + whref + bkref + whreg + bkreg)
```

`+` in the formula is used to concatenate two strings. Optional parameters can be empty strings.

## Examples of Hotlink Protection URL Generation
Assume that you have a video in VOD and its original playback URL is `http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4`. You have enabled key hotlink protection. The generated key is `24FEQmTzro4V5u3D5epW`, and the generated random string is `72d4cd1101`, and now you want to:
1. Generate a hotlink protection URL for this video and set the expiration time of the URL to 20:00 on January 31, 2018 (1517400000 in Unix time).
2. Generate a preview URL and set the preview duration to the first five minutes of the video (the original video duration is longer than five minutes).
3. Set the maximum number of IP addresses allowed to play the video to three.

The following describes how to generate hotlink protection URLs for three different example scenarios.

### Example 1. Limiting the expiration time
#### Step 1. Determine the hotlink protection parameters

| Parameter | Value | Description |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | The key you set when enabling key hotlink protection. |
| Dir | /dir1/dir2/ | The part of the original video URL with the filename `myVideo.mp4` removed. |
| `t`      | `5a71afc0`             | The expiration timestamp (1517400000) converted to hexadecimal.          |
| `us`     | `72d4cd1101`           | The generated random string.                                   |


#### Step 2. Calculate the signature

```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc072d4cd1101") = "3d8488faeb37d52d6bf63b63c1b171c3"
```

#### Step 3. Generate a hotlink protection URL
Add the hotlink protection parameters to the original URL in the form of a query string:
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&us=72d4cd1101&sign=3d8488faeb37d52d6bf63b63c1b171c3
```

### Example 2. Limiting the number of IP addresses
#### Step 1. Determine the hotlink protection parameters

| Parameter | Value | Description |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | The key you set when enabling key hotlink protection. |
| Dir | /dir1/dir2/ | The part of the original video URL with the filename `myVideo.mp4` removed. |
| `t`      | `5a71afc0`             | The expiration timestamp (1517400000) converted to hexadecimal.          |
| `rlimit` | `3`                    | Allow up to three IP addresses to play the video.                   |
| `us`     | `72d4cd1101`           | The generated random string.                                   |

#### Step 2. Calculate the signature
```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc0372d4cd1101") = "c5214f0d5961b13acd558b4957c4dfc5"
```

#### Step 3. Generate a hotlink protection URL
Add the hotlink protection parameters to the original URL in the form of a query string:
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&rlimit=3&us=72d4cd1101&sign=c5214f0d5961b13acd558b4957c4dfc5
```

### Example 3. Limiting the playback duration
#### Step 1. Determine the hotlink protection parameters

| Parameter | Value | Description |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | The key you set when enabling key hotlink protection. |
| Dir | /dir1/dir2/ | The part of the original video URL with the filename `myVideo.mp4` removed. |
| `t`      | `5a71afc0`             | The expiration timestamp (1517400000) converted to hexadecimal.          |
| `exper`  | `300`                  | Preview the first five minutes (i.e., 300 seconds).                                 |
| `us`     | `72d4cd1101`           | The generated random string.                                   |

#### Step 2. Calculate the signature

```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc030072d4cd1101") = "547d98c4b91e81b5ea55c95cef63223f"
```

#### Step 3. Generate a hotlink protection URL
Add the hotlink protection parameters to the original URL in the form of a query string:
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&exper=300&us=72d4cd1101&sign=547d98c4b91e81b5ea55c95cef63223f
```

## Key Hotlink Protection URL Generator and Checker
VOD provides key hotlink protection URL generator and checker for you to quickly and accurately generate and check hotlink protection URLs.

- [Key hotlink protection URL generator](https://vods.cloud.tencent.com/referer/gen_video_url.html)
- [Key hotlink protection URL checker](https://vods.cloud.tencent.com/referer/check_sign.html)

## Notes
- This feature is optional and disabled by default.
- After key hotlink protection is enabled, the original video URL can no longer be used for playback. You need to generate a hotlink protection URL according to the rules specified above.
- The key (`KEY`) must contain 8–20 letters or digits.
- If the hotlink protection URL expires or the signature fails to pass the check, the video cannot be played back and a 403 response code will be returned.
- Make sure the parameters in the query string of a hotlink protection URL are in the order of `t`, `exper`, `rlimit`, `us`, and `sign`; otherwise, playback will fail.
- If you use the preview feature, make sure that the preview duration is shorter than the video duration; otherwise, the video cannot be played back.
- The preview feature has strict restrictions on video formats (for example, only H.264 is supported, and the metadata must be included in the header of the video file). Preview will fail if a video does not meet the requirements. We recommend you transcode your video in VOD before enabling preview (all transcoding files generated by VOD meet the preview requirements).