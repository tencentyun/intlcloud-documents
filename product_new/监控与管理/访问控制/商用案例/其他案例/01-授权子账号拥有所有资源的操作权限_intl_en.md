
A sub-account, Developer, under the enterprise account, CompanyExample, requires full access permission to all resources belonging to the enterprise account.

Solution A:

The CompanyExample enterprise account directly associates the Developer sub-account with the preset policy AdministratorAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": "*",
            "resource": "*"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

