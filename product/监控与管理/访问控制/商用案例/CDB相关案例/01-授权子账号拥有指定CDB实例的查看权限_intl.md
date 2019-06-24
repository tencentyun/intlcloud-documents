### Grant a sub-account permission to view specified CDB instances

A sub-account Developer under the enterprise account CompanyExample (ownerUin: 12345678) requires view permission of two CDB instances (instance IDs are cdb-1 and cdb-2 respectively) of the enterprise account CompanyExample.

Step 1: Create the following policy using policy syntax
```
 {
    "version": "2.0",
    "statement":
     {
         "effect": "allow",
         "action": "cdb:*",
         "resource": ["qcs::cdb::uin/12345678:instanceId/cdb-1", "qcs::cdb::uin/12345678:instanceId/cdb-2"]
     }
}
```
Step 2: Authorize the policy to the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Note: The sub-account Developer can only view the resources of instance cdb-1 and cdb-2 in the CDB query list.



