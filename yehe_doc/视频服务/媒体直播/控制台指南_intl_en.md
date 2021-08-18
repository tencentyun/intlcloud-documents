## Overview

StreamLive is a premium stream processing platform newly launched by Tencent Cloud, which provides broadcast-grade and real-time live stream processing services. It uses Tencent Cloud's proprietary high-performance video encoding and compression algorithms to reduce transfer traffic consumption while delivering a better watch experience.

The StreamLive service is managed at the channel level in the StreamLive console. You can set up high-quality video streams and distribute them to various types of devices.

## Console Overview

The StreamLive service is managed at the channel level in the StreamLive console via three modules: security group, input, and channel. The security group module allows you to manage the security verification of inputs; in the input module, you can select the protocol and input method (push or pull) of an input; the channel module is the main module of StreamLive, via which you can perform various video processing operations such as transcoding and remuxing and send the results to the specified destination or store them on COS.
![](https://main.qcloudimg.com/raw/e76d930fd73f010632e9e4571a8351d9.png)

## Prerequisites

Log in to the [StreamLive console](https://console.cloud.tencent.com/mdl/security).

## Directions

### 1.   Select a region
Currently, StreamLive is available in three AZs: Mumbai (India), Bangkok (Thailand), and Seoul (Korea), which you can choose as needed. AZs such as Tokyo (Japan) will be available soon. If you need to use the service in other AZs, please [contact us](https://intl.cloud.tencent.com/contact-sales).
![](https://main.qcloudimg.com/raw/c9da8ddd469f557487c5b6d943ef69af.png)

### 2.   Create a security group
A security group is used to verify the validity of an input source's IPv4 address, which makes the input of StreamLive channels more secure.

Select "Security Group Management" and click "Create Security Group". Enter a name, and add IPs to the allowlist (the IPs must be in CIDR block format, separated with commas or line breaks). Then, click "Confirm" to complete the creation.

![](https://main.qcloudimg.com/raw/e5c7365ba3724802b2013b3c25cdc07b.png)

>?
>- The status of a security group can be either "idle" or "occupied".
>- "Idle" indicates that a security group is currently not associated with an input and can be edited and deleted.
>- "Occupied" indicates that a security group is currently associated with an input and can only be edited, not deleted.
>- You can create up to 5 security groups in the console by default. If you need more security groups, please [submit a ticket](https://console.cloud.tencent.com/workorder).

### 3.   Create an input

Select "Input Management" and click "Create Input".

Inputs are the source of streams for StreamLive channels. An input is usually associated with 1 security group and 1 StreamLive channel. Currently, the protocols supported for inputs include RTP, RTP-FEC, RTMP, UDP, HLS, and HTTP-MP4. An input is either a push input or a pull input.

Each input can be associated with 1 security group and 1 channel. An input associated with a channel is marked as "attached".

![](https://main.qcloudimg.com/raw/eed9a73cc25fc646b1f601ac545ccc0e.png)

>?
>- The console supports up to 5 inputs by default.
>- An input source must contain at least 1 video data channel.
>- When MPEG-TS multiplexing is used, a maximum of 8 channels can be transferred simultaneously.

### 4.   Create a StreamLive channel

1. Select "Channel Management" and click "Create Channel".

2. Enter a custom channel name, which is used to identify different channels created, and click "Next Step".

![](https://main.qcloudimg.com/raw/824d8ad80106fb65f69df5dffae7bd0b.png)

3. Attach one or more of the inputs created to the channel. **The first input attached is used by default.** Other inputs may be used in failover or when an event is triggered. You can attach up to 5 inputs to a channel, including 2 push inputs.

![](https://main.qcloudimg.com/raw/72974873310b8f07ea0acc09ce3c3f64.png)

Click "Settings" to configure an input:

a. "Audio Selector": If there are multiple audio streams in your RTP_PUSH/RTP-FEC_PUSH/UDP_PUSH inputs, you can create a selector using the PID encapsulated in MPEG-TS so that you can configure multiple audio languages for outputs.

![](https://main.qcloudimg.com/raw/8ea9e3a78e57242e446f4ab2f4cd6850.png)

>!
>- The PID must be the same as that of the input audio stream; otherwise, the transcoding task may fail.
>- You can configure audio selectors only for the first input attached. If a plan is configured and another input is used instead of the first one, StreamLive will randomly select an audio stream to transcode.
>- If input source failover is enabled, the audio selectors configured for the primary input will be automatically applied to the backup input to ensure the availability of the audio encoding feature in case of failover.

 

b. "Pull Input Configuration": You can select either the "LOOP" or "ONCE" mode for MP4_PULL/HLS_PULL inputs. "LOOP": the pull loops; "ONCE": the input is disconnected after the first pull.

![](https://main.qcloudimg.com/raw/a721d60a7263dddeab3927b3331cfaa2.png)

c. "Failover Configuration": You can enable failover for RTMP_PUSH/RTP_PUSH inputs so that StreamLive switches automatically to the backup input when the primary one fails. After enabling failover for an input, you can select for it a backup input, set a downtime threshold (the wait time after the primary input is down before failover is triggered; 3000 ms by default), and select the input preferences, i.e., whether to switch back to the primary input after it recovers ("PRIMARY_PREFERRED": the primary input is prioritized; "EQUAL_PREFERRED": the primary and backup inputs have the same priority).

![](https://main.qcloudimg.com/raw/588efa49ee40b158793421c6ced77319.png)

![](https://main.qcloudimg.com/raw/ebc0d3305a94534edaf97d09ecf18f9c.png)

>?
>- You can configure only 1 backup for an input. The primary and backup inputs must be of the same type and have the same number of pipelines.
>- Once an input is used as a backup, the failover feature will be disabled for the input automatically, which means that you cannot configure a backup for this input. To make modifications (for example, if you want to switch the role of the two inputs), you must remove the primary/backup relationship between the inputs first.
>- After successful configuration, "Primary" and "Backup" will appear next to the names of the primary and backup inputs.
>- The backup input will appear below the primary input.

In addition to the above, you can also do the following to an input:

- Click "Details" to view the input address and other basic information of an input.
- Click "Set as First" to pin an input to the top and set it as the default input. Note: you cannot do this to a backup input.
- Click "Delete" to delete an input.

Click "Next Step".


4. Configure output groups.

a. Configure multiple output groups. You can click the "+" icon to configure multiple output groups for a channel.

![](https://main.qcloudimg.com/raw/e6af7ba8a52e288e0d02dc3bea54871e.png)

b. Set the name and type of an output group. Currently, StreamLive supports outputs in HLS and DASH formats. You can output HLS files to COS for archiving (for detailed directions, please see section 5), or output HLS/DASH streams to Tencent Cloud’s StreamPackage under the same account (for detailed directions, please see section 6). This allows you to build your own origin server for stable and large-scale distribution of live streams.

>?
>- For more information on COS, please visit: [COS details](https://intl.cloud.tencent.com/document/product/436/6222)
>- For more information on StreamPackage, please visit:[StreamPackage details](https://intl.cloud.tencent.com/document/product/1063/41786)

![](https://main.qcloudimg.com/raw/6b87cbe42011cc98c045af99369348a3.png)

c. Set a CDN streaming address. If an HLS or DASH output is used, you can set the destination to a CDN URL. Enter the verification information if the URL requires verification.

![](https://main.qcloudimg.com/raw/8fb39dfab5a32ea34444b9a6f1e4edab.png)

d. Configure segments. Set the segment duration and quantity in your "manifest" file. If you want to insert UTC time into the tag file, enable "PdtInsertion" and set "PdtDuration" (time interval for insertion).

![](https://main.qcloudimg.com/raw/36b16a1dda37c530d7b8f497688a93d9.png)

e. Configure DRM. You can use third-party DRM services in StreamLive.

![](https://main.qcloudimg.com/raw/fbb528cc453be167497d4d7eca823d43.png)

>? If you select HLS/HLS_ARCHIVE/HLS_StreamPackage for "Output Group Type" and enable DRM, FairPlay encryption will be used. If you select DASH/DASH_StreamPackage and enable DRM, Widevine encryption will be used.
>- FairPlay encryption settings: If you select HLS/HLS_ARCHIVE/HLS_StreamPackage as the output type, FairPlay will be used as the encryption method. You need to enter the FairPlay Content ID (key ID), key, and IV (both key and IV are 32-character hexadecimal strings).
![](https://main.qcloudimg.com/raw/e172623be22b4397d9f4964d90e8eb03.png)
>- Widevine encryption settings: If you select DASH/DASH_StreamPackage as the output type, Widevine will be used as the encryption method. You need to enter the Widevine content ID and set the tracks. Track types include SD, HD, UHD1, UHD2, and AUDIO.
>-  If you select "All Track", you can set the same key ID and key for all five track types.
![](https://main.qcloudimg.com/raw/06b22ae97702570f7bdfac4161219ece.png) 
>- You can also click "Select Track" to set a key ID and key for each track type.
![](https://main.qcloudimg.com/raw/9c9e6b56980d6c87aea64c2b3b426ad5.png)

f. Set audio transcoding. You are allowed to configure multiple audio transcoding schemes with one output unit. Create an audio template, specifying the name, transcoding format, bitrate, and audio language. If no audio selector is associated, the default stream in the input will be transcoded. Currently, the bitrate range supported for audio transcoding is 6000-1024000 bps. Language code is a 3-character code for the audio language to use, whose naming follows the ISO 639 standard.

![](https://main.qcloudimg.com/raw/c092adee1a2aeca7f9e98f18659b4aef.png)

g. Set video transcoding. Create a video template, specifying the name, encoder type (only H264 is supported currently), bitrate (value range: 50000-40000000 bps), resolution, frame rate, etc. Top speed codec transcoding is a high-performance video transcoding service developed by Tencent Cloud. It uses AI algorithms to calculate in real time the optimal encoding parameters based on the business scenario to ensure high-quality transcoding at low bitrate. Bitrate compression ratio is the percentage by which video bitrate is expected to be reduced.

![](https://main.qcloudimg.com/raw/92242c0a054e342a1071794db28600de.png)

>? You can enable top speed codec if you want a better codec with smart video compression algorithms. It uses AI algorithms to calculate in real time the optimal encoding parameters based on the business scenario to ensure high-quality transcoding at low bitrate.

h. Assemble outputs by combining the audio and video transcoding templates created. You can enable SCTE-35 to pass SCTE-35 information in HLS or DASH file tags.

![](https://main.qcloudimg.com/raw/9e2db2401085804c20ea520364f43c3a.png)

i. Click "Done" to save the configuration.

![](https://main.qcloudimg.com/raw/1874e5ebae643cddbe8f41c00bc92731.png)

j. Click "Start" to run the channel created.

![](https://main.qcloudimg.com/raw/ec0fe249551d5db6d80697a1c5d47d36.png)

### 5.   Output content to COS for archiving through StreamLive

StreamLive allows you to output HLS files to COS for archiving, for which you need to create a bucket in COS first and grant StreamLive access to the bucket.

1. Activate the COS service and create a COS bucket.

Before outputting content to COS for archiving, please make sure that you have [activated the COS service](https://console.cloud.tencent.com/cos5). Then, select "Bucket List" in the [COS console](https://console.cloud.tencent.com/cos5) and click "Create Bucket" to create a COS bucket in a nearby region.

![](https://main.qcloudimg.com/raw/258a128f8e010886f7bea5b6dac83c72.png)

2. Set the output type to "HLS_ARCHIVE". Return to the StreamLive console, and select "HLS_ARCHIVE" for "Output Group Type".

![](https://main.qcloudimg.com/raw/5e782e85e27d4f860d9921cc86f1165f.png)

3. Authorize StreamLive to access the COS bucket. As you have not granted StreamLive access to your COS bucket, the COS destination fields are grayed out and cannot be entered. Click "click here" as instructed, and an authorization dialog box will pop up. Click "Authorize Now" to enter the authorization page, and then click "Grant" to complete the authorization.

![](https://main.qcloudimg.com/raw/5327f143f1fc7482c68225e8abad3c82.png)

![](https://main.qcloudimg.com/raw/3b3a91b1e9053f9ac0b6c9bc2955e12c.png)

After completing the authorization, return to the StreamLive console and click "Authorization completed". The COS destination fields are now editable.

![](https://main.qcloudimg.com/raw/ee8f5a51ec6fb2642e570a9c67f91865.png)

![](https://main.qcloudimg.com/raw/41fc5c9c4a18d04b54f6585241231688.png)

4. Enter the COS URL for archiving based on the COS bucket created, which is in the format of http://<BucketName-APPID>.cos.<Region>.myqcloud.com/path.

5. Submit the configuration. Proceed with other channel configurations in section 4-4 and then submit the configurations.

### 6.   Output content to StreamPackage through StreamLive

You can use StreamLive together with StreamPackage and output HLS/DASH live streams directly to StreamPackage under the same account. This allows you to build your own origin server for video distribution and playback.

1. Activate StreamPackage.

Before you output content to StreamPackage, please [activate StreamPackage](https://console.cloud.tencent.com/mdp/channel) first.

2. Create a channel.

Click "Create Channel" in the top-left corner to create a channel. Enter a channel name. For "Input Protocol", select the same protocol as the output type; for example, if the output type is "HLS_StreamPackage", select `HLS`.

>! StreamLive and StreamPackage must be in the same region.

![](https://main.qcloudimg.com/raw/ca0ae9e483499e4489a8db47b7bb290b.png)

3. Create an endpoint.

After creating the channel, you will enter its details page, where you can create an endpoint and select whether to enable IP blocklist/allowlist or authentication.

![](https://main.qcloudimg.com/raw/da2c4f2cefcbb73aa5ba68f75579937c.png)

4. Get the endpoint address and channel ID.

The URL of the endpoint created is the playback/origin server address.

![](https://main.qcloudimg.com/raw/30594049a37593a5d8827990bd9a13a1.png)

>? You will need the channel ID when configuring outputs in StreamLive.
![](https://main.qcloudimg.com/raw/c66b1bb5f1c9f570225310e66f8e0a66.png)

5. Set output type to "HLS_STREAMPACKAGE" or "DASH_STREAMPACKAGE".

Return to the StreamLive console, based on your needs and the type of the StreamPackage channel just created, select "HLS_STREAMPACKAGE" or "DASH_STREAMPACKAGE" for "Output Group Type", and enter the channel ID in StreamPackage.

![](https://main.qcloudimg.com/raw/486e54380f8bbecd2430c01ad8265c86.png)

6. Submit the configuration. Proceed with other channel configurations in section 4-4 and then submit the configurations.

### 7.   Import, export, clone, edit, or delete a channel

StreamLive allows you to import/export a channel configuration file and clone an existing channel.

1. Export a channel.

All created channels and their states are displayed in "Channel Management" of the StreamLive console. Click "Export" in the "Operation" column to quickly export a JSON file of the channel configuration.

![](https://main.qcloudimg.com/raw/764c7eea7b0ea222364a5b4dad88eb41.png)

![](https://main.qcloudimg.com/raw/e67829bbee59c2148ba68ae1e652f8da.png)

2. Import a channel.

Go to "Channel Management" and click "Create Channel". Click "Import Configuration", and select a modified JSON file of channel configuration.

After the import, you will enter the channel editing page. Complete the rest of the configurations and submit them.

![](https://main.qcloudimg.com/raw/1fe8fdf4c50c5be5a6fe1dc820f5469f.png)

>?
>- Channel importing is a quick configuration process. Based on the JSON file imported, StreamLive can complete the "Basic Information" and "Output Group Setting" steps for you, but not "Input Setting". You need to select an input. Therefore, please create a new input in advance if you want to create a channel through channel importing.
>- If you import a new configuration file when editing a channel, the existing configurations will be overwritten.

3. Clone a channel.

Channel cloning is essentially a quick channel exporting and importing process. Go to "Channel Management", and click "Clone" in the "Operation" column to clone the channel and enter its configuration page.

StreamLive will complete the channel configurations (except "Input Setting") automatically according to the cloned channel. Complete the rest of the configurations and submit them.

![](https://main.qcloudimg.com/raw/92bf580af5c4f013363915688744f1f6.png)

4. Edit or delete a channel.

A channel in "RUNNING" state cannot be edited or deleted. To edit/delete it, click "Stop" to stop it first.

![](https://main.qcloudimg.com/raw/57923bc62f83d99ee10df572bebbb6e3.png)

### 8.   Monitor channel quality

Click a channel in "Channel Management" to go to its details page, where you can view its input, output, alerts, health, and other information.

![](https://main.qcloudimg.com/raw/c97468a3a9fbeb51e9c15ae552d53efd.png)

If a problem occurs or is likely to occur in any pipeline of a channel, StreamLive will generate an alert for the channel. "Set time" is the time when the alert is generated, and "Cleared time" is the time when the alert is cleared. The state of an alert changes. When the alert state is "SET", the "Set time" and "State" columns are highlighted in red. After an alert is cleared, its state changes to "CLEARED", and the highlighting is removed. You can query alert data, including the problematic pipeline, alert type, and other details, for the last 5 days with a time range of less than 24 hours.

Not cleared:

![](https://main.qcloudimg.com/raw/a76c4bb27dd86c6e2d06f2dd6ccbb42e.png)

Cleared:

![](https://main.qcloudimg.com/raw/4a986687ccdf97ce0e222aac2b936fb6.png)

The "Heath" tab displays channel input (bandwidth and input video/audio frame rate) and output (bandwidth) information as well as corresponding charts, which help you determine whether the current channel is working properly. You can query data for the last 5 days with a time range of less than 24 hours.

![](https://main.qcloudimg.com/raw/e49e312b0d134d0d9fb1c8dccbcee00b.png)

![](https://main.qcloudimg.com/raw/de84757254338b428e55695b4b3a2170.png)

 

### 9.   Configure plan

You can configure events for StreamLive channels to perform specified actions at scheduled time, for example, switch to input_2 at 15:00:00.

Under the "Channel Management" tab, click the name of the channel to go to its details page, select "Plan", and click "Add" to add an event.

1. You can select either the fixed time or immediate mode to trigger an event. In the fixed time mode, you need to manually set an event trigger time. In the immediate mode, the event is performed immediately after creation.

2. For event type, only input switch is supported currently. You can select an input to switch to.

Click "Create" to finish the configuration.

![](https://main.qcloudimg.com/raw/b45ec0b7275bc1c4363bd683652dd541.png)

![](https://main.qcloudimg.com/raw/cb4c8a9d4f289072476364297346fb4d.png)

> !
>- The time entered is local time and must not be earlier than the current time.
>- If the pull mode for the MP4_PULL/HLS_PULL input that is switched to is ONCE, the input will be disconnected after the first pull, and events will not be triggered again.

The events created can be listed chronologically by trigger time. You can view or delete an existing event as well as create an event.

>! Events created cannot be modified.
