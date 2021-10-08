This document describes how to create a CKafka trigger and invoke a function.

### 1. Create a function
Log in to the [SCF console](https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default) and upload and deploy your function code on the **Create** page.

![](https://main.qcloudimg.com/raw/f3c1461afc4892119b77e288b833b337.png)

The following takes the CKafka sample template as an example to create a function project. In the default creation process with the template, a trigger is directly configured. In actual use cases, you can also configure a trigger after creating the function. Here, configuration after function creation is used as an example for description:
![](https://main.qcloudimg.com/raw/5188f999bd1f628c3ce2ab9491d2d762.png)


### 2. Configure a trigger
After selecting **CKafka Trigger**, configure the queue name, topic, and other information as prompted to create a trigger:
>! Note: make sure that your function and CKafka instance are in the same VPC.

![](https://main.qcloudimg.com/raw/81777ea8d1b32707e2abf24d074f9d7e.png)

### 3. Manage the trigger
After successful creation, you can see the information of the created trigger on the **Trigger Management** page, where you can enable/disable the trigger.
![](https://main.qcloudimg.com/raw/275d59c7cc1ddc644aeab9c032d61b7e.png)

