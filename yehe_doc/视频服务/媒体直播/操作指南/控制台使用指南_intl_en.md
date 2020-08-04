MediaLive is managed at the channel level in three major modules: input security group, input, and channel.
The security group module mainly manages the security verification of the input source; the input module can configure the protocol and input method of the channel input source; and the channel module is the main module of MediaLive and can perform various operations such as transcoding and remuxing on the input stream and then generate the output stream.

## Security Group
An input security group is used to verify the validity of the input source's IPv4 address, which makes the input of MediaLive channels more secure.
### Creating security group
![](https://main.qcloudimg.com/raw/d6a6ae8de1db8cb120e995c11b61aec3.png)
Name: name of the security group, which is a string containing 32 letters, digits, and underscores.
Allowlist: valid range of the input IPv4 addresses in CIDR format; for example, `0.0.0.0/0` means that all input IPs are valid. Up to 10 IP ranges can be entered and separated by line break.

**Note**: you can create up to 5 security groups in the console by default. If you need more security groups, please submit a ticket for assistance.

### Viewing security group

![](https://main.qcloudimg.com/raw/a3c9a3f88f00d65e8993de2224244d3e.png)
The security group list is composed of 4 parts:
The first column is the name of the security group as explained above;
The second column indicates the status of the security group, which can be either "idle" or "occupied". The former means that the security group is currently not associated and can be edited and deleted, while the latter indicates that the security group is currently associated with a channel input and can be edited but not deleted.

## Channel Input

A channel input is MediaLive's media stream input channel, which is usually associated with one security group and one MediaLive channel.
### Creating input
![](https://main.qcloudimg.com/raw/f6890473b696bfa90064d2f3edffc76d.png)
Name: name of the channel input.
Type: supports 5 input types (RTP, RTMP, UDP, HLS, and HTTP-MP4) and 2 input methods (PULL and PUSH).
Security Group: associated security group. One input can be associated with only one security group.
**Note**


> 1. There can be up to 5 inputs in the console by default.
> 2.The input media source currently must contain at least one video data channel.
> 3.When MPEG-TS multiplexing is used, a maximum of 8 channels can be transferred simultaneously.

## Channel
A channel contains the details of various operations on an input stream in MediaLive such as transcoding, remuxing, and relaying to other destination address.
A channel can be created in the following steps:

> 1.Associate an existing input.
> 2.Configure an audio selector.
> 3.Configure parameters for transcoding, remuxing, and output.

Multiple ways are provided to configure channels:

> 1. Create a channel from scratch, so that you can fully customize all the options you want.
> 2. Use a built-in or custom template for creation.
> 3. Clone the configuration of an existing channel and make desired modifications.

### Creating channel
![](https://main.qcloudimg.com/raw/010317a5d04d3019c1856dfafb1ffade.png)
1. Name the channel.
**Note**: the channel name must be unique under the account; otherwise, channel creation will fail.
2. Associate a channel input and create an audio selector.
You can select an input that can be associated from the list of created inputs, so that the channel can input the stream through the associated input.
3. Configure channel outputs.
Configure an output group:


> 1. Name the output group to identify the output group and associate the name of the main manifest file of the playback address.
> 2. Configure the output group type to configure the package type of the current output task. Valid values include `hls`, `dash`, and `hls archive`.
> 3. Configure the output addresses which divide into the master output address and slave output address corresponding to the master/slave input addresses in the input, respectively. If your CDN injection point has authentication enabled, you can enter authentication parameters for verification, including `UserName` and `Password`.
> 4. Configure DRM parameters. After enabling this feature, you can enter a custom `Content Id`. For the generation method, please see the related DRM document.
> 5. Configure an audio template, including audio name, audio transcoding format, audio bitrate and corresponding audio language. If no audio selector is associated, a default stream will be selected from the input streams for transcoding output. Currently supported audio transcoding bitrate range is 6000–1024000 bits. The language code follows the ISO 639 standard, so a 3-character language code needs to be entered.
> 6. Configure a video template, including video template name, encoder type (valid values: H264), video transcoding bitrate (value range: 50000–40000000 bits), resolution, frame rate, etc. Top speed codec transcoding is a high-performance video transcoding service developed by Tencent Cloud Video Team. After this feature is enabled, AI algorithms can be used to calculate the optimal dynamic encoding parameters based on the business scenario in real time to implement transcoding services with low bitrate and high quality. Bitrate compression ratio is the percentage of video bitrate that is expected to be reduced.
> 7. Configure outputs to combine and associate the created audio and video transcoding templates. In addition, you can pass through SCTE-35 information in MPEG-TS.

At this point, the channel configuration is completed.
You can operate on your input stream based on the configured channel and output it. In addition, you can view the channel running status on the channel's Alerts and Health pages to identify and analyze some basic alerts.
