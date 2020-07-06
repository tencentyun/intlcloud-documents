## Background
You may consider real server-based protection scheduling if your customers have low tolerance for connection latency or if your business requires normal traffic to directly access the real server.
This scheme can quickly schedule protection after attacks occur, while allowing normal traffic to access the real server.

## Protection Scheme
The figure below illustrates how real server-based protection scheduling works:
>This scheme requires monitoring and intelligent switching provided by DNS service providers.

 ![](https://main.qcloudimg.com/raw/2c31072460266c94057af601ced2392f.png)

## Scheme Description
To implement this scheme, you need an Anti-DDoS Advanced IP, a DNS monitor, an external business IP, and a standby IP of the real server.
- Under normal circumstances, your business domain name is resolved to the outbound IP. Requests access the real server directly. DNS monitors watch over whether the applications are accessible on the real server in real time.
As soon as the DNS monitor detects that the outbound IP is not accessible, DNS will resolve the business domain name to the Anti-DDoS Advanced IP according to the preset switching rules. Anti-DDoS Advanced will cleanse and remove the attack traffic and forward normal traffic to the standby IP of the real server, thus ensuring service availability.
>To avoid faulty switching caused by uncontrollable factors such as network jitter, manual switching is recommended.


## Benefits
- Meets the needs of direct access to the real server under normal circumstances.
- Applies to businesses that require very low connection latency.
- When the traffic volume is beyond the protection capability of the real server, the domain name will be automatically resolved to the Anti-DDoS Advanced IP.

## Tips and Precautions
- Configure the forwarding rules of real server standby IP and Anti-DDoS Advanced IP in advance.
- Deploy the standby IP and primary IP of the real server with different physical addresses for better protection results.
- Practice and test regularly and familiarize yourself with scheme details to solve potential problems.

