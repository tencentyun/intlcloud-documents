This document describes the error codes for CAT audio/video test tasks. The following error codes, if any, will be counted into top five error types in testing statistics.

| Error Code | Definition                       | Description                                                     |
| ------ | ------------------------------------------------------- | ------------------------------------------------------------ |
| 601    | DNS resolution failed.          | This error code will be reported if the network is abnormal or the domain is incorrect. |
| 602    | Server connection failed.                                  | This error code will be reported if the network is abnormal or the server does not work properly.           |
| 605    | The network is abnormal during receiving.                                          | The network is abnormal during receiving.                                              |
| 660    | Connection timed out.                                              | This error code will be reported if the server cannot be connected to for a long time due to slow network.      |
| 661    | The URL is invalid.                                             | The URL is invalid. Check whether the configured URL is correct.      |
| 662    | The protocol is not supported.                                            | This error code will be reported, for example, if the URL is `http://www.baidu.com/` and the transfer protocol is HTTP, but HTTP is not supported in the streaming media task. |
| 664    | No resources could be found.                                           | No video resource was scraped during page browsing.                         |
| 665    | Playback failed.                                             | An error occurred while playing back the streaming media.                                |
| 666    | No stream was not found.                                           | The server notified that there was no video stream when the stream was requested.             |
| 667    | The streaming media was not played back within the timeout period.                                        |  The streaming media was not played back within the timeout period.  |
| 669    | The time to first frame exceeds the threshold.                                          | The time to first frame exceeds the threshold set by the server.                  |
| 671    | The video playback was interrupted.                                           | In the M3U8 task, an error occurred in the transport stream (TS) request.            |
| 700    | A serious lag occurred, where the playback duration is shorter than 5% of the monitoring duration and the size of the total download exceeds 5 MB. | -                                                            |
| 701    | A playback status error occurred (the data is insufficient but the obtained data was played back).              | In the M3U8 task, the playback duration exceeds 30 seconds and the buffer data is smaller than 3 MB before the playback. |
| 702    | The duration of the first buffer is too long (exceeding five seconds).                             | The duration of the first buffer exceeds five seconds and the download speed during the first five seconds exceeds 100 KB/s, indicating that data was discarded abnormally. |
| 703    | There are consecutive M3U8 files, with no TS files.                                | 1. There are two or more consecutive M3U8 files (if the interval between their start time is greater than or equal to the refresh cycle, it is abnormal; otherwise, it is normal, as the server did not update the M3U8 files).<br>2. The second M3U8 file starts after the last TS file ends. This error code will be reported if both conditions are met. |
| 704    | The connection failed but the IP is 0.0.0.0.                         | -                                                            |
| 705    | The playback duration exceeds the monitoring duration (the time difference of no greater than five seconds is allowed).             | The device performance is poor; for example, it takes 30 seconds to play back a 20-second video.                    |
| 706    | The playback duration is longer than the total duration of all TS files. | -                                                            |
| 707    | The first playback duration is shorter than the value set in the buffer.                  | -                                                            |
| 708    | The streaming media was buffered too many times, and more than three lags occurred per test minute.            | -                                                            |
