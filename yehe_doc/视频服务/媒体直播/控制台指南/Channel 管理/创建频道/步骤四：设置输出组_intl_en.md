StreamLive supports different types of outputs. This document shows you how to create outputs and output groups.

## Configuring multiple output groups for a channel
You can configure multiple output groups for a channel by clicking the plus icon.
![](https://qcloudimg.tencent-cloud.cn/raw/3e13eac666167d0f867e51e8a97cc1f0.png)

## Setting the name and type of an output group
Set the name and type of an output group:
![](https://qcloudimg.tencent-cloud.cn/raw/6b239c37c95f0cc226bc93e12a481395.png)
Currently, the types of outputs supported are HLS, DASH, HLS_STREAM_PACKAGE, DASH_STREAM_PACKAGE, HLS_ARCHIVE, and DASH_ARCHIVE.

- HLS and DASH outputs are sent to the destination via HTTP PUT.
- HLS_STREAM_PACKAGE and DASH_STREAM_PACKAGE outputs are sent to [StreamPackage](https://intl.cloud.tencent.com/document/product/1048/45219) of the current account. You can use the outputs as origin servers to stream content via CDNs.
- HLS_ARCHIVE and DASH_ARCHIVE outputs are saved to [Tencent Cloud COS](https://intl.cloud.tencent.com/document/product/1048/45218).

## Configuring the destinations
- If the output type is HLS or DASH, enter the CDN URLs to push to. Enter the authentication information as well if the URLs require authentication.
![](https://qcloudimg.tencent-cloud.cn/raw/e76f39828aade1c04c31b17e521220ed.png)
- If the output type is HLS_STREAM_PACKAGE or DASH_STREAM_PACKAGE, enter the **ID of the StreamPackage channel** to push live streams to.
![](https://qcloudimg.tencent-cloud.cn/raw/05cae1db0fcfe74a723a0d828e3f5485.png)
- If the output type is HLS_ARCHIVE or DASH_ARCHIVE, enter the **COS destinations** to save the output. StreamLive will save live streams in the last seven days to COS (the data will be overwritten after restart).
![](https://qcloudimg.tencent-cloud.cn/raw/15f727c5101320835259eeb4b0f82529.png)

## Configuring DRM
StreamLive supports DRM (CustomDRMKeys and SDMCDRM). For detailed directions how to enable the feature, see [Channel DRM Configuration via DRMtoday](https://intl.cloud.tencent.com/document/product/1048/45217).
![](https://qcloudimg.tencent-cloud.cn/raw/8d81955db11e160cb0be5e2a8ed9226a.png)

## Configuring transcoding templates
You can configure either joint or separate transcoding templates. For HLS outputs, separate transcoding allows you to combine different audio tracks. If you don’t need this, we recommend you use joint transcoding templates.
- A joint transcoding template includes settings for both audio and video transcoding.
![](https://qcloudimg.tencent-cloud.cn/raw/5567d7eff345ae787a98f4e5c0692bc9.png)
- With separate transcoding, you need to set audio and video transcoding parameters separately.
![](https://qcloudimg.tencent-cloud.cn/raw/aa81355608bc2ad72eab06e043a88fb3.png)
![](https://qcloudimg.tencent-cloud.cn/raw/00196f0a0566111d33a4aef484809110.png)
>! **Top Speed Codec Transcoding** is a high-performance transcoding service developed by the Tencent Cloud Video team. It offers low-bitrate, high-quality transcoding by leveraging AI algorithms to dynamically determine the best encoding parameters. **Bitrate Compression Ratio** is the percentage of video bitrate expected to be reduced.

### Configuring outputs
- If you configure joint transcoding templates, you can select only one template for each output, which is used as one stream in multi-bitrate streaming.
![](https://qcloudimg.tencent-cloud.cn/raw/b007445cb3f47a9ec6d827f959cff9ba.png)
- If you configure separate transcoding templates, you can select one video transcoding template and multiple audio transcoding templates for each output. The video transcoding template specifies transcoding parameters for one stream in multi-bitrate streaming, while the audio transcoding templates specify parameters for the audio tracks the stream can use.
![](https://qcloudimg.tencent-cloud.cn/raw/8b758ded635531a9a24f1aae51eb9828.png)

### Saving the configuration
Click **Done** to save the configuration. This concludes the configuration of a channel. You can then click **Start** to start the channel.
![](https://qcloudimg.tencent-cloud.cn/raw/a596817ccf73cd4573f83e3d572fcbee.png)