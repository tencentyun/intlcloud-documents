## Overview
Cloud Access Management (CAM) is used to manage the access permissions for the resources under Tencent Cloud accounts. With CAM, you can use the identity management and policy management features to control which Tencent Cloud resources can be accessed by which sub-accounts. This document describes how to use certain policies in the console.

## Samples
### Full access policy in Private DNS
To grant a user the permission to create and manage private domains in Private DNS, associate the **QcloudPrivateDNSFullAccess** policy with the user.
Associate the preset policy **QcloudPrivateDNSFullAccess** with the user as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
The policy syntax is as follows:
```
{
  "version": "2.0",
  "statement": [
  {
    "action": [
        "privatedns:*"
     ],
     "resource": "*",
     "effect": "allow"
   }
  ]
}
```

### Read-only policy in Private DNS
To grant a user the permission to view private domains in Private DNS but not create or delete them, associate the **QcloudPrivateDNSReadOnlyAccess** policy with the user.
Associate the preset policy **QcloudCVMInnerReadOnlyAccess** with the user as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
The policy syntax is as follows:
```
{
  "version": "2.0",
  "statement": [
  {
    "action": [
       "privatedns:Describe*"
     ],
     "resource": "*",
     "effect": "allow"
    }
  ]
}

```
