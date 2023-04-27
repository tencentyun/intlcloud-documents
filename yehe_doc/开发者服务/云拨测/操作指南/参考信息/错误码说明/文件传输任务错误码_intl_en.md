This document describes the error codes for CAT file transfer tasks. The following error codes, if any, will be counted into top five error types in multidimensional analysis.

| Error Code | Definition                       | Description                                               |
| :----- | :------------------------------------------- | :----------------------------------------------------------- |
| 600    | DNS resolution failed.            | This error code will be reported if the network is abnormal or the DNS server or domain is incorrect. |
| 601    | Server connection failed.                             | HTTP and FTP protocols are supported in the download test. This error code will be reported if server connection times out or encounters an error. |
| 602    | The server refused login.                               | This error code will be reported if the server does not return the 230 response code after the client has sent the username and password during the FTP download. |
| 603    | The request protocol is not supported by the server.                       | This error code will be reported if a non-HTTP or -FTP URL is configured.       |
| 604    | The PASV mode is not supported by the server.                       | The FTP server does not support the PASV mode, which is supported only for CAT's FTP download. |
| 605    | Redirect failed.           | Before the download, CAT will check whether the configured URL in the task has a redirect, and if so, it resolves the target URL before starting one or more download threads. This error code indicates that a TCP-layer but not HTTP-layer error has occurred before the redirect, which is caused by DNS or TCP connection failure in most cases (if the error is an HTTP error, the corresponding HTTP error code will be reported).  |
| 606    | The URL is invalid.                                   | The URL is invalid. Check whether the configured URL is correct.                |
| 607    | The protocol is invalid.                                   | This error code will be reported, for example, if the URL is `http://www.baidu.com/` and the transfer protocol is HTTP, but HTTP is not supported for the task. |
| 608    | The connection to the server was terminated unexpectedly.                         | The connection to the server was terminated.                                       |
| 609    | The connection to the server was reset.                           | The issue is related to the local ISP connection, specifically, poor connection linkage and rate. |
| 610    | The SSL certificate has expired.                  | You need to install the SSL certificate to access HTTPS websites. This error code will be reported if the certificate expires. The system error code is 12037. |
| 611    | The domain in the certificate is incorrect.                              | This error code will be reported if the domain field in the SSL certificate is invalid, for example, the website to be accessed is `www.123.com`, but the domain field is `www.124.com`. The system error code is 12038. |
| 612    | The client certificate is required.                             | The server requires installing the SSL certificate on the client. The system error code is 12044.      |
| 613    | Request sending timed out.                                 | This error code will be reported if no data is returned after a request is sent by the client to the server. |
| 614    | The file does not exist.                                   | The file does not exist on the FTP server.                                   |
| 615    | Failed to open the file.                 | Failed to open the file on the FTP server.                                    |
| 616    | Failed to find the file.                            | Failed to find the file on the FTP server.                                    |
| 617    | Failed to set the working directory.                            | An error occurred while setting the working directory for the upload or download task.               |
| 618    | The password is incorrect.                                     | The login password is incorrect. Check whether the password is correct.                           |
| 619    | The username is incorrect.                                   | The login username is incorrect. Check whether the username is correct.                       |
| 620    | The operation was not completed.                                   | The operation was not completed, as the session with the server was terminated.             |
| 621    | Failed to upload the file.                          | Failed to upload the file due to a certain cause.                               |
| 622    | Failed to log in to the server.                          | The request to log in to the FTP server failed.                                    |
| 623    | The CA is invalid.                          | The SSL certificate used by the server is not issued by the valid CA. The system error code is 12045. |
| 624    | An SSL certificate error occurred.                             | The system error code is 12055.                                          |
| 625    | The SSL certificate is invalid.                                 | The system error code is 12169.                                          |
| 626    | A redirect occurred during the transfer.                              | This error code will be reported if redirect is disabled for the transfer task but a redirect occurs. |
| 627    | Failed to verify the string.                   | This error code will be reported if the configured string cannot be found in the response header after the successful download.    |
| 628    | The response data is invalid.                               | The response data from the server could not be parsed.                                   |
| 629    | The download is incomplete.                                   | This error code will be reported if the size of the actually downloaded part is smaller than the `Content-Length` and configured value when the response header contains the `Content-Length` field, or if the size of the actually downloaded part is smaller than the configured value when the response header does not contain the `Content-Length` field, which means the actual file size cannot be obtained. |
| 630    | Download timed out.                                     | This error code will be reported if the download task times out and the download is not completed.                     |
| 631    | An HTTP to HTTPS redirect error occurred.                   | This error code will be reported if the HTTP to HTTPS redirect fails due to the security mechanism of the server running Windows Server 2012. |
| 632    | Failed to verify the MD5 checksum.                              | The MD5 checksum does not match that configured in the task after the download.               |
| 633    | Redirect failed.                                   | This error code will be reported if the number of redirects exceeds the system default value of `10` and the redirect is stopped by the system. |
| 634    | The SSL algorithms do not match.                               | The client and server algorithms do not match, which may be that the SSL protocol version was not selected or the Windows XP system version does not support the latest SSL protocol version. |
| 635    | User confirmation is required for redirect.                           | It corresponds to the `ERROR_HTTP_REDIRECT_NEEDS_CONFIRMATION` (12168) error code of WinINet, indicating that the redirect needs to be confirmed by the user. |
| 636    | Server response timed out.                         | The server response was not received within the monitoring period after the file of the specified size was uploaded over HTTP successfully. |
| 637    | Failed to send the request data.                         | The request data was not sent after an HTTP connection was established.                   |
| 638    | SSL handshake failed.                                 | For HTTPS, in most cases, the request data was not sent due to SSL handshake failure, or the SSL handshake is successful but no error was reported and no request data was sent. |
| 639    | The SSL certificate was not revoked.                             | The system error code is 12056.                                          |
| 640    | The SSL certificate was revoked.                               | The system error code is 12170.                                          |
| 641    | Client authorization was not configured on the computer.                   | The system error code is 12046.                                          |
| 642    | The requested resource requires Fortezza authentication.              | The system error code is 12054.                                          |
| 643    | The function failed due to a security check.                       | The system error code is 12171.                                          |
| 644    | The SSL content is incomplete.                       | The system error code is 12041.                                        |
| 645    | The SSL certificate was revoked.                               | The system error code is 12057.                                          |
| 646    | An error occurred while SSL was loading the SSL libraries.                    | The system error code is 12157.                                          |
| 647    | SSL connection failed.                                  | The cURL system error code is 35.                                         |
| 648    | The SSL certificate of the remote server is incorrect.                    | The cURL system error code is 51.                                         |
| 649    | The specified SSL encryption engine could not be found.                    | The cURL system error code is 53.                                         |
| 650    | Failed to set the selected SSL encryption engine as the default option.        | The cURL system error code is 54.                                        |
| 651    | The local client certificate is incorrect.                         | The cURL system error code is 58.                                        |
| 652    | Unable to use the specified key.                           | The cURL system error code is 59.                                         |
| 653    | Unable to use the known CA certificate to verify the SSL certificate.           | The cURL system error code is 60.                                        |
| 654    | Failed to recognize transfer encoding.                             | The cURL system error code is 61.                                        |
| 655    | Failed to request the SSL level.                       | The cURL system error code is 64.                                        |
| 656    | Failed to initialize the SSL engine.                         | The cURL system error code is 66.                                        |
| 657    | An error (which may be the directory error) occurred while reading the SSL CA certificate. | The cURL system error code is 77.                                        |
| 658    | Failed to terminate the SSL connection.                            | The cURL system error code is 80.                                        |
| 659    | Failed to load the certificate revocation list.                         | The cURL system error code is 82.                                        |
| 660    | Certificate revocation check failed.                            | The cURL system error code is 83.                                        |
| 661    | The keys do not match.                                   | The cURL system error code is 90.                                        |
| 662    | The CA is invalid.                           | The cURL system error code is 91.                                        |
| 663    | An internal error occurred in cURL, which needs to be located based on the log.                | -                                                            |
| 664    | An error occurred in cURL while receiving network data.            | The cURL system error code is 56.                                          |
| 665    | The specified file to be uploaded is invalid.                       | The content could not be downloaded, or the MD5 verification failed.                          |
| 720    | Failed to get the target IP.                            | Failed to get the target IP or the list of target IPs in the transfer task.           |
| 721    | An unknown network error occurred.                           | An unknown system error occurred.                                     |
| 722    | The DNS query duration in the transfer task is too long.                  | The DNS query duration in the transfer task is longer than 20 seconds.                                 |
| 723    | Failed to get the size of the downloaded part or the download duration from the response header.          | The size of the downloaded part or the download duration could not be obtained from the response header.      |
