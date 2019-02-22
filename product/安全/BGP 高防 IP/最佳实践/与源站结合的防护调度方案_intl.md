[//]: # (chinagitpath:XXXXX)

## Scenarios
For applications have a high requirement for latency, or must access the real server directly when the volume of business requests is normal. In this case, the real server-based defense scheduling solution can be considered.
This solution can enable user businesses to access the real server directly under normal traffic conditions and to acquire the ability to defend against large-traffic attacks.

## Protection Solution
The real server-based defense scheduling solution is shown as below:
>? This solution relies on DNS service providers to provide monitoring and intelligent switching capabilities.

 ![](https://main.qcloudimg.com/raw/302376f5b0a0a2c11391cffaa16cab65.png)

## Solution Description
This solution mainly consists of protective IP, DNS monitoring, external business IP of customer's real server and standby IP of the real server.
- Under normal circumstances, the customer domain name is resolved to the outbound IP. Requests accesses the real server directly. DNS monitoring monitors in real time whether the application on the real server can be accessed.
- When DNS monitoring detects that the outbound IP cannot be accessed, the customer domain name will be resolved to the Anti-DDoS Advance IP instantly according to the preset rules. Anti-DDoS Advance cleanses the attack traffic and then forwards the normal traffic to the standby IP of the real server, thus ensuring business availability.
>! To avoid mis-switching caused by jitter or other factors, manual switching is recommended.


## Solution Effects
- Meets the needs of direct access to the real server under normal circumstances.
- Applies to businesses that have a high requirement for latency.
- When the traffic is beyond the defense capability of the real server, the business will be quickly resolved to the protective IP.

## Suggestions and Notes
1. The standby IP of the real server and the forwarding rules for the protective IP should be configured beforehand.
2. Deploy the standby IP and primary IP on in different physical lines for better protection result.
3. Conduct regular verification and drills to get familiar with the solution and solve possible problems.


