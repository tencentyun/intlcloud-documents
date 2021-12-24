## Error Description
In a CLB UDP health check, the health check result is different from the actual status of the real server port.

## Cause
In a UDP health check, the CLB instance sends a UDP probe message to the real server. If the PING command is successful and an error message `port XX unreachable` is not returned within the response timeout period, the real server is considered healthy. Otherwise, the real server is considered unhealthy.

There are two possible causes for this error:
- The response timeout period is too short for the real server to return a ICMP message `reply` or `port unreachable` to the health check nodes, leading to an inaccurate health check result.
- The real server restricts the rate at which ICMP messages are generated. In this case, when a service exception occurs, `port XX unreachable` cannot be returned, and the CLB instance considers that the health check is successful as no ICMP response is received. Therefore, the health check result is inconsistent with the actual server health.

## Troubleshooting Procedure
1. Check whether the response timeout period is too short. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), and increase the timeout duration for the UDP listener. For more details, see [Configuring a UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518).
>? UDP health checks are different from other health checks. If the health check timeout period is too short, the health check result will switch back and forth between healthy and unhealthy.
2. If the error persists, check whether the real server restricts the frequency of ICMP messages. Log in to the real server, and run the following commands to check the rate limit.
```
sysctl -q net.ipv4.icmp_ratelimit
sysctl -q net.ipv4.icmp_ratemask
```
3. Check whether the return value of the first command is `0` or `1000` (default). We commend using the default value.
4. If the error persists, run the following command to disable the rate limit of the ICMP `port unreachable` messages.
>!Note that if the rate limit of ICMP `port unreachable` messages is lifted, when the real server is connected to the public network and encounters UDP port scanning attack, it will keep returning `port unreachable` messages 
>
```
# Run the command `net.ipv4.icmp_ratemask` in step 2 to query the rate mask.
# Keep the first three digits of the returned rate mask unchanged, and subtract 8 from the last digit. For example, if the mask returned is “6168”, replace "xxxx" with 6160; if it is 1819, replace "xxxx" with 1811.
sysctl -w net.ipv4.icmp_ratemask=xxxx
```


