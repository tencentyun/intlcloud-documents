### What languages does GME's voice messaging and speech-to-text service support?
At present, the voice messaging and speech-to-text service activated in the Tencent Cloud Console supports over 120 languages including Simplified Chinese, English, Traditional Chinese, Japanese and Korean.


### Can GME's voice messaging and speech-to-text service be used together with Voice Chat?
Yes, they can be switched by calling the relevant APIs.


### After the API for voice file uploading is called successfully, the fileid in the return value is a URL. How to use it?
Call the API for file downloading and use this URL to download the file.


### Can offline voice files be downloaded?
After a file is uploaded, a URL will be returned which can be used to download the voice file.

### How long is the validity of an offline voice file?
Offline voice files are stored on the server for one week.

### Is there a time limit for offline voice recording?
The time limit ranges from 1 to 60 seconds.

### The error QAVPTTERROR_UPLOAD_APPINFO_UNSET 8200 appears when using Offline Voice, and the prompt is that there is no appInfo configured. How to fix this error?
This error is due to incorrect initialization of Offline Voice, and it is recommended to check whether the appid and openid entered during initialization and authentication are correct.
