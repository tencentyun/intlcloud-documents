You can record a live streaming channel through APIs. For more information, see [Creating a Recording Task](https://cloud.tencent.com/document/api/267/30148).
After you finish recording, the recording files will be automatically stored on the VOD platform. Therefore, before using the recording feature, you need to activate the VOD service first and purchase the storage capacity and traffic needed for the storage and playback of the recorded video files. For more information, see [Getting Started with VOD](https://cloud.tencent.com/document/product/266/8757).

**Steps:**
Select **Function Template** > **Recording Configuration** in the left sidebar in the LVB Console and click "+".
![](https://main.qcloudimg.com/raw/d59024914f236040d516e220e786e60e.png)
Set the basic information.
![](https://main.qcloudimg.com/raw/c59cbc2ea1cb6b3f35376087da704105.png)
The .hls format supports recording resumption after push interruption, and the timeout period for resumption can be set between 0 and 300 seconds.

**Specifications:**
1. Videos are recorded based on the original bitrate of the live stream and can be outputted in .hls, .mp4, .flv, and .acc formats. The .acc format records the audio only.
2. The maximum length of a single file recorded in .mp4 or .flv format is 90 minutes, and if a file exceeds this limit, a new file will be created to continue recording. There is no upper limit for .hls format.
3. A single recording file can be retained up to 10,000 days.
4. During the live streaming, you can obtain a recording file in about 5 minutes after the recording process ends. For example, if you start recording a live stream at 12:00, you can get the corresponding clip for 12:00 to 12:30 at around 12:35.

**Associate the template with a domain name**
After creating a recording template, you need to select the corresponding push domain name in **Manage Domain** and go to **Configure Template** to specify the recording template for the domain name.
![](https://main.qcloudimg.com/raw/1a7309cc8f0f06ac53390305a4a09685.png)

>?
>- If you want to unbind the recording configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
>![](https://main.qcloudimg.com/raw/22d95e62a0750b419b83dc4d49c1cd83.png)
>- The recording templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the recording configuration with a specified stream through the recording management API and want to disassociate them, you need to call the [Delete Live Record Template API](https://cloud.tencent.com/document/product/267/32612).
