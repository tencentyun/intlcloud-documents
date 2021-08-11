This document describes how to create a CKafka trigger and invoke a function.

### 1. Create a function
Upload and deploy your function code on the **Create** page in the SCF console.

![](https://main.qcloudimg.com/raw/f8047105b56df5f01d2da6524b70fddc.png)

The following takes the CKafka sample template as an example to create a function project. In the default creation process with the template, a trigger is directly configured. In actual use cases, you can also configure a trigger after creating the function. Here, configuration after function creation is used as an example for description:
![](https://main.qcloudimg.com/raw/be4e6fef7619073b9a73a9f04e30bdb0.png)


### 2. Configure a trigger
After selecting **CKafka Trigger**, configure the queue name, topic, and other information as prompted to create a trigger:
>! Note: make sure that your function and CKafka instance are in the same VPC.

![](https://main.qcloudimg.com/raw/fdb2f5da3bc22dae4d748f284d86ed0f.png)

### 3. Manage the trigger
After successful creation, you can see the information of the created trigger on the **Trigger Management** page, where you can enable/disable the trigger.


