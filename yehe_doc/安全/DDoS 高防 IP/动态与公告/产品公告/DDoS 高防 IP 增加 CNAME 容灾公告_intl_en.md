## Background
To improve the disaster recovery capability against out-of-control emergencies in Anti-DDoS lines, Anti-DDoS Advanced instances now can be accessed via CNAME from May 13, 2022. CNAME can be resolved to different Anti-DDoS Advanced instance IPs. When the primary instance IP fails (which does not caused by blocking), CNAME will be resolved to the secondary instance IP to ensure service continuity.

## Updates
- Anti-DDoS Advanced instances can be connected via CNAME starting from May 13, 2022.
- If you already purchased or used Anti-DDoS Advanced instances before May 13, 2022, the IP addresses of the instances will still be retained to serve your business. However, to improve your business stability, you’re recommended to change the DNS resolution target to the assigned CNAME.
- If Anti-DDoS Advanced instances are purchased after that date, change the DNS resolution target to the assigned CNAME.

>!Note that these updates are not available for non-BGP resources.

## Notes
The DNS resolution target of the access source should be changed to the assigned CNAME as soon as possible. The CNAME will then be resolved to an instance IP that can forward cleansed traffic back to the origin server. These updates will not have any effect on existing users.
>? Anti-DDoS Advanced instance IPs may change. To avoid DNS resolution failure, modify your DNS address to the assigned CNAME.
