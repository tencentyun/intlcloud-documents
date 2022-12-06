
You can quickly get started with Config in the Tencent Cloud console. This document describes how to quickly activate Config.

### Step 1. Sign up for a Tencent Cloud account

Click [here](https://intl.cloud.tencent.com/en/account/register) to sign up for a Tencent Cloud account. If you already have one, skip this step.

### Step 2. Activate Config

Select the target resource type to be monitored and recorded by Config.
For more information, see [Monitoring Management](https://www.tencentcloud.com/document/product/1164/51538).
Before activating Config, you need to grant Config the access to resource information and COS buckets.

### Step 3. View the details of global resources and configuration items

In the resource list in the Config console, you can search for monitored resources by region and view the change history of each resource.
Config will update the resource list periodically (00:00 AM every day) or based on the captured CloudAudit configuration change history. You can also manually update resource snapshots.
For more information, see [Viewing Resource List](https://www.tencentcloud.com/document/product/1164/51500) and [Viewing Resource Details](https://www.tencentcloud.com/document/product/1164/51501).

### Step 4. Create a rule or conformance pack to evaluate the compliance of resource configurations

You can create a rule or a conformance pack of rules to evaluate the compliance of resource configuration changes in Config.
For more information, see [Managing Rule](https://www.tencentcloud.com/document/product/1164/51516) and [Managing Conformance Pack](https://www.tencentcloud.com/document/product/1164/51527).

### Step 5. Create a tracking set to deliver resource histories

In the Config console, you can query the resource history in the last year. If you want to retain snapshots for a longer time or query, export, and analyze snapshots as needed, you can create a tracking set to deliver resource histories to COS buckets for further processing.
For more information, see [Delivery Service](https://www.tencentcloud.com/document/product/1164/51539).

