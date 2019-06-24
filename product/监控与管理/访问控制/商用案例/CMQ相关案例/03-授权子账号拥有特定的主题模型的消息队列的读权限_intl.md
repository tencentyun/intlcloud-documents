### Grant a sub-account permission to read a topic-based message queue

An enterprise account CompanyExample (ownerUin: 12345678) has a topic-based message queue, and wants to give its sub-account Developer access.

Step 1: Create the following policy using policy syntax
```
{
    "version": "2.0",
    "statement":   
     {
        "action": "cmqqueue:SendMessage",
        "resource":"qcs::cmqqueue:::queueName/uin/12345678/test-caten",
        "effect": "allow"
     } 
}
```

Step 2: Authorize the policy to the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

