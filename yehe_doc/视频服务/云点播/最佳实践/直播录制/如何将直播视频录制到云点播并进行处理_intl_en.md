Live recording is a solution that stores the files remuxed from original streams (without modifying audio/video data, timestamp etc.) to VOD, and then processes, distributes, plays back the recorded files. For details, see [Live Recording](https://intl.cloud.tencent.com/document/product/1082).

## Features
- Based on the capabilities of CSS, it can quickly record and store live streaming content on the VOD platform for secondary production and distribution.
- Relying on Tencent Cloud's leading AI technologies in audio and video and globally deployed cache nodes, it provides top-notch audiovisual services such as professional and stable live push, transcoding, distribution, and playback that fully meet the requirements for ultra-low latency, ultra-high image quality, and ultra-high performance to sustain massive volumes of concurrent requests.
- It can quickly distribute your live streaming events to various scenarios and applications.
- It is suitable for many industry-specific scenarios such as corporate live streaming, ecommerce live streaming, and education live streaming. It can deliver video content through many channels such as Tencent Video.

## Prerequisites
- You have [signed up](https://intl.cloud.tencent.com/register) and [logged in to](https://intl.cloud.tencent.com/login) a Tencent Cloud account, and completed identity verification. Unverified users cannot purchase instances of live recording to VOD for Chinese mainland.
- You have activated both the CSS and VOD services. If not, please go to [CSS](https://console.cloud.tencent.com/live/livestat) and [VOD](https://console.cloud.tencent.com/vod/overview) consoles to activate.

## Directions
### Step 1. Create a recording template
To use the live recording feature, you need to create a recording template first. The configuration of live recording is saved in the recording template. You can create recording templates with different configurations to record files into different formats or of different durations.
- **Creation in the console**:
   1. Log in to the [CSS console](https://console.cloud.tencent.com/live/config/record) and select **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
![](https://qcloudimg.tencent-cloud.cn/raw/2c70d96915ff91297434a1415aea49d0.png)

   2. Click **Create Recording Template** and select the desired recording file type (select at least one). For more information on the configuration items, please see [Creating a Recording Template](https://intl.cloud.tencent.com/document/product/267/34223).
		![](https://qcloudimg.tencent-cloud.cn/raw/af659794c5324cec4ed060377d74f04b.png)
		
   3. Click **Save** to create a template.
- **Creation through an API**:
You can call the [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) API to create a recording template. The corresponding template ID will be returned after the template is created successfully.

### Step 2. Select a recording scheme
CSS offers the following schemes for calling the live recording feature in different scenarios:

#### Scheme 1. Specified domain name global recording
You can bind your live recording template to a push domain name in the [CSS console](https://console.cloud.tencent.com/live/config/record) or by calling an API, and streams pushed through the domain name will be recorded automatically.

- **Use cases**: show live streaming, e-commerce live streaming, online classroom, and video surveillance.
- **Steps**:
	1. After creating a recording template, you will be prompted to [bind a domain name](https://console.cloud.tencent.com/live/config/record). You can click **Bind Domain Name** and select a push domain name.
![](https://qcloudimg.tencent-cloud.cn/raw/5286148ae522898575744fe54b16938a.png)

   2. In **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click your [live push domain name](https://console.cloud.tencent.com/live/domainmanage) to enter the push details page. Select **Template Configuration** > **Recording Configuration** and click **Edit** to bind the push domain name. For more information, please see [Binding Recording Template](https://intl.cloud.tencent.com/document/product/267/34224).
![](https://qcloudimg.tencent-cloud.cn/raw/c74c5d420b6ed296859532e887541e7c.png)

   3. Pass in the template ID of the recording template and the push domain name through the [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) API.

#### Scheme 2. Specified stream recording
You can bind your live recording template to a specified live stream through an API for recording.

- **Use cases**: event live streaming, exhibition live streaming, sports live streaming, and live streaming through co-anchoring.
- **Steps**: you can create a recording rule through the [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) API by passing in the template ID of the recording template and the target domain name, path, and `StreamName` (exact matching is required). This way you can bind your recording template to a specified live stream.

#### Scheme 3. Specified time period recording
You can set the start time and end time through API calls to initiate a task for recording within the specified time period.

- **Use cases**: news live streaming and event live streaming.
- **Steps**: you can create a recording task through the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API by passing in the template ID of the recording template and the target domain name, path, `StreamName` (exact matching is required), and start time and end time for recording.
-**Example**:
 1. In the simplest case, you only need to specify `StreamName`, `DomainName`, `AppName`, and `EndTime` to record live streams.
The following sample code creates a video recording task in .flv format for 8 AM to 10 AM, August 10, 2020, with 30-minute segments, and the recording files will be retained permanently.
Sample request:
```
https://live.tencentcloudapi.com/?Action=CreateRecordTask&AppName=live&DomainName=mytest.live.push.com&StreamName=livetest&StartTime=1597017600&EndTime=1597024800&TemplateId=0&<common request parameters>
```
 2. You can also specify the recording format, recording type, and storage parameters.
The following sample code creates a recording task in .mp4 format for 8 AM to 10 AM, August 10, 2020, with 1-hour segments, and the recording files will be retained permanently.
 3. Call the [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) API to create a recording template.
 Sample request:
 ```
 https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate&TemplateName=templat&Description=test&Mp4Param.Enable=1&Mp4Param.RecordInterval=3600&Mp4Param.StorageTime=0&<common request parameters>
 ```
 Sample response:
 ```
 {"Response": {"RequestId": "839d12da-95a9-43b2-a9a0-03366d01b532","TemplateId": 17016}}
 ```
 4. Call the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API to create a recording task.
 Sample request:
 ```
 https://live.tencentcloudapi.com/?Action=CreateRecordTask&StreamName=livetest&AppName=live&DomainName=mytest.live.push.com&StartTime=1597017600&EndTime=1597024800&TemplateId=17016&<common request parameters>
 ```

#### Scheme 4. Real-time recording (stream mix-based recording is supported)
You can record any frame of a stream in real time through API calls.

- **Use cases**: scenarios where only segments need to be recorded (or clipped after global recording), such as sports live streaming and game live streaming.
- **Steps**: you can create a recording task through the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API by passing in the template ID of the recording template and the target domain name, path, StreamName (exact matching is required), and end time for recording.
-**Example**:
 ```
 https://live.tencentcloudapi.com/?Action=CreateRecordTask&StreamName=test&AppName=live&DomainName=mytest.live.push.com&EndTime=1597024800&<common request parameters>
 ```

#### Scheme 5. Audio-only recording
You can configure audio recording in .acc format if only audio is pushed.

- **Use cases**: audio live streaming and audio mic connect.
- **Steps**: you can select the .aac format as the recording file type and bind the corresponding push address when creating a recording template.
>!A binding rule will take effect in about 5 to 10 minutes after creation. Any change of the binding rule will not affect live streams that are being pushed and will apply only to new live streams.

### Step 3. Push a live stream
After binding the recording template with the push domain name as instructed in [Step 2](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.80.89.E6.8B.A9.E5.BD.95.E5.88.B6.E6.96.B9.E6.A1.88), generate the corresponding push domain name from the push address and start [CSS push](https://intl.cloud.tencent.com/document/product/267/31558).

After the live stream is over, the recording file will be stored on the [VOD](https://console.cloud.tencent.com/vod/overview) platform.

>?
>- If you have selected "Recording to subapplication" in your recording template, the recording file will be stored in the corresponding subapplication.
>- If you want to call back the address information of the recording file, you need to create a callback template before the push, enter the recording callback address and save it, and bind the target push domain name. For more information, please see [Recording Event Notification](https://intl.cloud.tencent.com/document/product/267/38082).

### Step 4. Get a recording file
You can query and get a recording file through:
- **Recording callback**: before pushing a live stream, you need to configure a callback template (with a [recording callback address](https://console.cloud.tencent.com/live/config/callback)). The file will be sent to the callback server through a callback when the recording file is generated. For more information, please see [Recording Event Notification](https://intl.cloud.tencent.com/document/product/267/38082).
![](https://qcloudimg.tencent-cloud.cn/raw/137836f99132f0619ca4ccb6ca128fed.png)
- **VOD console**: you can query a recording file in the [VOD console](https://console.cloud.tencent.com/vod/media). For more information, please see [Viewing Videos](https://intl.cloud.tencent.com/document/product/266/33895).
- **VOD API**: you can call the [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) API to query files.

### Step 5. Process a recording file
#### Scheme 1. Live recording + automatic transcoding + video playback acceleration
- **Use cases**: the recording file of a live stream can be immediately transcoded and accelerated automatically for viewers to play back on demand. This scheme is suitable for most live streaming scenarios where no video processing is required.
- **Steps**:
	1. When creating a recording template before a live stream is pushed, click **Advanced Configuration** to configure a task flow.
	![](https://qcloudimg.tencent-cloud.cn/raw/643aa06605824bab31016d95a5607099.png)
	2. Bind the template to a task flow created in the VOD console.
	![](https://qcloudimg.tencent-cloud.cn/raw/f2c1fdb36cee77be20e9fa366b1994ca.png)
	3. Push the live stream. For details, see [CSS Push](https://intl.cloud.tencent.com/document/product/267/31558).
	4. After the recording is finished, get the `FileId`.
	![](https://qcloudimg.tencent-cloud.cn/raw/8a70ec2190bde5eb95401ad27b71f9fa.png)
	5. Get the URL for playback.

#### Scheme 2. Live recording + manual transcoding + video playback acceleration
- **Use cases**: if you only want to store the recording file of a live stream to VOD without transcoding it right away, you can create a recording task without adding other operations. If you want to transcode the video later, you can trigger the transcoding operation manually and use the on-cloud clipping feature in combination to achieve better results.

- **Steps**:
	1. Push a live stream. For details, see [CSS Push](https://intl.cloud.tencent.com/document/product/267/31558).
	2. Record the file automatically to VOD.
	3. Get the `FileId`.
	4. Configure a transcoding template or task flow to manually transcode the stream. For details, see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059).
![](https://qcloudimg.tencent-cloud.cn/raw/fef42635495040b17e98868ad9cd911a.png)
	5. Process the video based on your needs.
	6. Get the URL for subsequent playback after the transcoding and processing are finished.

#### Scheme 3. Live recording + adaptive bitrate streaming + video delivery acceleration + superplayer

- **Use cases**: if you have high requirements for video security that cannot be satisfied through HLS encryption, you can use self-adaption and superplayer in combination to further enhance the video security. This scheme is highly suitable for online education and corporate training.

- **Steps**:
	1. Push a live stream. For details, see [CSS Push](https://intl.cloud.tencent.com/document/product/267/31558).
	2. Record the file automatically to VOD.
	3. Get the VOD `FileId`.
	4. Configure a task flow to generate an adaptive bitrate stream. For details, see [Task Flow Settings](https://intl.cloud.tencent.com/document/product/266/14058).
	![](https://qcloudimg.tencent-cloud.cn/raw/461b55df5d688b52d94210f173368ddc.png)
	5. Configure the superplayer: select the adaptive bitrate stream generated for playback.
		![](https://qcloudimg.tencent-cloud.cn/raw/4fe2cb6836caad6861798bc38cde60cd.png)
	6. Play back the video through `FileId`.

