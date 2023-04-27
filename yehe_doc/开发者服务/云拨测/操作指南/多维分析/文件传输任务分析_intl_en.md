After creating a file transfer (upload/download) test task successfully, you can analyze the overall file transfer performance on the **Test Statistics** page.

## Directions

1. Log in to the [CAT console](https://console.cloud.tencent.com/cat/probe/tasklist).
2. Click **Test Statistics** on the left sidebar and select **File transfer**.
3. On the **Test Statistics** page, analyze the test data in multiple dimensions such as map, line chart, figure, and detailed data.

## Metric description

| Metric               | Description                                                     |
| -------------------- | ------------------------------------------------------------ |
| Average transfer speed (KB/s) | The average speed of downloading or uploading the target file:<br>Average transfer speed = number of bytes actually downloaded or uploaded / transfer duration. |
| Time to first packet (s)        | Download: The time taken by the client to receive the first response packet from the server after initiating a download request. <br>Upload: The time taken by the client to send a packet after initiating an upload request. |
| Success rate (%)          | The ratio of successful transfers to the total number of transfers.                             |
| Transferred file size (KB)       | Total number of uploaded or downloaded bytes, subject to the task type.                    |
| Errors | Number of error data samples.                                           |
| Valid tests | Number of valid data samples.                                           |
| Transfer duration (s)       | Download: The time taken to download the target file.<br>Upload: The time taken to receive the target file sent by the client. |
| DNS time   | The time taken to convert an input domain to an IP.                           |
| TCP time              | The time taken to establish a TCP connection when the target file is downloaded or uploaded.              |
| Top 5 error types       | The top five error types of the most errors.                             |
| Top 5 slowest regional ISPs     | The top five ISPs with the lowest average transfer speed.                               |
