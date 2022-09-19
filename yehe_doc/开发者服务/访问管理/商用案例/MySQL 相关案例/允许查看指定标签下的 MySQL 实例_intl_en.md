The enterprise account “CompanyExample” (ownerUin: 12345678) has a sub-account “Developer” that requires permissions to view its two TencentDB for MySQL instances (instance IDs: “cdb-1” and “cdb-2”, with the tags being “game&webpage” and “game&app”, respectively).

Step 1: Create the following policy by using policy syntax.
```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "game&webpage",
                        "game&app"
                    ]
                }
            }
        }
    ]
}
```
Step 2. Authorize the policy to the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

>?The sub-account “Developer” can only view the resources of instances with the IDs being “cdb-1” and “cdb-2” in the TencentDB for MySQL query list.


