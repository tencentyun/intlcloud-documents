### Grant a sub-account full permissions to access the messaging queue that it created

A sub-account of the enterprise account CompanyExample called Developer wants to access the message queue it created.

Solution A:

The enterprise account CompanyExample directly authorizes the preset policies QCloudCmqQueueCreaterFullAccess and QCloudCmqTopicCreaterFullAccess to the sub-account Developer. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: Create the following policy using policy syntax

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

Step 2: Authorize the policy to the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).


