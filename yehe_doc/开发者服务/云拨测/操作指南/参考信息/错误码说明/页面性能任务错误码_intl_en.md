This document describes the error codes for CAT page performance tasks. The following error codes, if any, will be counted into top five error types in multidimensional analysis.

| Error Code | Definition                       | Description                                                     |
| :----- | :---------------------------------------------- | :----------------------------------------------------------- |
| 300    | HTTP/1.1 300 Multiple Choices                   | -                                                            |
| 301    | HTTP/1.1 301 Moved Permanently                  | -                                                            |
| 303    | HTTP/1.1 303 See Other                          | -                                                            |
| 305    | HTTP/1.1 305 Use Proxy                          | -                                                            |
| 400    | HTTP/1.1 400 Bad Request                        | -                                                            |
| 401    | HTTP/1.1 401 Unauthorized                       | -                                                            |
| 402    | HTTP/1.1 402 Payment Required                   | -                                                            |
| 403    | HTTP/1.1 403 Forbidden                          | -                                                            |
| 404    | HTTP/1.1 404 Not Found                          | -                                                            |
| 405    | HTTP/1.1 405 Method Not Allowed                 | -                                                            |
| 406    | HTTP/1.1 406 Not Acceptable                     | -                                                            |
| 407    | HTTP/1.1 407 Proxy Authentication Required      | -                                                            |
| 408    | HTTP/1.1 408 Request Time-out                   | -                                                            |
| 409    | HTTP/1.1 409 Conflict                           | -                                                            |
| 410    | HTTP/1.1 410 Gone                               | -                                                            |
| 411    | HTTP/1.1 411 Length Required                    | -                                                            |
| 412    | HTTP/1.1 412 Precondition Failed                | -                                                            |
| 413    | HTTP/1.1 413 Request Entity Too Large           | -                                                            |
| 414    | HTTP/1.1 414 Request-URI Too Large              | -                                                            |
| 415    | HTTP/1.1 415 Unsupported Media Type             | -                                                            |
| 416    | HTTP/1.1 416 Requested range not satisfiable    | -                                                            |
| 417    | HTTP/1.1 417 Expectation Failed                 | -                                                            |
| 500    | HTTP/1.1 500 Internal Server Error              | -                                                            |
| 501    | HTTP/1.1 501 Not Implemented                    | -                                                            |
| 502    | HTTP/1.1 502 Bad Gateway                        | -                                                            |
| 503    | HTTP/1.1 503 Service Unavailable                | -                                                            |
| 504    | HTTP/1.1 504 Gateway Time-out                   | -                                                            |
| 505    | HTTP/1.1 505 http version not supported         | -                                                            |
| 601    | DNS resolution failed.                                    | This error code will be reported if the network is abnormal or the DNS server or domain is incorrect. |
| 602    | Server connection failed.                                 | This error code will be reported if the network is abnormal or the server does not work properly.           |
| 603    | The request protocol is not supported by the server.                          | This error code will be reported, for example, if the URL is `http://www.baidu.com/` and the protocol is HTTP, but HTTP is not supported by the server. |
| 604    | The connection to the server was terminated unexpectedly.                           | This error code will be reported if the network fluctuates or the request is canceled by the user.                 |
| 605    | The connection to the server was reset.                           | The issue is related to the local ISP connection, specifically, poor connection linkage and rate. |
| 606    | Redirect failed.                                      | This error code will be reported if the policy changes or all redirect attempts fail.             |
| 607    | The URL is invalid.                                      | The format of the URL configured in the task does not conform to the standard HTTP or HTTPS protocol.       |
| 617    | The network protocol is not supported.                                | Only HTTP and HTTPS protocols are supported for browsing or transaction tests.  |
| 622    | Direct access is not allowed.                                    | The network could not be accessed directly at this point.                                 |
| 623    | Requests are pending.                                     | The request operation could not be completed as certain requests are pending.               |
| 624    | The program is being redirected from HTTP to HTTPS.                       | The program is being redirected from the non-HTTPS connection to the HTTPS connection.          |
| 625    | The program is being redirected from HTTPS to HTTP.                       | The program is being redirected from the non-HTTP connection to the HTTP connection.            |
| 626    | Unable to find the HTTP header.                                  | It is usually because the custom header is written in an incorrect format.       |
| 627    | No header was returned by the server.                            | -                                                           |
| 628    | The response data is invalid.                               | The response data from the server could not be parsed.                                   |
| 629    | The HTTP header is invalid.                                 | It is usually because the custom header is written in an incorrect format.        |
| 630    | The request parameter is invalid.                                  | The handle parameter passed to `HTTPQueryInfo` is invalid.                      |
| 631    | The HTTP header already exists and could not be added.                     | -                                                           |
| 632    | The HTTP request was not redirected.                             | -                                                           |
| 633    | The HTTP cookie requires confirmation.                           | -                                                           |
| 634    | The HTTP cookie was rejected by the server.                        | -                                                           |
| 635    | The redirect requires user confirmation.                             | -                                                           |
| 636    | A secure channel error occurred.                                    | An internal error occurred while loading the SSL libraries. The system error code is 12157.   |
| 637    | The program could not cache the file.                                | -                                                           |
| 638    | The server is unreachable.                                  | -                                                          |
| 639    | The proxy server is unreachable.                              | -                                                           |
| 640    | The operation was canceled.                                      | The handle was canceled before the operation was completed.                                 |
| 641    | The operation on the element was terminated.                                  | The operation in the IE kernel is invalid. Specifically, the kernel had established a session for downloading the element and allocated resources such as the handle and context ID, but it directly closed the session (`InternetCloseHandle`) without establishing the socket connection. |
| 642    | No response was received for the request sent for the element.                          | No data was returned after the request was sent. Specifically, no data was returned by the server after the browser sent the request (the sending completion event was received). |
| 643    | Incomplete element data was returned.                             | The data packet received for the element is abnormal. Specifically, the received data packet cannot form a complete HTTP response header, or its data is abnormal. In this case, there is a time point when the first data packet was received. |
| 645    | The connection was reset after the redirect.                              | For more information on the cause, see error code 605.                                      |
| 646    | Rendering timed out after the redirect.                                | This error code will be reported if the basic document elements are not downloaded for the first five elements after the redirect. |
| 647    | Basic document download timed out.                                | This error code will be reported if the basic document elements are not downloaded for the first five elements and no redirect has occurred. |
| 648    | First screen rendering timed out.                                    | The height was not rendered to `400` after the basic document elements were loaded.                      |
| 649    | The page elements were not completely loaded.                              | The page elements had not been completely loaded when the monitoring timed out.                    |
| 650    | Failed to verify the string.                          | This error code will be reported if the configured string is not found in the page source code, basic document URL, and page title. |
| 651    | The page was redirected.                                | This error code will be reported if redirect is disabled but a page redirect occurs.     |
| 655    | Server connection timed out.                                  | It is usually due to the network.                                 |
| 656    | Request sending timed out.                                    | It is usually due to the network.                                |
| 657    | Server response timed out.                                  | It is usually due to the network.                                 |
| 658    | Data receiving timed out.                                    | It is usually due to the network.                                   |
| 659    | DNS query failed.                                   | This error code will be reported if the network is abnormal or the DNS server or domain is incorrect. |
| 660    | Element download timed out.                                    | The element load duration exceeds the configured page timeout period.                        |
| 662    | The key element was not downloaded.                                 | This error code will be reported if the key element is used to check whether page load ends but the download of the key element is not detected. |
| 664    | A certificate error occurred.                                    | An SSL certificate error occurred. The system error code is 12055.                        |
| 670    | SSL connection failed (mainly due to a certificate error).                    | Check the error based on the result.                                               |
| 671    | The domain field in the SSL certificate is invalid.                    | The system error code is 12038.                                          |
| 672    | The SSL certificate has expired.                                 | The system error code is 12037.                                          |
| 673    | The SSL certificate was revoked.                                  | The system error code is 12057.                                          |
| 674    |  The server requires installing the SSL certificate on the client.              | The system error code is 12044.                                          |
| 675    | The SSL certificate was not revoked.                                | The system error code is 12056.                                          |
| 676    | The SSL certificate was revoked.                                  | The system error code is 12170.                                          |
| 677    | The SSL certificate is invalid.                                    | The system error code is 12169.                                          |
| 678    | The SSL certificate used by the server is not issued by the valid CA. | The system error code is 12045.                                          |
| 679    | Client authorization was not configured on the computer.                      | The system error code is 12046.                                          |
| 680    | The requested resource requires Fortezza authentication.                 | The system error code is 12054.                                          |
| 681    | The function failed due to a security check.                          | The system error code is 12171.                                          |
| 682    |  The SSL content is incomplete.                         | The downloaded SSL content is incomplete. The system error code is 12041.              |
| 688    | The specified window was not found.                                  | A window was specified for executing a certain action during transaction playback, but the specified window was not found.  |
| 692    | The task configuration is invalid, as the task was configured to return no data.                 | The task was configured to return no data, usually for script configuration. If you do not care about the data in a step, you can configure the step to return no data.  |
| 697    | The new window was not opened.                                   | The page was not opened after the browsing operation.                     |
| 698    | The environment does not satisfy the conditions.                                      | Check whether the local environment satisfies certain conditions before browsing, for example, whether the required software is installed. |
| 703    | The local browsing environment may be abnormal.                            | Before returning the test results regularly to the server, the client will filter the browsing results. If it finds out that the ratio of 600 segmentation faults exceeds the threshold set by the server, it will consider all browsing data as noise data and place this error code in the returned result. |
| 704    | There is no network communication.                                    | This error code will be reported if no network data is found during data analysis after the browsing is completed.   |
| 705    | The request had stopped before the right basic document was obtained.          | The basic document (redirect not disabled) in the browsing task returned the 301/302 response code, but the browser did not redirect and continue the request. |
| 718    | The target IP was not obtained.                               | -                                                            |
| 719    | The time to first screen is too long.                   | The data is abnormal if the time to first screen exceeds five minutes.                        |
| 720    | This error code is set for testing the cache.                     | When cache is used in the general page performance task, this error code will be reported so as to discard the result and perform the task again. |
| 721    | JS download or execution failed in the browsing task.                      | This error code will be reported if the custom JS is configured in the task and the client fails to download or execute the JS file. |
