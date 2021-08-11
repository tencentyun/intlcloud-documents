This document describes how to create a COS trigger and invoke a function.

### Step 1. Create a function
Log in to the [SCF console](https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default) and upload and deploy your function code on the **Create** page. For more information, please see [Creating Functions in Console](https://intl.cloud.tencent.com/document/product/583/32742).


The following takes the COS sample template as an example to create a function project. In the default creation process with the template, a trigger is directly configured. In actual use cases, you can also configure a trigger after creating the function. Here, configuration after function creation is used as an example for description:
![](https://main.qcloudimg.com/raw/98fb93e60dd46dee4185e2842a0e4bf8.png)


### Step 2. Configure a trigger
After selecting **COS Trigger**, configure the bucket, triggering event type, and other information as prompted to create a trigger:
![](https://main.qcloudimg.com/raw/4bfbf21b3f60141c7844d9eb0cce8b25.png)

### Step 3. Manage the trigger
After successful creation, you can see the information of the created trigger on the **Trigger Management** page. You can also go to the COS console to perform other operations.
