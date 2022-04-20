### How do I connect to ASR?
ASR currently supports connection via API and SDK (recommended). For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/1118/43355).

### How do I try out the features of ASR?
To try ASR out, search for "Tencent Cloud AI Voice" on WeChat Mini Program and select ASR, or upload files or use URLs in the feature trial module in the [ASR console](https://console.cloud.tencent.com/asr).

### What factors affect the accuracy of speech recognition?
Factors such as being far away from the mic, obvious noise, and heavy accent affect the accuracy of speech recognition.

### How do I view audio format and attributes?
**Windows**:
You can download software tools such as Adobe Audition CS6 to view and modify the audio format.
**Linux or macOS**:
Use the **file** command, such as **file test.wav**.
Result:
![](https://main.qcloudimg.com/raw/769ec09e032d1a3d8b03749fe2039f34.png)
The sample rate of this audio is 8 kHZ, the bit depth is 16-bit, and the channel is mono (as compared to stereo).

### How do I update a file over 5 MB in size to the ASR console to try ASR out?
The ASR console provides a feature trial module for you to try ASR out. If your test audio file is large, we recommend you upload it to a URL and keep the audio length below 5 hours.

### How long does it take to convert a recording file to text and return the text?
The result return time is subject to factors such as network and audio length and needs to be determined according to the parameters.
