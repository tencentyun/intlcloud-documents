Bandwidth Package (BWP) is currently under the beta test. To use either type of BWP, submit an [application for the beta test](https://cloud.tencent.com/act/apply/bwp_apply).
## Device BWPs
- Only one BWP can be activated for one region (billed based on either the top 5 peaks or the monthly 95th percentile).
- After the BWP is activated, all CVMs and LBs in the region will be automatically billed by the BWP.
- The BWP billing method cannot coexist with other billing methods in the same region.
- The bandwidth fees that are already paid will be refunded after the conversion based on the hourly bandwidth.

## IP BWPs
- IP BWPs are only available to bill-by-IP users.
- Up to 20 BWPs can be activated for one region.
- The BWP billing method can coexist with other billing methods such as hourly bandwidth and traffic in the same region.
- IP address with monthly subscribed bandwidth cannot be added to the BWP.
- For the time being, only EIPs can be added to BWP. Public IP addresses must be converted to EIPs before they can be added to BWP, which can be done in [CVM Console](https://console.cloud.tencent.com/cvm/index).
