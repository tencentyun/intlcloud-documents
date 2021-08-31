## VOD Traffic Usage Estimation
### Example
User A, who runs a video website platform, needs to estimate the traffic consumption for accelerated playback of a video via VOD. The details are as follows:

- Viewers: 100
- Duration: 1 hour
- Video bitrate: 500 Kbps

### Cost estimation
Traffic = bitrate × duration × viewer numbers
>?The user can query the bitrate of the preset template in [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059), and can also define the bitrate of the template.

According to the above formula, traffic consumption in this example ≈ 500/8 KBps × 3600 s × 100 = 22,500,000 KB = 22.5 GB.


## Pay-as-You-Go Cost Estimation for VOD Transcoding
### Example
User A uses a preset template to transcode a video. The details are as follows:

- Input video resolution: 1280 × 640
- Transcoding template: 100030
- Video duration: 100 minutes

### Cost estimation
In the preset transcoding template 100030, the codec is set as H.264, the video will be transcoded into a video with height of 720 px and width scaled proportionally. The resolution of the output video is 1440 × 720. According to [Pay-as-You-Go (Postpaid Daily Billing Cycle)](https://intl.cloud.tencent.com/document/product/266/14666#basic-transcoding), the unit price is 0.0061 USD/min as the height of the output video is 720 px.
Fee in this example = 0.0061 USD/min × 100 min = 0.61 USD

## Pay-as-You-Go Cost Analysis for VOD Storage
### Example
User A needs to use the console to store videos outside Chinese mainland and then distribute them for viewing. The user wants to calculate the daily storage fee.

- Video size: 50 GB
- Storage period: 1 year

### Cost estimation
- Pay-as-you-go (postpaid daily billing cycle):
Total storage fee = 0.0009 USD/GB/day × 365 days × 50 GB = 16.425 USD


