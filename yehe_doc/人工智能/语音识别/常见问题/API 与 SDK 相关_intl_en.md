### What should I do if HTTP requests to ASR APIs return an authentication failure?
Check whether your parameters are uploaded correctly against the parameter table. For quick connection, we recommend you use the SDK provided at our official website.

### What should I do if a recognition result error is reported due to invalid URL in ASR?
The URL you provide must be a public network URL accessible by Tencent Cloud. You can use Tencent Cloud COS to store audio files and use relevant URLs. You also need to check whether the firewall is blocking access, whether the URL is at a private IP, and whether the audio files stored at other service providers can be downloaded by Tencent Cloud properly.

### What should I do if "Unregistered AppId" is reported during ASR API call?
You are not registered yet. To use ASR, you must activate it first as instructed in Getting Started. 

### Do ASR APIs have restrictions on the sample rate of audio files?
APIs don't restrict the sample rate of audio files, but if the sample rate is non-compliant, the recognition effect will be compromised.
