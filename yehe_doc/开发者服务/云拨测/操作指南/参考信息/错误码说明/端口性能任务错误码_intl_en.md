This document describes the error codes for CAT API monitoring tasks. The following error codes, if any, will be counted into top five error types in testing statistics.

| Error Code | Definition                 | Description                                                         |
| ------ | ------------------------ | ------------------------------------------------------------ |
| 600    | DNS resolution failed.          | This error code will be reported if the network is abnormal or the DNS server or domain is incorrect. |
| 601    | Server connection failed.         | Currently, only TCP-based protocols are supported for protocol monitoring. This error code will be reported if server connection times out after socket creation. The timeout period can be configured in the task.  |
| 602    | Failed to send the network data.        | The network is disconnected.                                                     |
| 603    | No response was received after connection to the server.       | This error code will be reported by the client if no data is received or data receiving times out after request sending. |
| 604    | Task execution timed out.             | The protocol test allows for sending protocol packets multiple times to the remote server. This error code will be reported if the time taken to send the protocol packet once exceeds the configured time limit. The time limit can be configured flexibly on the platform. |
| 605    | The data to be sent configured in the task is invalid. | Currently, the protocol test supports sending text or buffer. In text mode, data is sent without conversion. In buffer mode, the client needs to convert text into a hex buffer. This error code will be reported if an error occurs during the conversion. |
| 606    | The data to be verified configured in the task is invalid. | The protocol test will verify the content returned by the server in four ways: no verification, full match, partial match, and MD5 (recommended if the returned content is large in size). If the buffer mode is set, the content needs to be converted to a hex buffer for verification. This error code will be reported if an error occurs during the conversion. |
| 607    | Failed to verify the keyword.           | This error code will be reported if no verified keyword is contained in the data returned by the server.                             |
| 608    | SSL handshake failed.           | The port is incorrect or the network is disconnected.                                           |
| 609    | The step timed out.             | If one of the steps in a protocol task times out, no further steps will be performed and this error code will be reported. |
