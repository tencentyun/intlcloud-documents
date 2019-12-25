
A sub-account, Developer, under the enterprise account, CompanyExample, requires access to the message queue it created.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policies QCloudCmqQueueCreaterFullAccess and QCloudCmqTopicCreaterFullAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.

```
{
    "version": "2.0",
    "statement":
    [
       {
           "effect": "allow",
           "action": "cmqtopic:*",
           "resource": "qcs::cmqtopic:::topicName/uin/${uin}/*"
       },
       {
           "effect": "allow",
           "action": "cmqqueue:*",
           "resource": "qcs::cmqqueue:::queueName/uin/${uin}/*"
       }
    ]
}
```

Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

