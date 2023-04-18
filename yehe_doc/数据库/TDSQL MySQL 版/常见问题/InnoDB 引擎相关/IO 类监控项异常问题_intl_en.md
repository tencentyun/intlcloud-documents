## Exception
Log in to the [TDSQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql) and click an instance ID to enter the instance management page. On the **Monitoring and Alarms** tab, you can view three IO metrics.

| Metric | Category | Description |
| ------ | ------ | ------ |
|IOUsageRate| Instance monitoring | Maximum IO utilization of the source node |
|IOUsageRateShard| Shard monitoring | IO utilization |
|IOUsageRateNode| Node monitoring | IO utilization |

In actual use, the above three IO metrics may increase abnormally even during off-peak hours. Alarms configured for them, if any, will be triggered.

## Exception causes
Possible causes of the abnormal IO increase include:

- There is a calculation problem with the IO metrics, and the actually displayed values are IO values of the server where the instance and node reside.
- The IO levels of other instances on the same server increase, which may affect the IO monitoring of the current instance.

## Solution
This issue involves [alarms](https://console.cloud.tencent.com/monitor/policylist). We have located it and are fixing it. You can try the following workarounds for the time being:

- Do not configure alarms for these three IO metrics. Or, increase their alarm thresholds to avoid the impact of abnormal alarms.
- Ignore these three IO metrics when they increase abnormally and don't match the business usage.
- We are monitoring and handling the IO usage issue uniformly to ensure the normal operations of instances.

