### How do I fix the "InternalError" reported by the console?
1. "InternalError" is reported when a non-root account attempts to purchase an EMR cluster.
**Cause**: the current account lacks permission.
**Solution**: confirm whether the current account has completed identity verification and been granted the payment permission.
2. "InternalError" is reported when a non-root account clicks **Hardware Management** in the console.
**Cause**: the current account lacks permission.
**Solution**: open the following link:
`https://console.cloud.tencent.com/cam/role/grant?roleName=EMR_QCSRole&policyName=QcloudAccessForEMRRole&principal=eyJzZXJ2aWNlIjoiZW1yLmNsb3VkLnRlbmNlbnQuY29tIn0=&serviceType=EMR`. Then, grant the EMR permission by using the root account.
