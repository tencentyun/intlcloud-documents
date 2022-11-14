### Will public network assets be automatically identified on the overview page? How is it implemented?
Yes. Public network assets are automatically identified via Tencent Cloud APIs and CAM authorization. All assets of an account are enumerated through cloud APIs.

### After enabling the firewall feature, I want to enable "Observe" mode without interception. What should I do?
Enabling the firewall feature for a public IP address is OK. The "Observe" mode is used by default after the firewall feature is enabled. You do not need to configure the ACL, with the default ACL policy being "All-pass".

### How can I determine whether an IP address is blocked by CFW?
- Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw), select **Log auditing** -> **Intrusion defense logs** and **Access control logs**, and then you can check whether an IP address is blocked by CFW.
- Alternatively, enter **[Alert management](https://console.cloud.tencent.com/cfw/warncenter)** -> **Blocked attacks**, and then you can check the block statistics in the intrusion defense module.

### How can I check the Cloud Firewall version?
It is not supported to check the version currently. You can check the package and expiration date of the current account on the right of the [Overview](https://console.cloud.tencent.com/cfw) page.

### Can Cloud Firewall limit traffic by MAC address?
No. Cloud Firewall cannot limit traffic by MAC address. The second layer is shielded on cloud networks, so addressing can be performed only via IP. For example, addressing is performed via IP instead of ARP among CVMs.

### Can I adjust or disable Cloud Firewall bandwidth alert thresholds?
Bandwidth alert is an important indicator for Cloud Firewall, and traffic beyond the bandwidth limit will not be protected. You can adjust the first-level and second-level alert thresholds on the console. Disabling thresholds is not supported.

### Is my business affected when I enable or disable Cloud Firewall, scale up, add CAM authorization, and enable or disable intrusion defense?
- Enabling the edge firewall will not affect your business; enabling the NAT firewall or VPC firewall will cause an interruption of CCN for 1 to 2 seconds. In this case, you are advised to operate during non-peak hours.
- Scale-up of the edge firewall will not affect your business; scale-up of the NAT firewall may cause an interruption for 1 to 2 seconds. For any question, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Scaling up Cloud Firewall, enabling/disabling intrusion defense, or adding CAM authorization will not affect your business.
