The StreamLive service is managed at the channel level in the StreamLive console. You can set up high-quality video streams and distribute them to various types of devices. The channel management module is the main module of StreamLive, via which you can perform various video processing operations such as transcoding and remuxing and send the results to the specified destination or store them on COS.

### Creating a channel

Choose **Channel Management** on the left sidebar and click **Create Channel**.

#### 1. Customize the channel name

Enter a custom channel name, which is used to identify different channels created, and click **Next Step**.

![img](https://main.qcloudimg.com/raw/824d8ad80106fb65f69df5dffae7bd0b.png)

#### 2. Add inputs

You can add one or more of the inputs created to the channel. **Normally, the first input attached is used by default.** Other inputs may be used in failover or if a plan is configured. You can attach up to 5 inputs to a channel, including up to 2 push inputs.
![img](https://main.qcloudimg.com/raw/72974873310b8f07ea0acc09ce3c3f64.png)

Click **Settings** to configure an input:

a. **Audio Selector**: If there are multiple audio streams in your RTP_PUSH/RTP-FEC_PUSH/UDP_PUSH inputs, you can create a selector using the PID encapsulated in MPEG-TS so that you can configure multiple audio languages for outputs.
![img](https://main.qcloudimg.com/raw/8ea9e3a78e57242e446f4ab2f4cd6850.png)

>!
> - The PID must be the same as that of the input audio stream; otherwise, the transcoding task may fail.
> - You can configure audio selectors only for the first input attached. If a plan is configured and another input is used instead of the first one, StreamLive will randomly select an audio stream to transcode.
> - If input source failover is enabled, the audio selectors configured for the primary input will be automatically applied to the backup input to ensure the availability of the audio encoding feature in case of failover.

b. **Pull-Stream Settings**: You can select either the **LOOP** or **ONCE** mode for MP4_PULL/HLS_PULL inputs. **LOOP**: the pull loops; **ONCE**: the input is disconnected after the first pull.
![img](https://main.qcloudimg.com/raw/a721d60a7263dddeab3927b3331cfaa2.png)

c. **Failover Settings**: You can enable failover for RTMP_PUSH/RTP_PUSH inputs so that StreamLive switches automatically to the backup input when the primary one fails. After enabling failover for an input, you can select for it a backup input, set a downtime threshold (the wait time after the primary input is down before failover is triggered; 3000 ms by default), and select the input preferences, i.e., whether to switch back to the primary input after it recovers (**PRIMARY_PREFERRED**: the primary input is prioritized; **EQUAL_PREFERRED**: the primary and backup inputs have the same priority).
![img](https://main.qcloudimg.com/raw/588efa49ee40b158793421c6ced77319.png)
![img](https://main.qcloudimg.com/raw/ebc0d3305a94534edaf97d09ecf18f9c.png)

>?
> - You can configure only one backup for an input. The primary and backup inputs must be of the same type and attached to the same number of channels.
> - Once an input is used as a backup, the failover feature will be disabled for the input automatically, which means that you cannot configure a backup for this input. For modifications (for example, if you want to swap the role of the two inputs), you must disassociate the inputs first.
> - After successful configuration, **Primary** and **Backup** will appear next to the names of the primary and backup inputs.
> - The backup input will appear below the primary input.

In addition to the above, you can also do the following to an input:

- Click **Details** to view the input address and other basic information of an input.
- Click **Set as First** to pin an input to the top and set it as the default input. Note: you cannot do this to a backup input.
- Click **Delete** to delete an input.

Click **Next**.

#### 3. Configure output groups

a. Configure multiple output groups. You can click the "+" icon to configure multiple output groups for a channel.

![img](https://main.qcloudimg.com/raw/e6af7ba8a52e288e0d02dc3bea54871e.png)

b. Set the name and type of an output group. Currently, StreamLive supports outputs in HLS and DASH formats. You can output HLS files [to COS for archiving](https://intl.cloud.tencent.com/document/product/1048/45218) or output HLS/DASH streams [to Tencent Cloud's StreamPackage under the same account](https://intl.cloud.tencent.com/document/product/1048/45219). This allows you to build your own origin server for stable and large-scale distribution of live streams.

>?
> - [StreamLive Outputting to COS](https://intl.cloud.tencent.com/document/product/1048/45218)
> - [StreamLive Outputting to StreamPackage](https://intl.cloud.tencent.com/document/product/1048/45218)

![img](https://main.qcloudimg.com/raw/6b87cbe42011cc98c045af99369348a3.png)

c. Set a CDN streaming address. If an HLS or DASH output is used, you can set the destination to a CDN URL. Enter the verification information if the URL requires verification.

![img](https://main.qcloudimg.com/raw/8fb39dfab5a32ea34444b9a6f1e4edab.png)

d. Configure segments. Set the segment duration and quantity in your "manifest" file. If you want to insert UTC time into the tag file, enable **PdtInsertion** and set **PdtDuration** (time interval for insertion).

![img](https://main.qcloudimg.com/raw/36b16a1dda37c530d7b8f497688a93d9.png)

e. Configure DRM. You can use third-party DRM services in StreamLive.

![](https://qcloudimg.tencent-cloud.cn/raw/f1cffba329af61327687d0efbe7442e1.png)

If you select **SDMCDRM** as the DRM scheme, you need to set the **Uid**, **Secret id**, **Secret key**, and **Url** fields.

![](https://qcloudimg.tencent-cloud.cn/raw/e1350792aa213fe072920231474b0f68.png)

>?
>- If you select HLS/HLS_ARCHIVE/HLS_StreamPackage for **Output Group Type** in **Output Group Setting** and enable DRM, FairPlay encryption will be used. If you select DASH/DASH_StreamPackage and enable DRM, Widevine encryption will be used.
>- FairPlay encryption settings: If you select HLS/HLS_ARCHIVE/HLS_StreamPackage as the output type, FairPlay will be used as the encryption method. You need to enter the FairPlay Content ID (key ID), key, and IV (both key and IV are 32-bit hexadecimal strings).
 ![img](https://main.qcloudimg.com/raw/e172623be22b4397d9f4964d90e8eb03.png)
>- Widevine encryption settings: If you select DASH/DASH_StreamPackage as the output type, Widevine will be used as the encryption method. You need to enter the Widevine content ID and set the tracks. Track types include SD, HD, UHD1, UHD2, and AUDIO.
>- If you select **All Track**, you can set the same key ID and key for all five track types.
 ![img](https://main.qcloudimg.com/raw/06b22ae97702570f7bdfac4161219ece.png)
>- You can also click **Select Track** to set a key ID and key for each track type.
![img](https://main.qcloudimg.com/raw/9c9e6b56980d6c87aea64c2b3b426ad5.png)

f. Set audio transcoding. You are allowed to configure multiple audio transcoding schemes with one output unit. Create an audio template, specifying the name, transcoding format, bitrate, and audio language. If no audio selector is associated, the default stream in the input will be transcoded. Currently, the bitrate range supported for audio transcoding is 6000-1024000 bps. Language code is a 3-character code for the audio language to use, whose naming follows the ISO 639 standard.

![img](https://main.qcloudimg.com/raw/c092adee1a2aeca7f9e98f18659b4aef.png)

g. Set video transcoding. Create a video template, specifying the name, encoder type (only H264 is supported currently), bitrate (value range: 50000-40000000 bps), resolution, frame rate, etc. Top speed codec transcoding is a high-performance video transcoding service developed by Tencent Cloud. It uses AI algorithms to calculate in real time the optimal encoding parameters based on the business scenario to ensure high-quality transcoding at low bitrate. Bitrate compression ratio is the percentage by which video bitrate is expected to be reduced.

![img](https://main.qcloudimg.com/raw/92242c0a054e342a1071794db28600de.png)

>? You can enable top speed codec if you want a better codec with smart video compression algorithms. It uses AI algorithms to calculate in real time the optimal encoding parameters based on the business scenario to ensure high-quality transcoding at low bitrate.

h. Assemble outputs by combining the audio and video transcoding templates created. You can enable SCTE-35 to pass SCTE-35 information in HLS or DASH file tags.

![img](https://main.qcloudimg.com/raw/9e2db2401085804c20ea520364f43c3a.png)

i. Click **Done** to save the configuration.

![img](https://main.qcloudimg.com/raw/1874e5ebae643cddbe8f41c00bc92731.png)

j. Click **Start** to run the channel created.

![img](https://main.qcloudimg.com/raw/ec0fe249551d5db6d80697a1c5d47d36.png)


### Importing, exporting, cloning, editing, or deleting a channel

StreamLive allows you to import/export a channel configuration file and clone an existing channel.

#### Exporting a channel

All created channels and their states are displayed in **Channel Management** of the StreamLive console. Click **Export** in the **Operation** column to quickly export a JSON file of the channel configuration.

![img](https://main.qcloudimg.com/raw/764c7eea7b0ea222364a5b4dad88eb41.png)

![img](https://main.qcloudimg.com/raw/e67829bbee59c2148ba68ae1e652f8da.png)

#### Importing a channel

Go to **Channel Management** and click **Create Channel**. Click **Import Configuration**, and select a modified JSON file of channel configuration.

After the import, you will enter the channel editing page. Complete the rest of the configurations and submit them.

![img](https://main.qcloudimg.com/raw/1fe8fdf4c50c5be5a6fe1dc820f5469f.png)

>?
> - Channel importing is a quick configuration process. Based on the JSON file imported, StreamLive can complete the **Basic Information** and **Output Group Setting** steps for you, but not **Input Setting**. You need to select an input. Therefore, please create a new input in advance if you want to create a channel through channel importing.
> - If you import a new configuration file when editing a channel, the existing configurations will be overwritten.

#### Cloning a channel

Channel cloning is essentially a quick channel exporting and importing process. Go to **Channel Management**, and click **Clone** in the **Operation** column to clone the channel and enter its configuration page.

StreamLive will complete the channel configurations (except **Input Setting**) automatically according to the cloned channel. Complete the rest of the configurations and submit them.

![img](https://main.qcloudimg.com/raw/92bf580af5c4f013363915688744f1f6.png)

#### Editing or deleting a channel

A channel in **RUNNING** state cannot be edited or deleted. To edit or delete it, click **Stop** to stop it first.

![img](https://main.qcloudimg.com/raw/57923bc62f83d99ee10df572bebbb6e3.png)

### Monitoring channel quality

Click a channel in **Channel Management** to go to its details page, where you can view its input, output, alerts, health, and other information.

![img](https://main.qcloudimg.com/raw/c97468a3a9fbeb51e9c15ae552d53efd.png)

If a problem occurs or is likely to occur in any pipeline of a channel, StreamLive will generate an alert for the channel. **Set time** is the time when the alert is generated, and **Cleared time** is the time when the alert is cleared. The state of an alert changes. When the alert state is **SET**, the **Set time** and **State** columns are highlighted in red. After an alert is cleared, its state changes to **CLEARED**, and the highlighting is removed. You can query alert data, including the problematic pipeline, alert type, and other details, for the last 5 days with a time range of less than 24 hours.

Not cleared:

![img](https://main.qcloudimg.com/raw/a76c4bb27dd86c6e2d06f2dd6ccbb42e.png)

Cleared:

![img](https://main.qcloudimg.com/raw/4a986687ccdf97ce0e222aac2b936fb6.png)

The **Heath** tab displays channel input (bandwidth and input video/audio frame rate) and output (bandwidth) information as well as corresponding charts, which help you determine whether the current channel is working properly. You can query data for the last 5 days with a time range of less than 24 hours.

![img](https://main.qcloudimg.com/raw/e49e312b0d134d0d9fb1c8dccbcee00b.png)
![img](https://main.qcloudimg.com/raw/de84757254338b428e55695b4b3a2170.png)


### Configuring a plan

You can configure plans for StreamLive channels to perform specified events at scheduled time, for example, switch to input2 at 15:00:00.

Under the **Channel Management** tab, click the name of the channel to go to its details page, select **Plan**, and click **Create Event** to add an event.

1. You can select either the fixed time or immediate mode to trigger an event. In the fixed time mode, you need to manually set an event trigger time. In the immediate mode, the event is performed immediately after creation.
2. For **Event Type**, only **Input Switch** is supported currently. You can select a target input.

Click **Confirm**.

![img](https://main.qcloudimg.com/raw/b45ec0b7275bc1c4363bd683652dd541.png)

![img](https://main.qcloudimg.com/raw/cb4c8a9d4f289072476364297346fb4d.png)

>!
> - The time entered must be the local time and cannot be earlier than the current time.
> - If the pull mode for the MP4_PULL/HLS_PULL input that is switched to is ONCE, the input will be disconnected after the first pull, and the event will not be triggered again.

The events created are listed chronologically by trigger time. You can view or delete an existing event as well as create an event.

>! Events created cannot be modified.

### Channel configuration best practices

StreamLive also provides a wide range of custom features, as described in the following best practice guidelines:

[Channel DRM Configuration via DRMtoday](https://intl.cloud.tencent.com/document/product/1048/45217) 
[StreamLive Outputting to COS](https://intl.cloud.tencent.com/document/product/1048/45218)
[StreamLive Outputting to StreamPackage](https://intl.cloud.tencent.com/document/product/1048/45218)
[Live Streaming Time Shifting via StreamLive](https://intl.cloud.tencent.com/document/product/1048/45220)

