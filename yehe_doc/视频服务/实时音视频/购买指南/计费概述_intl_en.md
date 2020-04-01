## Billable Items

TRTC fees consist of basic service fees and value-added service fees.

### Basic service fees
Basic services refer to basic TRTC communication services such as audio call, video call, co-anchoring, and low-latency LVB. Call fees generated when you use basic services are called [basic service fees](https://cloud.tencent.com/document/product/647/37097). You can use such services as needed and only pay for what you use.
### Value-added service fees
Value-added services include instant messaging, relayed live streaming, on-cloud recording, On-Cloud MixTranscoding, and porn information detection in video. Each value-added service has its own independent billing rule. Fees generated when you use value-added services are called value-added service fees.
Value-added services are disabled by default and will not be charged if they are not used after being activated. For more information on billing, please see [Value-added Service Fees](https://cloud.tencent.com/document/product/647/32574).

<span id="Type"></span>
## Call Type Description
The call type is determined by the type of data stream received by the recipient.
- Audio call refers to a pure-audio call received by the recipient that has only an audio stream but no video stream.
- Video call refers to a call with video stream and video image that can be properly displayed for the recipient. Video calls have the following definitions: SD (360p), HD (720p), and FHD (1080p) as detailed below:
 - SD (360p) video call: video call received by the recipient with a resolution lower than 640x480, e.g., 640x360.
 - HD (720p) video call: video call received by the recipient with a resolution between 640x480 and 1280x720, e.g., 640x720.
 - FHD (1080p) video call: video call received by the recipient with a resolution between 1280x720 and 1920x1080, e.g., 1920x1080.


<span id="callduration"></span>
## Call Duration Calculation Rules
- Call duration is accurate down to the second, and all calls are aggregated by month to get the monthly total call duration in minutes. Call duration below 1 minute will be calculated as 1 minute.
- Call duration is calculated by summing up the durations of calls received by all recipients.
For example, if A, B, and C had a video call (all at the SD (360p) resolution), A received calls from B and C, B received only the call from A, C received only the call from A, and the call lasted for 10 minutes, then:
 · SD call duration of A = 10 minutes + 10 minutes = 20 minutes
 · SD call duration of B = 10 minutes
 · SD call duration of C = 10 minutes
 Total SD call duration = SD call duration of A + SD call duration of B + SD call duration of C = 20 minutes + 10 minutes + 10 minutes = 40 minutes
- If there is only one person in a room, receipt data will not be generated; therefore, no call duration will be calculated.
- The call type is subject to the type of call actually received by the recipient.
 · If a camera is enabled by the sender and video image is properly displayed for the recipient, the call will be considered as a video call for call duration calculation.
 · If a camera is enabled by the sender, but video image from the sender is disabled by the recipient and only an audio stream is received, the call will be considered as an audio call for call duration calculation.
- For a video call from the same sender, the recipient receives the audio and video streams at the same time. However, only video call duration will be calculated, while no audio call duration will be calculated.
- Screen sharing is a separate channel of video stream, which is equivalent to a virtual user participating in the call only as a sender instead of generating call duration for data receipt. When other users receive the video stream of screen sharing, call duration of each user will be calculated based on their respective duration of data receipt and resolution.
