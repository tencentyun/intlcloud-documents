## AD insertion
With the advancement of streaming media technology and applications on internet, it is apparent that ad-supported streaming media delivery has become a major monetization strategy. By using Tencent Cloud's Stream Service, you can implement dynamic ad insertion based on CTE-35 ad markers and SSAI. The complete general process of SSAI is as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/3d7f3f8f5ba9186e284d96458364a2b3.png)

1）The publisher pushes the live stream to StreamLive for transcoding, packaging, and inserting SCTE-35 ad markers, and then transmits it to StreamPackage. If there are no subsequent processes, step 1) has already completed all server-side steps in CSAI.
2）The player requests the manifest (m3u8/mpd), and StreamPackage fetches the origin manifest while parsing the manifest and checking the SCTE-35 ad markers.
3）StreamPackage send the request to the Ad Decision Server, parses the VAST/VMAP response, and obtains the ad video address.
4）StreamPackage downloads the ad video, transcodes and stores it.
5）StreamPackage updates the transcoded ad segment url in the manifest by inserting and replacing, and then distribute it. 
6）After the ad is played on the client-side, StreamPackage reports to the ad Tracking service for tracking the event.

If you use this AD insertion feature. [AD insertion fee](https://www.tencentcloud.com/document/product/1063/50091?lang=en&pg=) will be incurred.

### 1. Enabling Ad Configuration
Click the channel name or Info on the right to go to the channel details page. In the endponts tab, you can enable Ad Configuration for the endpoints:

![](https://qcloudimg.tencent-cloud.cn/raw/e820b2dda085733f139fc685ad6a016b.png)

Click **AD Configuration** to enter the configuration page which includes：
- **Ad decision server**：The URL for the ad decision server (ADS).
- **Configuration aliases**：Configuration aliases are used for dynamic variable replacement.
- **Personalization details**：Optional settings for ad break personalization.
- **Advanced settings**：Advanced settings allow you to fine-tune properties related to your content delivery network (CDN) prefix, DASH.


### 2. Configuring URL for the ADS
![](https://qcloudimg.tencent-cloud.cn/raw/16cdc5256cb736d949af14e5a84e1eb2.png)
The ad decision server (ADS) is the origin server that’s providing content to StreamPackage. It determines which ads StreamPackage will insert in ad breaks in the manifest. The URL for the ad decision server (ADS) is an address starting with http:// or https://. Maximum 25,000 characters.

### 3. Configuring aliases
Player parameters and aliases used for dynamic variable replacement. Click **Add player parameter**, **Edit**, **Delete** on the right to maintain player parameters. Parameter name can contain up to 32 letters, digits, underscores(_), and hythens(-).

![](https://qcloudimg.tencent-cloud.cn/raw/db2f8ab197d1741e60b0fdda12b6d5c8.png)

Enter alias key name and alias value in the parameter. You'll use the alias key as a player parameter variable during dynamic variable replacement. StreamPackage will replace the alias key with the mapped alias value.


#### An example：
#### 1）URL for the ADS
```
https://my.ads.com/path?ad_type=[player_params.ad_type]&region=[player_params.region]
```

#### 2）Aliases for dynamic variable replacement
```
"ConfigurationAliases": {
    "player_params.ad_type": {
        "customized": "abc",
        "default": "default"
    },
    "player_params.region": {
        "india": "ap-mumbai",
        "japan": "ap-tokyo"
    },
}
```

#### 3）Add key-value in the request to StreamPackage
```
<master>.m3u8?ad_type=customized&region=india
```

#### 4）StreamPackage will pass the parameters to ADS
```
https://my.ads.com/path?ad_type=abc&region=ap-mumbai
```

### 4. Setting default slate ad
The slate ad is a default ad that’s used if an ad break isn’t filled by an ad replacement. It lets you define what happens when an ad break isn’t completely filled by the ads dictated by the ad decision server (ADS). This way, if an ad is unavailable or too short, or if network conditions prevent the ad decision server from responding to StreamPackage, you know exactly what will be played instead. If an ad slate isn’t specified, then the default is to show the underlying content stream. The URL for the slate ad is an address starting with http:// or https://. Maximum 25,000 characters.

![](https://qcloudimg.tencent-cloud.cn/raw/c06a36db8c817361e6a298331b95a98a.png)

The personalization threshold sets the maximum duration (in seconds) of underfilled ad time allowed in an ad break. If the duration of underfilled ad time exceeds the personalization threshold, then personalization of the ad break is abandoned and the underlying content is shown.



### 5. Advanced settings
![](https://qcloudimg.tencent-cloud.cn/raw/da1325577ee521b3c158fbd15d36991c.png)

- **Ad marker passthrough**：Enable or disable ad marker passthrough.
- **DASH mpd location**：Enable or disable DASH support for sticky HTTP redirect behavior in players that don't support sticky.
- **SCTE-35 ad message type**：Specify how ad markers are packaged in the output.

### 6. Origin manifest and personalized manifest after replacement
The following examples provide a comparison between the origin manifest and the personalized manifest after replacement.

#### Origin manifest
Here is an example of the HLS master manifest obtained by StreamPackage from the original stream: 
```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-INDEPENDENT-SEGMENTS
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=500000,RESOLUTION=640x360
tx_ssai_temp1.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=2000000,RESOLUTION=960x540
tx_ssai_temp2.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=3000000,RESOLUTION=1280x720
tx_ssai_temp3.m3u8
```
Here is an example of the HLS media manifest obtained by StreamPackage from the original stream, which includes inserted SCTE-35 markers:
```
#EXTM3U
#EXT-X-VERSION:5
#EXT-X-MEDIA-SEQUENCE:3835222
#EXT-X-TARGETDURATION:6
#EXTINF:6.000, no desc seq 3835223
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907362016.ts?&3835223
#EXTINF:2.333, no desc seq 3835224
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907368016.ts?&3835224
#EXT-OATCLS-SCTE35:/AAgAAHwulfuAAAADwUAAACcAPCAAA27oAAAAAAAAPKrLtw=
#EXT-X-CUE-OUT:10
#EXTINF:3.667, no desc seq 3835225
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907370349.ts?&3835225
#EXT-X-CUE-OUT-CONT:ElapsedTime=3.667,Duration=10,SCTE35=/AAgAAHwulfuAAAADwUAAACcAPCAAA27oAAAAAAAAPKrLtw=
#EXTINF:6.000, no desc seq 3835226
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907374016.ts?&3835226
#EXT-X-CUE-OUT-CONT:ElapsedTime=9.667,Duration=10,SCTE35=/AAgAAHwulfuAAAADwUAAACcAPCAAA27oAAAAAAAAPKrLtw=
#EXTINF:0.333, no desc seq 3835227
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907380016.ts?&3835227
#EXT-X-CUE-IN
#EXTINF:5.667, no desc seq 3835228
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907380349.ts?&3835228
#EXTINF:6.000, no desc seq 3835229
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907386016.ts?&3835229
#EXTINF:6.000, no desc seq 3835230
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907392016.ts?&3835230
```
#### Personalized manifest
Here is an example of the personalized HLS master manifest generated by StreamPackage:
```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-INDEPENDENT-SEGMENTS
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=500000,RESOLUTION=640x360
tx_ssai_temp1.m3u8?session_id=fd320a4d99ba7df952f5a214ed901935&type=manifest
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=2000000,RESOLUTION=960x540
tx_ssai_temp2.m3u8?session_id=fd320a4d99ba7df952f5a214ed901935&type=manifest
#EXT-X-STREAM-INF:PROGRAM-ID=0,BANDWIDTH=3000000,RESOLUTION=1280x720
tx_ssai_temp3.m3u8?session_id=fd320a4d99ba7df952f5a214ed901935&type=manifest
```


Here is an example of the personalized HLS media manifest generated by StreamPackage:
```
#EXTM3U
#EXT-X-VERSION:5
#EXT-X-MEDIA-SEQUENCE:3835222
#EXT-X-TARGETDURATION:6
#EXTINF:6.000, no desc seq 3835223
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907362016.ts?&3835223
#EXTINF:2.333, no desc seq 3835224
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907368016.ts?&3835224
#EXT-X-DISCONTINUITY
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835224
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835225
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835226
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835227
#EXTINF:2.000,
segment?type=segment&session_id=fd320a4d99ba7df952f5a214ed901935&manifest_num=tx_ssai_temp3.m3u8&seq_num=3835228
#EXT-X-DISCONTINUITY
#EXTINF:5.667, no desc seq 3835228
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907380349.ts?&3835228
#EXTINF:6.000, no desc seq 3835229
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907386016.ts?&3835229
#EXTINF:6.000, no desc seq 3835230
64998DFC00006B56A7AF-p0_tmplav9601_av9601-1689907392016.ts?&3835230
```