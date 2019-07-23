You can record a live streaming channel through APIs. For more information, see [Creating a Recording Task](https://intl.cloud.tencent.com/document/product/267/30847).
After the recordings are converted to VOD, the recording files will be automatically stored on the VOD platform. Therefore, before using the recording feature, you need to activate the VOD service first and purchase storage capacity and traffic for storing and playing back recorded video files. 

Select **Feature Template** > **Recording Configuration** in the left sidebar in the LVB Console and click "+".
![](https://main.qcloudimg.com/raw/1c3f2c9b2ff45a9e67522a75e5213c18.png)
Set the basic information.
![](https://main.qcloudimg.com/raw/e9fc563c3fba24ffc85f29b88b85adab.png)

The .hls format supports recording resumption after push interruption, and the timeout period for resumption can be set between 0 and 300 seconds.

**Specifications:**
1. Videos are recorded based on the original bit rate of the live stream and can be outputted in .hls, .mp4, .flv, and .acc formats. The .acc format records only the audio.
2. The maximum length of a single file recorded in .mp4 or .flv format is 120 minutes, and if a file exceeds this limit, a new file will be created to continue to record. There is no upper limit for the .hls format.
3. A single recording file can be retained up to 10,000 days.
4. During the live streaming, you can obtain a recording file in about 5 minutes after the recording process is ended. For example, if you start recording a live stream at 12:00, the corresponding clip for 12:00 to 12:30 can be obtained at around 12:35.

**Associate a domain name**
After creating a recording template, you need to select the corresponding push domain name in **Domain Name Management** and go to **Template Configuration** to specify the recording template for the domain name.
![](https://main.qcloudimg.com/raw/8f024817b2c842fcf00139558984a1a2.png)


>- If you want to unbind the recording configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>[](https://main.qcloudimg.com/raw/f5dbc62a52e371bdf5e70f6a891930fa.png)
>- The recording templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated a specified stream through the recording management API and want to disassociate it, you need to call the [recording template deletion API](https://intl.cloud.tencent.com/document/product/267/30842) to do so.
