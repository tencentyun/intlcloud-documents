The connectivity test feature is mainly used to check the connectivity between the sync tool and target database. Below are the two main check items:
- Telnet: whether the network can be properly connected.
- MySQL Connect: whether the database can be properly connected.

### Test failures
**Telnet test failure**
Possible causes: incorrectly entered target instance IP, traffic blocked by firewall, or incorrect iptable configuration.
Solution: please check the IP and configure the firewall to allow it.

**MySQL Connect test failure**
Possible causes: special configuration on the target instance; for example, SSL connection is enabled, the account is configured with HOST, or the `bind_address` configuration is listened on.
Solution: please check the IP and configure the firewall to allow it.

