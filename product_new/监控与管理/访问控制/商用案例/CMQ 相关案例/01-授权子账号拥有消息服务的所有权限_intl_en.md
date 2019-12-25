
The enterprise account, CompanyExample, has a sub-account, Developer, that requires full permissions to read and write the message queue of CompanyExample. The message queue for read and write permissions can be either topic model or queue model.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policies QCloudCmqQueueFullAccess and QCloudCmqTopicFullAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.
```
 {
    "version": "2.0",
    "statement":[
     {
         "effect": "allow",
         "action": ["cmqtopic:*","cmqqueue:*"],
         "resource": "*"
     }
   ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

