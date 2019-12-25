
A sub-account, Developer, under the enterprise account, CompanyExample (ownerUin: 12345678), requires view permission for two TencentDB for MySQL instances (instance IDs cdb-1 and cdb-2 respectively) belonging to the CompanyExample enterprise account.

Step 1: create the following policy by using policy syntax.
```
 {
    "version": "2.0",
    "statement":[
     {
         "effect": "allow",
         "action": "cdb:*",
         "resource": ["qcs::cdb::uin/12345678:instanceId/cdb-1", "qcs::cdb::uin/12345678:instanceId/cdb-2"]
     }
   ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Note: The Developer sub-account can only view the resources of instances with the IDs cdb-1 and cdb-2 in the TencentDB for MySQL query list.

