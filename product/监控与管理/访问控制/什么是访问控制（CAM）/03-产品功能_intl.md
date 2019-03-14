CAM provides the following features:
    
**1) Access authorization**
    
You can authorize other users, including sub-accounts or other root accounts, to access the resources in your root account, without sharing the identity credentials of the root account.
    
**2) Granular permission management**
    
You can grant your desired permissions to Tencent Cloud entities. For example, You can allow certain sub-accounts to either read or write access to objects in a COS bucket.  CAM provides ease of use that you can use permissions to control who can access what kind of Tencent Cloud resources and services.
    
**4) Data integrity
    
CAM is now available in Tencent Cloud in multiple regions that allows you to synchronize cross-region data simply through replicating policy data. Although the modified CAM policies will be submitted immediately, the cross-region policy synchronization can result in delayed effects; CAM utilizes cache to improve performance (currently one-minute cache), and the updates do not take effect until the cache expires.

