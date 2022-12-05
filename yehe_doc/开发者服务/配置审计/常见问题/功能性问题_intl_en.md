## Which Tencent Cloud services and resource types does Config support?
For more information, see [Supported Resource Types](https://www.tencentcloud.com/document/product/1164/51495).

## Why aren't some resources displayed in the resource list?
After you activate the Config service, modify the monitoring scope, or manually update the resource snapshot, Config will be triggered to update all information of all resource types. As the data volume is high, it takes about 15 minutes to pull, generate, or update the resource configuration snapshot.

## Why is the resource configuration information displayed in Config different from the configuration information of the same resource in the product's console?
In the following scenarios, the resource configuration information displayed in Config is different from the configuration information of the same resource in the product's console:
1. If a resource configuration field of the product is not one of the configuration items defined in Config, this field won't be displayed in the Config console.
2. If a resource configuration field of the product is one of the configuration items defined in Config, but its change operation event failed to be reported to CloudAudit, then the change of the configuration information cannot be captured by CloudAudit and Config. As a result, the configuration information of the same resource in the Config console and the product's console differ.
3. If there is a high data volume under your account, it will take about 15 minutes to pull, generate, or update resource configuration snapshots, after which the data will be updated.

## Why isn't a configuration change operation displayed on the resource timeline?
After you change a resource configuration, Config will notice the change within 15 minutes. If you restore the configuration to the original one within this period, Config may not generate the change record.

## How far back can Config record the configuration data?
Config retains the resource information and configuration history in the last year by default. If you want to retain a longer history, you can create a tracking set to persistently store the configuration data. For more information, see [Delivery Service](https://www.tencentcloud.com/document/product/1164/51539).

## How often are the configuration histories on the resource timelines in Config delivered to COS?
Configuration histories are delivered to the COS bucket at 00:30 every day.

## How can I use more rules?
You can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to describe your required rules in detail. For the rule format, see [Supported Managed Rules](https://www.tencentcloud.com/document/product/1164/51503). Config and CloudAudit teams will jointly review your application and determine whether to provide your required rules as managed rules.

## Why isn't a set rule triggered for evaluation?
If the rule is set to be triggered periodically, evaluation will be performed only at a fixed time point.
If the rule is set to be triggered when the configuration changes, after it is bound, it will be triggered only when the configuration of the associated resource changes.
On the rule details page, you can manually trigger a rule for audit again to quickly get the latest evaluation result.

