### Grant a sub-account permission to read a topic-model-based message queue

For example, we have an enterprise account CompanyExample that has a topic-based message queue, and a sub-account called Developer who wants to read the message queue.

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

Step 2: Authorize the policy to the sub-account. For more information on authorization, see [Authorization Management](https://cloud.tencent.com/document/product/378/8961).

