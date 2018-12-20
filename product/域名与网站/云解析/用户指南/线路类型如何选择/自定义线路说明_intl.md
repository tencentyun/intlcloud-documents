### What Is Custom Resolution?
Custom resolution means that you can specify an IP range to access the specified server.

> **Note:**
> The specified IP range must be the IP of your recursive DNS;
> The IP of the recursive DNS is the egress IP of the connected client DNS, i.e. the backend IP;
> The backend DNS IP range needs to be collected by yourself.

### How to Collect the IP of the Recursive DNS (Egress IP of the DNS)?

Use the client where the DNS address is set to visit `http://ip.dnspod.cn/` and click **Start detection** for Whois lookup to get the server address, where you can see the egress IP range of the DNS. For example, running Whois lookup for 219.141.136.10 gets the IP range: 219.141.128.0 - 219.143.255.255.
>**Note:**
> It is recommended to refresh and look up for several times and verify whether there is any missing IP.

### When Will Custom Resolution Be Used?

If you need to distinguish the lines more delicately, specify an IP range to access the specified server according to your own needs or prevent users of a DNS or in a region from visiting your website, you can use custom resolution.
> **Note:**
> **Custom lines** have higher priority than **system-defined lines**;
> Google DNS still follows the Google extension.

