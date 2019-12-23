
The enterprise account, CompanyExample (ownerUin: 12345678), wants to give its sub-account, Developer, access to its topic-based message queue.

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [  
     {
        "action": "cmqqueue:SendMessage",
        "resource":"qcs::cmqqueue:::queueName/uin/12345678/test-caten",
        "effect": "allow"
     } 
     ]
}
```

Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
