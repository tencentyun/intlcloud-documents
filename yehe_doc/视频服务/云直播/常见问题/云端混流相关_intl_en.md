<span id="que1"></span>
### What should I do if error code -505 is returned for stream mix after push?
Please wait for about 5 seconds after push starts before starting stream mix.


<span id="que2"></span>
### How do I troubleshoot if the stream mix API returned code -505?
If -505 is reported by the stream mix API, the stream ID has no corresponding data on the LVB backend.
1. You can pull the stream to check whether the stream has been successfully pushed. If the pull succeeds, the push is successful.
2. If the stream can be pulled, but -505 is reported by the API, please check whether the entered `AppID` is correct in the stream mix parameters.

<span id="que3"></span>
### What should I do if the assistant host's voice cannot be heard after stream mix of an audio stream?
Please check whether `input_type` of the audio stream is set to 4.


<span id="que5"></span>
### What will happen if stream mix is not canceled after it is applied for?
The stream mix will continue until the command to cancel it is received.

<span id="que6"></span>
### What will happen if the input stream is suddenly interrupted during stream mix?
If a non-background stream is interrupted, its image will freeze at the last frame. If a background stream is interrupted, the entire video image will freeze. If the interrupted stream is successfully pushed again with the same stream ID within 15 minutes, stream mix will resume automatically.

<span id="que7"></span>
### How do I get the recording stream mix result?
For detailed directions, please see [Creating Recording Task](https://intl.cloud.tencent.com/document/product/267/37309).

<span id="que8"></span>
### Why are there black bars in the video image after stream mix?
Possible causes include:
1. An original stream contains black bars.
2. The output aspect ratio in the stream mix parameters is different from that of an original stream. For example, if the target aspect ratio of stream mix is 16:9, but the original video aspect ratio is 4:3, the stream mix backend will add black bars to the original video to change the aspect ratio to 16:9 for output.

You can prevent black bars in the following two ways:
1. Use the aspect ratio of the input video for the output video.
2. Use cropping parameters as instructed in the cropping feature usage.

<span id="que9"></span>
### Why is the assistant host's video image in the mixed stream not in the expected position?
Generally, this is caused by the change of the resolution of an input stream in stream mix. For example, if the input stream resolution is 1280x720 during stream mix application, but it becomes 2560x1440 after a while, then the output video image will change and in a different position.

>? We recommend you not change the resolution of the input stream during stream mix. If necessary, you should calculate the position parameters and apply for stream mix again.

<span id="que10"></span>
### Can the stream mix output be encoded in H.265?
Currently, stream mix supports only H.264 encoding for the output stream. Even if the input stream is encoded in H.265, the output stream can be encoded only in H.264.

<span id="que11"></span>
### Why is error code -30300 returned after I cancel stream mix twice?
The API for canceling stream mix only needs to be called once and should not be called again after the cancellation succeeds.

<span id="que12"></span>
### When will stream mix be automatically canceled after an input stream is interrupted during stream mix?
Taking mixing two streams as an example, if one stream is interrupted, stream mix will not be canceled automatically. If recording is enabled, recording will also continue. If both streams are interrupted, stream mix will be canceled automatically after 15 minutes.

<span id="que13"></span>
### Why does the video image slightly reverse when stream mix is called?
The implementation mechanism of stream mix will align the video images of different streams as much as possible; therefore, slight reverse may occur during processing. To prevent this from affecting your business, unless necessary, please do not call the stream mix API frequently.

<span id="que14"></span>
### If a host mics off during stream mix, will the stream mix layout automatically change?
No. The stream mix scheduler will not modify your layout parameters. If a host mics off, you need to calculate the layout parameters again and initiate stream mix again.
