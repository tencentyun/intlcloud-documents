Based on the LVB recording capability, the time shifting feature stores the TS segment addresses and TS files separately into the VOD system. A client can replay video content before the current time point by passing in a time parameter through the time shifting domain name.
## How It Works

In a common live broadcast in HLS format, the pushed video content is sliced into multiple TS segments. When a viewer watches it, the TS segment addresses are accessed by requesting the .m3u8 files to get the TS files. In this case, because the TS files are not persisted, the viewer cannot replay the live video content before the current time point.



## Playback Request

The request parameter is in the following format:
```
http://[Domain]/timeshift/[AppName]/[StreamName]/timeshift.m3u8?delay=xxx
```
Here:
* [Domain] is the time shifting service access domain name you registered, i.e., the domain name you added in the VOD Console.
* timeshift is a fixed field.
* [AppName] is the application name. For example, if your application name is `live`, enter `live`.
* [StreamName] is the stream name. Enter the stream name corresponding to your request.
* timeshift.m3u8 is a fixed field.
* delay indicates the relative time shifting duration in seconds. Currently, if this value is less than 90, the backend can adjust it to 90.
For example, if you want to use time shifting to replay the content 5 minutes ago of the stream `SLPUrIFzGPE` in the application `live`, then the request URL is as follows:
```
http://testtimeshift.com/timeshift/live/SLPUrIFzGPE/timeshift.m3u8?delay=300
```
