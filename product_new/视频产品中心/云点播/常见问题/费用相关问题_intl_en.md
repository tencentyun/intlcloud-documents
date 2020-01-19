### How do I change my VOD billing mode?
VOD offers two billing modes: daily billing and monthly billing. The default billing mode is daily billing. If you want to change it to monthly billing, please contact your Tencent Cloud rep.


### Will fees be incurred repeatedly if a video is watched with the same device ID multiple times a day?
Yes. Every time a video is watched with the same device ID through the VOD link, there will be traffic consumed, and fees will be incurred accordingly.

### Will billing continue after a video is transcoded?
No. Each transcoding task is billed only once. A transcoded video will be billed another time only if it is transcoded again.

### How do I calculate the accelerated traffic in VOD?
Accelerated traffic = bitrate * duration * number of viewers. You can use this formula to estimate how much traffic will be needed.
For example, if a video lasts for one hour at a bitrate of 500 Kbps and is watched by 100 users, the traffic consumed will be about 500 / 8 * 3600 * 100 = 22,500,000 KB = 22.5 GB

### Are transcoding fees and task flow fees the same thing?
A task flow is to perform multiple template tasks at a time by splicing them. The total fees are the same, but a task flow is more convenient.
