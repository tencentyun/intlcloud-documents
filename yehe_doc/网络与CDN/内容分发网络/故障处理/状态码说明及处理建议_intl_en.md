

The table below explains the status codes of CDN.

| Status Code | Meaning | Suggestion |
| :----- | :------------------------------- | :----------------------------------------------------------- |
| 400 | HTTP request syntax error and the server cannot parse the request | Check whether the request syntax is correct.                                  |
| 403    | Request is rejected                             | Check whether the request is blocked by access controls such as referer blocklist/allowlist, IP blocklist/allowlist, and authentication. |
| 404    | Server cannot return correct information           | Check whether the original server is running normally, and whether the original server information or origin domain configurations are changed. |
| 413    | Content length of the POST request exceeds the limit                    | Check the content size of the POST request from the client (the maximum size is 32 MB by default).           |
| 414    | URL length exceeds the limit                     | The maximum URL size is 2 KB by default.                                        |
| 423    | Looping request                           | Check the 301/302 configuration, HTTPS origin-pull, and rewriting method of the origin server. |
| 499    | The client closes the connection                  | Check the client status and timeout configuration.                                |
| 502    | Gateway Error                             | Check whether the business origin server is normal.                                       |
| 503    | COS frequency control is triggered                          | Check the cache configuration or whether the COS origin server returns no-cache/no-store.                 |
| 509    | Blocked due to CC attack                | Please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) |
| 514    | IP access frequency exceeds the limit                       | Check the IP access frequency control configuration in the CDN Console.                                 |
| 531    | Error resolving the origin-pull domain name in the HTTP request          | Check the domain name resolution configuration of the origin server.                                       |
| 532    | Failed to establish a connection with the origin server in the HTTPS request              | Check the port 443 status of the origin server, certificate configuration, or availability of the origin server.                  |
| 533    | Origin-pull connection timeout in the HTTPS request              | Check the port 443 status of the origin server, certificate configuration, or availability of the origin server.                  |
| 537    | Origin server data reception timeout in the HTTPS request             | Check the stability of the business origin server.                                         |
| 538    | SSL handshake of HTTPS request failed                | Check the compatibility between the origin server protocol and algorithm.                                 |
| 539    | Certificate validation of HTTPS request failed           | Check whether the certificate of the origin server is correctly configured (validity period and completeness of the certificate chain).       |
| 540    | Certificate domain name validation of HTTPS request failed          | Check whether the certificate of the origin server is correctly configured.                                  |
| 562    | Failed to establish a connection in the HTTPS request                | Please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) and provide the X-NWS-LOG-UUID information for troubleshooting. |
| 563    | Connection timeout in the HTTPS request              | Please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) and provide the X-NWS-LOG-UUID information for troubleshooting. |
| 564    | HTTP origin request failed                | If HTTP is configured as the origin request protocol, check the load and bandwidth utilization or access limit of the origin server. If the protocol is set to **Follow Request**, check the port 443 status and certificate configuration of the origin server. If no error is found in the origin server, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) and provide the X-NWS-LOG-UUID information for troubleshooting.|











