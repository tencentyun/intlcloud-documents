The arrears policies for peering connections vary with billing modes. This document describes these methods in detail.
## For billing by daily peak bandwidth
- When your account balance becomes 0, you can continue to use your cross-region peering connection for two hours and fees are deducted normally.
- Two hours later, if your account is still in arrears, your cross-region peering connection will be isolated (unavailable) and fee deduction stops.
- If you pay the overdue payment within 24 hours, the bandwidth cap for your cross-region peering connection is reset to the value you set, and the connection becomes available again.
- If you fail to pay the overdue payment within 24 hours, the system repossesses the resources.
![](https://main.qcloudimg.com/raw/849fdae515d56e6c82c11e1bf111827b.jpg)

## For billing by monthly 95th percentile
- When your account balance becomes 0, you can continue to use your cross-region peering connection for 24 hours and fees are deducted normally.
- 24 hours later, if your account balance is still in arrears, your cross-region peering connection will be isolated (unavailable) and fee deduction stops.
- If you pay the overdue payment within seven days (168 hours), the bandwidth cap for cross-region peering connections is reset to value you set, and the connection becomes available again.
- If you fail to pay the overdue payment within seven days (168 hours), the system repossesses the resources.

