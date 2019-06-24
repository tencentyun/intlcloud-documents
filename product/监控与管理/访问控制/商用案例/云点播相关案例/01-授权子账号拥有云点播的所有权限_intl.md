### Grant a sub-account full permissions to manage Tencent Cloud VOD services

A sub-account Developer under the enterprise account CompanyExample (ownerUin: 12345678) requires full permissions to manage Tencent Cloud VOD services in the enterprise account.

Solution A:

The enterprise account CompanyExample directly authorizes the preset policy QcloudVODFullAccess to the sub-account Developer. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/378/10602).

Solution B:

Step 1: Create the following policy using policy syntax
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "vod:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": "cos:*",
            "resource": "qcs::cos::uid/10022853:*",
            "effect": "allow"
        }
    ]
}
```
Step 2: Authorize the policy to the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/378/10602).


