### What languages does GME's voice messaging and speech-to-text service support?
At present, the voice messaging and speech-to-text service activated in the Tencent Cloud Console supports over 120 languages such as Simplified Chinese, English, Traditional Chinese, Japanese, and Korean.


### Can GME's voice messaging and speech-to-text service be used together with voice chat?
Yes. They can be switched by calling the relevant APIs.


### After the API for voice file uploading is called successfully, the `fileid` in the returned value is a URL. How do I use it?
Call the API for file downloading and use this URL to download the file. Specifically, the `fileid` called back upon file upload completion needs to be sent to the server, and other clients can get the voice message through the `fileid`.


### Can offline voice files be downloaded?
After a file is uploaded, a URL will be returned which can be used to download the voice file.

### How long is the validity of an offline voice file?
An offline voice file will be retained on the server for 90 days. Then, the download link to the file will become invalid. If you want to retain the file permanently, please store it on your own server.

### Is there a time limit for offline voice recording?
The voice messaging and speech-to-text service supports recording for 1–60 seconds.

### What should I do if error 8200 is reported when the voice messaging and speech-to-text service is used?
This error is caused by incorrect initialization of the voice messaging and speech-to-text service, and you are recommended to check whether the `appid` and `openid` entered during initialization and authentication are correct.


### What should I do if it takes too long to upload or download an offline recording file?
For the voice messaging and speech-to-text service, if the conversion delay is too high, you are recommended to use the streaming recording API which calls back the returned text.

### Why can't I access the recording file and the error 4101 is reported after I finish recording? Do I need to first create a folder?
Yes. Due to security reasons, you have to create your folder and ensure the file path is correct.
