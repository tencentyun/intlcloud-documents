## Prerequisites

- You [have signed up for](https://intl.cloud.tencent.com/register) and [logged in to](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fcloud.tencent.com) your Tencent Cloud account and completed identity verification.
- You have activated the LVB service. Click here to activate [LVB](https://console.cloud.tencent.com/live/livestat).
- You have activated the VOD service. Click here to activate [VOD](https://console.cloud.tencent.com/vod/overview).



## Directions

<span id="step1"></span>
### Step 1. Create a recording template

To use the LVB recording feature, you need to create a recording template first. The configuration of LVB recording is saved in the recording template. You can create recording templates with different configurations to achieve effects such as different formats and recording file durations.

-  **Creation in the console**:
	1. Go to the LVB console and select **Feature Template** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
	2. Click **Create Recording Template** and select the desired recording file type (select at least one). For more information, please see [Creating Recording Template](https://intl.cloud.tencent.com/document/product/267/34223).
	3. Click **Save**.
- **Creation through an API**:
You can call the [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) API to create a recording template. The corresponding template ID will be returned after the template is created successfully.


[](id:step2)

### Step 2. Select a recording scheme

LVB offers the following schemes for calling the LVB recording feature in different scenarios:

#### Scheme 1. Specified domain name global recording

You can bind your LVB recording template to a push domain name in the console or by calling an API, and streams pushed through the domain name will be recorded automatically.

- **Use cases**: show live streaming, ecommerce live streaming, online classroom, and video surveillance.
- **Steps**:
  - After creating a recording template, click **Bind Domain Name** in the pop-up window and select a push domain name.
  - In **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, select the target push domain name to enter the details page, select **Template Configuration** > **Recording Configuration**, and bind the created push domain name. For more information, please see [Binding Recording Template](https://intl.cloud.tencent.com/document/product/267/34224).
  - Pass in the template ID of the recording template and the push domain name through the [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) API.

#### Scheme 2. Specified stream recording
You can bind your LVB recording template to a specified live stream through an API for recording.

- **Use cases**: event live streaming, exhibition live streaming, sports live streaming, and live streaming through mic connect
- **Steps**: you can create a recording rule through the [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) API by passing in the template ID of the recording template and the target domain name, path, and StreamName (exact matching is required). This way you can bind your recording template to a specified live stream.

#### Scheme 3. Specified time period recording
You can set the start time and end time through API calls to record a stream within the specified time period.

- **Use cases**: news live streaming and event live streaming.
- **Steps**: you can create a recording task through the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API by passing in the template ID of the recording template and the target domain name, path, StreamName (exact matching is required), and start time and end time for recording.

#### Scheme 4. Real-time recording (stream mix-based recording is supported)

You can record any frame of a stream in real time through API calls.

- **Use cases**: scenarios where only segments need to be recorded (or clipped after global recording), such as sports live streaming and game live streaming.
- **Steps**: you can create a recording task through the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API by passing in the template ID of the recording template and the target domain name, path, StreamName (exact matching is required), and end time for recording.

#### Solution 5. Pure audio recording

You can configure audio recording in .aac format if the push is pure audio.

- **Use cases**: audio live streaming and audio mic connect.
- **Steps**: you can select the .acc format as the recording file type and bind the corresponding push address when creating a recording template.

>! A binding rule will take effect in about **5 to 10 minutes** after creation. Any change of the binding rule will not affect live streams that are being pushed and will apply only to new live streams.



<span id="step3"></span>

### Step 3. Push a live stream
1. After binding the recording template with the push domain name as instructed in [Step 2](#step2), generate the corresponding push domain name from the push address and start [LVB push](https://intl.cloud.tencent.com/document/product/267/31558).
2. After the live stream is over, the recording file will be stored on the [VOD](https://console.cloud.tencent.com/vod/overview) platform.

>? 
>- If you have selected "Record to subapplication" in your recording template, the recording file will be stored in the corresponding subapplication.
>- If you want to call back the address information of the recording file, you need to create a callback template before the push, enter the recording callback address and save it, and bind the target push domain name. For more information, please see [Recording Event Notification](https://intl.cloud.tencent.com/document/product/267/38082).

<span id="step4"></span>
### Step 4. Query and get the video recording file

You can query and get a recording file through:

- **Recording callback**: before pushing a live stream, you need to configure a callback template (with a recording callback address). The file address will be sent to the callback server through a callback when the recording file is generated. For more information, please see [Recording Event Notification](https://intl.cloud.tencent.com/document/product/267/38082).
- **VOD console**: you can query a recording file in the VOD console. For more information, please see [Viewing Videos](https://intl.cloud.tencent.com/document/product/266/33895).
- **VOD API**: you can call the [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) API to query a file.



<span id="step5"></span>

### Step 5. Process the recording file

#### Scheme 1. LVB recording + automatic transcoding + video playback acceleration

- **Use cases**: the recording file of a live stream can be immediately transcoded and accelerated automatically for viewers to play back on demand. This scheme is suitable for most live streaming scenarios where no video processing is required.
- **Steps**:
  1. Push a live stream.
  2. Record the file automatically to VOD.
  3. Get the VOD `FileId` and video callback information.
  4. Use the configured template to transcode the recording file automatically.
  5. After the transcoding is completed, get the playback address for subsequent playback.



#### Scheme 2. LVB recording + manual transcoding + video playback acceleration

- **Use cases**: if you only want to store the recording file of a live stream to VOD without transcoding it right away, you can create a recording task without adding other operations. If you want to transcode the video later, you can trigger the transcoding operation manually and use the on-cloud clipping feature in combination to achieve better results.
- **Steps**:
  1. Push a live stream.
  2. Record the file automatically to VOD.
  3. Get the VOD `FileId`.
  4. Configure a task flow and clip the video.
  5. Get the video address for subsequent playback after the transcoding and processing are finished.



#### Scheme 3. LVB recording + adaptive bitrate streaming + video delivery acceleration + superplayer

- **Use cases**: if you have high requirements for video security that cannot be satisfied through HLS encryption, you can use self-adaption and superplayer in combination to further enhance the video security. This scheme is highly suitable for online education and corporate training.
- **Steps**:
  1. Push a live stream.
  2. Record the file automatically to VOD.
  3. Get the VOD `FileId`.
  4. Configure a transcoding template or task flow to perform adaptive bitrate streaming.
  5. Configure the superplayer.
  6. Play back the video through `FileId`.

