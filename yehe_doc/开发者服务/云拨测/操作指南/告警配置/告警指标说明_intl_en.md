This document describes the test metrics for different policies.

### Internet

| Metric | Unit | Description |
| ------------------ | ------------|------------------------------------------------------------ |
| Latency | ms | The time taken by a message or packet to travel from source to the destination, which is subject to the internet routing. If a channel is slow or too crowded, the latency may be high, or data packets may be lost. |
| Packet loss rate | % | The ratio of the number of lost packets to the total number of transferred packets, which may be due to physical line failure, device failure, network congestion, route error, etc. |
| DNS query duration | s | The time taken to convert an input domain to an IP. |

### Browsing

| Metric | Unit | Description |
| ------------------ | ----------|------------------------------------------------------------ |
| Overall performance | s | The time from starting browsing a page to receiving the last packet.  |
| 100 KB time | s | The average time taken to load 100 KB of content, which is calculated as the overall performance / total number of downloaded bytes * 100. |
| Time to first screen | s | The time from entering an URL to rendering an area on the page to a height greater than or equal to the specified height, which is 600 pixels by default. If the height is smaller than 600 pixels, the time is from starting browsing to the IE kernel sending the `Document Completed` event. |
| Overall speed | KB/s | The average speed of loading a page, which is calculated as the total number of downloaded bytes / overall performance. |
| Document completion duration | s | The time from starting browsing a page to parsing the basic document.  |

### Protocol

| Metric | Unit | Description |
| ------------------ | -----------|------------------------------------------------------------ |
| Overall performance | s | The time from the start of the DNS process to the data receiving. |
| Accuracy  | % | The ratio of the data that passed the verification to all the returned data. Passing the verification means passing the verification in the verification method configured in the protocol configuration item. |
| Request duration | s | The time taken to send a protocol request. |
| Response duration | s | The time taken for the client to receive the first response packet from the server after sending the data. |

### Transfer

| Metric | Unit | Description |
| ------------------ | -----------|-------------------------------------------------------- |
| Average transfer speed | KB/s | The average speed of downloading or uploading the target file, which is calculated as the number of bytes actually downloaded or uploaded / transfer duration. |
| Time to first packet | s | Download: The time taken by the client to receive the first response packet from the server after initiating a download request. <br>Upload: The time taken by the client to send a packet after initiating an upload request. |
| Transfer duration | s | Download: The time taken to download the target file.<br>Upload: The time taken to receive the target file sent by the client. |
| DNS query duration  | s | The time taken to convert an input domain to an IP. |
| TCP time | s | The time taken to establish a TCP connection when the target file is downloaded or uploaded. |

### Streaming media

| Metric | Unit | Description |
| ------------------ | -----------|-------------------------------------------------------- |
| Duration of the first buffer | s | Duration of the first buffer = time to first frame - time to first video packet. |
| Total buffer duration | s | Total buffer duration = duration of the first buffer + duration of lag 1 + duration of lag N. |
| Total buffers | - | Total number of buffers = first buffer + number of lags. |
| Average download speed | KB/s | The speed at which the player downloads video resources during playback, which is calculated as the total number of downloaded bytes / throughput duration. |



