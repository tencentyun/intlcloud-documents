[//]: # (chinagitpath:XXXXX)

## Real Server-based Defense Scheduling
You may consider real server-based defense scheduling if your customers have low tolerance for connection latency or if your business requires normal traffic directly access the real server. This plan can quickly schedule defense after attacks, while allowing normal traffic to access the real server. 

## Defense Solution
The figure below illustrates how real server-based defense scheduling works:
>This solution requires monitoring and intelligent switching provided by DNS service providers.

 ![](https://main.qcloudimg.com/raw/2c31072460266c94057af601ced2392f.png)

## Solution Description
This solution mainly consists of protective IP, DNS monitoring, external business IP of customer's real server and standby IP of the real server.
- Under normal circumstances, the customer domain name is resolved to the outbound IP. Requests accesses the real server directly. DNS monitoring monitors in real time whether the application on the real server can be accessed.
- As soon as the DNS monitor detects that the outbound IP is not accessible, DNS will resolve the customer domain name to the Anti-DDoS Advanced IP address according to the preset switching rules. Anti-DDoS Advanced will clean and remove the attack traffic and then forward the normal traffic to the standby IP of the real server, thus ensuring service availability. 
> To avoid mis-switching caused by uncontrollable factors such as jitter, manual-switching is recommended.

## Solution Results
- Meets the needs of direct access to the real server under normal circumstances.
- Applies to businesses that require very low connection latency.
- When the traffic volume is beyond the defense capability of the real server, the domain name will be auto-resolved to the Anti-DDoS Advanced IP.

## Suggestions and Notes
1. Preset the forwarding rules of real server standby IP and Anti-DDoS Advanced IP.
2. Deploy the standby IP and primary IP using different physical addresses for better protection results.
3. Practice and test regularly and familiarize yourself with solution details to solve potential problems.

