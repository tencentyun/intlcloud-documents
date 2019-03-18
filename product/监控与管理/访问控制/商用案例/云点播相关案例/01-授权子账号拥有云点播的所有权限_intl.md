### Grant a sub-account full permissions to access Tencent Cloud VOD services

For example, we have a sub-account of the enterprise account CompanyExample called Developer, which requires full permissions to mnanage Tencent Cloud VOD services in the enterprise account CompanyExample.

Solution A:

The enterprise account CompanyExample directly authorizes the preset policy QcloudVODFullAccess to the sub-account Developer. For more information on authorization, see [Authorization Management](https://cloud.tencent.com/document/product/378/8961).

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
Step 2: Authorize the policy to the sub-account. For more information on authorization, see [Authorization Management](https://cloud.tencent.com/document/product/378/8961).


