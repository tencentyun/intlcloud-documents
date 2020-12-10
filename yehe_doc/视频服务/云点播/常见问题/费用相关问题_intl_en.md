### How do I change my VOD billing mode?
VOD offers two billing modes: daily billing and monthly billing. The default billing mode is daily billing. If you want to change it to monthly billing, please contact your Tencent Cloud rep.
>?Packages fall into the daily billing mode.

### Why are fees still incurred after I purchase a resource package?
After you purchase a resource package, there will be no additional fees incurred on the purchase date. As fees for a day are charged on the next day in the daily billing mode, the additional fees on the package purchase date are actually for the previous day.

### Will fees be incurred repeatedly if a video is watched with the same device ID multiple times a day?
Yes. Every time a video is watched with the same device ID through the VOD link, there will be traffic consumed, and fees will be incurred accordingly.

 ### Will billing continue after a video is transcoded?
Each transcoding task is billed only once. A transcoded video will be billed another time only if it is transcoded again.

 ### Why do I receive deduction notifications during the validity period of a resource package?
There are many possible reasons. You can simply troubleshoot as follows:
- Check in the console whether the package is used up; and if yes, fees will be billed daily.
- Check whether the correct billable items are deducted; for example, traffic can be deducted only by a traffic resource package, while transcoding duration can be deducted only by a transcoding resource package.
- Transcoding resource packages purchased before February 12, 2020 are legacy packages and cannot be used for video transcoding to 1080p or lower.
- If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### How do I calculate the accelerated traffic in VOD?
Accelerated traffic = bitrate * duration * number of viewers. You can use this formula to estimate how much traffic will be needed.
For example, if a video lasts for one hour at a bitrate of 500 Kbps and is watched by 100 users, the traffic consumed will be about 500 / 8 * 3600 * 100 = 22,500,000 KB = 22.5 GB

### Are transcoding fees and task flow fees the same thing?
A task flow is to perform multiple template tasks at a time by splicing them. The tasks contained in the task flow are charged at the same prices as the corresponding billable items.

