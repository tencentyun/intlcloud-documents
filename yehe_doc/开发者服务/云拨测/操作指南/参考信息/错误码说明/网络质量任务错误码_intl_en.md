This document describes the error codes for CAT network quality tasks. The following error codes, if any, will be counted into top five error types in testing statistics.

| Error Code | Definition                       | Description                                                     |
| :----- | :------------------------- | :----------------------------------------------------------- |
| 601    | No server was found during the ping test.      | In a ping test, DNS query is performed to resolve the domain to be pinged to an IP, and then the ICMP packet is sent. This error code will be reported if an error occurs during domain resolution. |
| 602    | The number of tracert hops exceeds the limit.   | By default, there can be up to 30 hops in a tracert test. If the number of hops is set to a value smaller than 30, the configuration applies. This error code will be reported if the number of IPs in a tracert exceeds the limit. |
| 603    | The network environment test timed out.           | This error code applies to DNS query, ping, and tracert tests.    |
| 605    | The tracert server is unreachable.       | The server will be regarded as unreachable if the tracert operation times out and already has five hops.  |
| 606    | CNAME query failed.        | CNAME query failed in the DNS process.                          |
| 608    | The local DNS server could not be found.      | This error code will be reported if the local DNS server address cannot be obtained.                |
| 609    | The DNS requests of all NS servers failed. | Multiple NS servers are available for DNS query. The client will get the list of all NS servers and perform query operations one by one. DNS query is regarded as successful if one of the requests returns the DNS record successfully. This error code will be reported if the DNS requests of all NS servers fail. |
| 610    | The NS root servers could not be resolved.         | The iteration process requires the 13 NS root servers in the international domain system and cannot start if these servers cannot be resolved. |
| 611    | The intermediate NS server could not be resolved.     | The iteration process requires resolving the NS server under each domain in a top-down manner and will fail if the NS server under any domain fails to be resolved. |
| 612    | The domain does not exist.                 | The NS server returned an error code to notify the local server that the domain does not exist.                    |
| 613    | Another error was returned by the NS server.         | The NS server returned another error code.                                  |
| 614    | Failed to send the request.              | All echo requests failed.                                         |
| 615    | The request returned that the target network is unreachable.   | All echo requests returned that the network is unreachable.                             |
| 616    | The request returned that the protocol is unreachable.       | All echo requests returned that the protocol is unreachable.                             |
| 617    | The request returned that the port is unreachable.       | All echo requests returned that the port is unreachable.                             |
| 618    | The packet is too large and needs to be split.           | All echo requests returned that the packet needs to be split.                                 |
| 619    | The request timed out.                   | All echo requests timed out.                                         |
| 620    | The TTL timed out during transfer.          | The TTL of all echo requests timed out during transfer.                         |
| 621    | The TTL timed out during packet reassembling.      | The TTL of all echo requests timed out during packet reassembling.                      |
| 622    | The target address is invalid.               | All echo requests returned the invalid target address.                           |
| 623    | The address is invalid.                | The entered task address is invalid.                                         |
| 624    | The custom NS server address is invalid. | You need to check whether the custom NS server is correct, which can be an IP or domain. |
| 625    | The server refused connection.             | This error code will be reported if the port of the server is not open during a TCP ping.            |
