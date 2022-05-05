## Overview
Tencent Cloud CloudAudit can be used to retrieve the historical records of API calls under your Tencent Cloud account, including API calls via the Tencent Cloud console, Tencent Cloud SDKs, command line tools, and other Tencent Cloud services. This means that any deployment behavior on Tencent Cloud is monitored, and you can find out the source IP address and time when a sub-user or collaborator calls a Tencent Cloud API.

Currently, Tencent Cloud CloudAudit has been fully integrated into EventBridge. You can use the default Tencent Cloud service event bus to receive **write** operations on the cloud for management and Ops. For the services and APIs that support CloudAudit, see [CloudAudit-Enabled Services and APIs](https://intl.cloud.tencent.com/document/product/1021/37598).

## Event Format

```json
{
    "specversion":"1.0",
    "id":"13a3f42d-7258-4ada-da6d-023a33******",
    "source":"${ProductName}.cloud.tencent",
    "type":"cvm:CloudEvent:ApiCall",
    "subject":"${resource ID}",
    "time": 1615430559146,
    "region":"ap-guangzhou",
    "resource":[
        "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
    ],
    "datacontenttype":"application/json;charset=utf-8",
    "tags":{
        "key1":"value1",
        "key2":"value2"
     },
    "data":{
        ${Raw API operation log}
    }
}
```
The event parameters are as detailed below:

| Field | Description | Data Type |
| --------------- | ------------------------------------------------------------ | ---------- |
| specversion     | Event structure version (CloudEvents version. Currently, only CloudEvents - Version 1.0 is supported.)        | String     |
| id              | ID returned by `PUT Event`.                                   | String     |
| type            | Type of the event input through `PUT Event`. CloudAudit events are classified into three types based on the event source: `${Product name abbreviation}:CloudEvent:ApiCall`, `${Product name abbreviation}:CloudEvent:ConsoleCall`, `${Product name abbreviation}:CloudEvent:MiniProgramCall`. | String     |
| source          | Event source (which is required for a Tencent Cloud service event and is the abbreviation of `subject`). The value is `xxx.cloud.tencent` by default for a Tencent Cloud service. | String     |
| subject        | Event source details, which can be customized. QCS description such as `qcs::dts:ap-guangzhou:appid/uin:xxx` is used for a Tencent Cloud service by default. | String     |
| time           | Event time, which is a GMT+0 timestamp in milliseconds such as `1615430559146`.         | Timestamp  |
| datacontenttype | Data structure declaration.                                               | String     |
| region          | Region information.                                                   | String     |
| data            | Details of the event input through `PUT Event`. For a CloudAudit event, pass in the complete CloudAudit log here.                                   |  Json     |

## Call Method
Before receiving CloudAudit events, make sure that you have **activated the CloudAudit service and created related service roles**.

1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb) and open the **Tencent Cloud service event bus** under the **Guangzhou region**.
![](https://qcloudimg.tencent-cloud.cn/raw/a0c6a84612400e9194b6d67e8b3fc265.png)
2. On the event bus details page, select to enable CloudAudit.
3. On the **Event Rule** page, select an event bus, create an event rule, filter event types, and bind delivery targets. For detailed directions, see [Creating Event Rule](https://intl.cloud.tencent.com/document/product/1108/42289).
