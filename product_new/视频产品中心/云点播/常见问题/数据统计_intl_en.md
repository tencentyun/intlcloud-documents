### What statistics can be viewed?
In the VOD Console, you can view statistics of bandwidth/traffic, storage capacity, and transcoding.

- Bandwidth/traffic statistics: details of VOD bandwidth and traffic usage by domain name/region/ISP, top 10 districts for traffic usage, and comparison of ISPs for traffic usage.
- Storage capacity statistics: VOD storage capacity usage over time, including the total number of files and storage capacity currently used.
- Transcoding statistics: types, details, and proportions of transcoding tasks in VOD over time.

In addition, VOD provides data analysis of the number of requests and number of access requests from unique IPs by domain name/region/ISP. For playback statistics, it also supports querying file playbacks by `FileId` and top 100 videos played back.

### What is the number of requests?

The number of requests refers to the number of all playback requests sent to CDN in a certain period of time. This data contains statistics from all sources, including Tencent Cloud Player, webpages, and custom players.
The number of requests is related to the video format: if the format is MP4, it equals to the number of playbacks; if the format is HLS, it equals to the number of requests for M3U8 and TS parts. This value is updated once every five minutes.

### What are the number of playbacks and traffic statistics?
- The number of file playbacks is reported by the Tencent Cloud Player, which only includes statistics of sources using the Tencent Cloud player and is updated once every three hours.
- The traffic statistics are reported by the CDN nodes, which include statistics of all sources (including Tencent Cloud player, webpage, and custom players) and are updated once every hour.

### How are the bandwidth statistics in usage statistics collected?
Each CDN edge server of VOD collects traffic data in real time and reports it to the computing center which aggregates the data into total traffic data of the domain name and displays the converted bandwidth statistics by time duration, used traffic, or time.
- If the total traffic generated in a minute is 6 MB, then the corresponding bandwidth is (6 * 8) / 60 = 0.8 Mbps.
- As the usage for bill-by-bandwidth is calculated based on the statistics at a 5-minute granularity, the corresponding bandwidth value is total traffic in 5 minutes / 300 seconds.


### Why are the traffic statistics displayed in the usage statistics in the console different from those in the log?

The traffic counted based on the downstream bytes in the log of an acceleration domain name in VOD is only about the data at the application layer.
The traffic generated during actual data transfer over the network is around `5–15%` more than application-layer traffic:

- Consumption by TCP/IP headers: in TCP/IP-based HTTP requests, each packet has a maximum size of 1,500 bytes, including TCP/IP headers of 40 bytes, **which generate traffic during transfer but cannot be counted by the application layer**. The overheads of this part is around `3%`.
- TCP retransmission: during normal data transfer over the network, around `3–10%` packets are lost on the internet, and the server will retransmit the lost ones. This type of traffic cannot be counted by the application layer, which accounts for `3–7%` of the total traffic.

As an industry standard, the billable traffic is the sum of the application-layer traffic and the overheads as described above. VOD increases the application-layer monitoring statistics by 10%, so the billable accelerated traffic (as displayed in the usage statistics) is about `110%` of the accelerated traffic calculated in the log.
