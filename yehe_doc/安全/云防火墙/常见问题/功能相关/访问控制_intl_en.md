### Does CFW allow or block traffic by default when no rules are configured?
By default, CFW allows all traffic. Once enabled, CFW will record traffic logs and generate intrusion defense alerts, but will not block any traffic because no rules are configured.

### How can CFW allow a specific port?
1. After enabling the edge firewall, select **[Access Control](https://console.cloud.tencent.com/cfw/ac)** -> **Edge Rules** -> **Inbound Rules** to enter the inbound rule page.
2. Click **Add Rule** to allow a specific port, and then add a rule to block all ports.
>?If no rule is configured, all traffic is allowed by default.

### When will configured access control rules take effect?
CFW rules will take effect after 10 seconds to 1 minute upon configuration.

### Does CFW support access control by domain name?
Both edge firewall and NAT firewall can set outbound rules by domain name.

### Can CFW configure limitation policies by domain name?
Currently, limitation policies can be configured by domain name for assets in Chinese mainland and Hong Kong.

### Does CFW support blocking by region?
Enterprise Edition and above support blocking by region.

### Why can't I select the automatic both-way enterprise security group?
Automatic both-way access is supported only when the source address is an instance, subnet, or private network address. In this case, a same outbound rule (with the earliest execution order) will be allocated, which is applicable to scenarios that allow both-way internal-to-internal access.

### Will the login protocol port be blocked if the edge firewall feature is not enabled for an asset?
No.
