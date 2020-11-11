
## Step 1: Configure channel name.
Channel name is used to identify the different channels that you created.
 ![](https://main.qcloudimg.com/raw/d4bae364e0c3c51d6be78858d85e661d.jpg)

## Step 2: Select an input.
Select an input to associate with the channel.
If you have multiple audio streams in your rtp / rtp-fec / udp input source, you can create a selector here based on the audio pid encapsulated in mepgts so that you can configure multiple audio languages in the output configuration.
 ![](https://main.qcloudimg.com/raw/6eb57c71f10a3ad9ec209f218efdc148.jpg)

>! The pid here must be the same as the pid in input audio stream, otherwise the transcoding task may fail.

## Step 3: Configure output group.
### 1. Configure multiple output groups.
MediaLive supports multiple output groups for one channel. Click “+” on the upper right to add multiple output groups.
![](https://main.qcloudimg.com/raw/1d1ba42772601106731cc81cc88fca45.jpg)

### 2. Configure the name and type of the output group.
Set the name and type for the current output group. Currently, MediaLive supports outputting HLS, DASH files. You can also output HLS files to COS for archiving. For more information, see [Outputting LVB stream to COS for archiving](https://intl.cloud.tencent.com/document/product/1048/38361). MediaLive also supports integration with MediaPackage and directly outputs HLS/DASH live streams to MediaPackage under the same account. This helps you build your own origin servers and perform stable distribution of live broadcast at a large-scale. For more information, see [Outputting LVB stream to MediaPackage](https://intl.cloud.tencent.com/document/product/1048/38362).
![](https://main.qcloudimg.com/raw/e85b466e4310cf22e05a26fdd7cb9f5b.jpg)

> ? For more information about COS, see [COS Overview](https://intl.cloud.tencent.com/document/product/436/6222)

### 3. Configure a CDN URL for MediaLive outputting.
If a HLS or DASH output is used, you can set a CDN here and enter the verification information when needed. 
![](https://main.qcloudimg.com/raw/b6e6995cb7c14ce36893fb1c5df99c58.jpg)

### 4. Configure segment.
Set the duration and number of segment in the manifest file. Enable “PdtInsertion” and configure the “PdtDuration” if you need to insert UTC time in the tag file.
 ![](https://main.qcloudimg.com/raw/9eb8dae8fd4105cef8fa0d3009043d24.jpg)

### 5. Configure DRM.
MediaLive supports Tencent DRM and custom DRM. Please select based on your needs.
![](https://main.qcloudimg.com/raw/3d51bc21d6554446339aa2ea857d0dd0.jpg)

>!
>- If you select HLS/HLS_ARCHIVE/HLS_MediaPackage as “Output Group Type” in “Output Group Setting”, Fairplay encryption will be used when DRM is enabled.
>- If you select DSAH/DASH_MediaPackage as “Output Group Type” in “Output Group Setting”, Widevine encryption will be used when DRM is enabled.

a. Fairplay key configuration
When you select HLS/HLS_ARCHIVE/HLS_MediaPackage as the output type, the encryption method will be Fairplay. You need to configure the Fairplay's ContentId(KeyId), Key and Iv. Key and Iv are 32-bit hexadecimal strings.
![](https://main.qcloudimg.com/raw/9d972f049ac9f58f5c3c1e440d0ae38c.jpg)
b. Widevine key configuration
When you select DSAH/DASH_MediaPackage as the output type, the encryption method will be Widevine. You need to configure Widevine’s ContentId and Track Setting. Track type includes SD/HD/UHD1/UHD2/AUDIO.
When you select “All Track”, all five track types will share the same KeyId and Key.
  ![](https://main.qcloudimg.com/raw/ccd46622e810f98f376e0080ceeea93c.jpg)
When you select “Select Track”, the KeyId and Key of each track type will be customizable
 ![](https://main.qcloudimg.com/raw/338479820cd026f1c1906ca3c8b82ff9.jpg)

### 6. Configure audio templates.

You are allowed to configure multiple audio transcoding with one output unit. You can configure an audio template, including audio name, audio transcoding format, audio bitrate and corresponding audio language. If no audio selector is associated, a default stream will be selected from the input streams for transcoding output. Currently the supported audio transcoding bitrate range is 6000–1024000 bits. The language code follows the ISO 639 standard, and requires a 3-character language code entry.
![](https://main.qcloudimg.com/raw/a3b17971253ef16421b73b5b18e147ad.jpg)

### 7. Configure video templates.

Configure a video template here, including video template name, encoder type (valid values: H264), video transcoding bitrate (value range: 50000–40000000 bits), resolution, frame rate, etc. Top speed codec transcoding is a high-performance video transcoding service developed by Tencent Cloud Video Team. When you enable the feature, AI algorithms can be used to calculate the optimal dynamic encoding parameters based on the business scenario in real time to implement transcoding services with low bitrate and high quality. Bitrate compression ratio is the video bitrate percentage that is expected to be reduced.
![](https://main.qcloudimg.com/raw/960518ebce570f617872941257da7ba7.jpg)

>? If you need a better codec with smart video compression algorithm, enable "Top speed codec transcoding”. When this feature is enabled, AI algorithms can be used to calculate the optimal dynamic encoding parameters based on the business scenario in real time to implement transcoding services with low bitrate and high quality. You can enter the bitrate compression ratio expected to be reduced in the input box on the right side.
>

### 8. Configure and combine outputs.
Configure outputs to combine and associate the created audio and video transcoding templates. In addition, you can pass through SCTE-35 information in the file tags of HLS or DASH.
 ![](https://main.qcloudimg.com/raw/a8076054a9b3c0664f2a876fcf86c0c0.jpg)

## Step 4. Complete the configuration.

After completing the configuration, you can click “Start Channel” to run the channel.
