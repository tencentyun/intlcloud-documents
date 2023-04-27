After creating an audio/video experience monitoring task successfully, you can analyze the overall audio/video performance on the **Test Statistics** page.

## Directions
1. Log in to the [CAT console](https://console.cloud.tencent.com/cat/probe/tasklist).
2. Click **Test Statistics** on the left sidebar and select **Audio/Video experience**.
3. On the **Test Statistics** page, analyze the test data in multiple dimensions such as map, line chart, figure, and detailed data.

## Metric description

| Metric               | Description                                                     |
| ------------------- | ------------------------------------------------------------ |
| Duration of the first buffer (s)   | Duration of the first buffer = time to first frame – time to first video packet <br>Lag duration: The cumulative duration of lag (buffer) after the start of video playback (excluding the first buffer). |
| Total buffer duration (s)     | Total buffer duration = duration of the first buffer + duration of lag 1 + duration of lag N.                |
| Total buffers          | Total number of buffers = first buffer + number of lags.                                 |
| Time to first video packet (s)   | The time from getting the actual video address to getting the first video packet.      |
| Average download speed (KB/s) | The speed at which the player downloads video resources during playback: <br>Average download speed = total number of downloaded bytes / throughput duration. |
| Availability (%)           | The percentage of successful streaming media tasks to the total number of test tasks.                   |
| Time to first frame (s)   | The time from getting the actual video address to playing back the first video frame.      |
| Total buffer duration (s)     | Total buffer duration = duration of the first buffer + duration of lag 1 + duration of lag N.                |
| Lag duration (s)       | The cumulative duration of lag (buffer) after the start of video playback (excluding the first buffer).<br> Lag duration = total buffer duration – duration of the first buffer. |
| Percentage of lag duration (%)   | The ratio of the lag duration to the total playback duration, i.e., lag duration / total playback duration (up to 60s). |
| Lag rate (%) | Lag rate = total number of lag samples / number of valid test tasks. Total number of lag samples: Total number of samples buffered again during the playback of all videos. |
| Errors     | Number of failed access requests in the test.                                           |
| Top 5 error types       | The top five error types of the most errors.                             |
| Top 5 slowest ISPs     | The top five ISPs with the longest total buffer duration.                               |
| Resource DNS time | The time taken to resolve the domain of the resource server when the player downloads video resources. |
| Resource TCP connection duration | The time taken to establish a TCP connection when the player downloads video resources. |

