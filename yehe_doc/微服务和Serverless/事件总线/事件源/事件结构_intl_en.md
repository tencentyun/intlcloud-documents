An event is a data record of a status change. This document describes the details of event parameters in EventBridge.

Event release from an event source to EventBridge needs to comply with CloudEvents specifications. For more information, please see [CloudEvents - Version 1.0](https://github.com/cloudevents/spec/blob/v1.0/spec.md?spm=a2c4g.11186623.2.2.749c6781ZcKk8R&file=spec.md).

Below is a sample structure of event release from an event source to EventBridge:


<dx-codeblock>
:::  json
{
   "specversion":"0",
   "id":"13a3f42d-7258-4ada-da6d-023a333b4662",
   "type":"cos:created:object",
   "source":"cos.cloud.tencent",
   "subjuect":"qcs::cos:ap-guangzhou:uid1250000000:bucketname",
   "time":"1615430559146",
   "region":"ap-guangzhou",
   "datacontenttype": "application/json;charset=utf-8",
   "data":{
      $data_value
   }
}
:::
</dx-codeblock>




The event parameters are as detailed below:

| Field | Description | Data Type |
| --------------- | ------------------------------------------------------------ | ---------- |
| specversion     | Event structure version (CloudEvents version, which is 1.0.2 currently).        | String     |
| id              | ID returned by `PUT Event`.                                   | String     |
| type            | Type of the event input through `PUT Event`. The value is `COS:Created:PostObject` by default for a Tencent Cloud service. Different types are separated with colons. | String     |
| source          | Event source (which is required for a Tencent Cloud service event and is the abbreviation of `subjuect`). The value is `xxx.cloud.tencent` by default for a Tencent Cloud service. | String     |
| subjuect        | Event source details, which can be customized. QCS description such as `qcs::dts:ap-guangzhou:appid/uin:xxx` is used for a Tencent Cloud service by default. | String     |
| timer           | Event time, which is a GMT+0 timestamp in milliseconds such as `1615430559146`.         | Timestamp  |
| datacontenttype | Data structure declaration.                                               | String     |
| region          | Region information.                                                   | String     |
| data            | Details of the event input through `PUT Event`.                                   | String     |



There are two types of events published from event sources to EventBridge:

- **Tencent Cloud service event**
  Tencent Cloud services are automatically connected to EventBridge as event sources.
- **Custom application event**
  When connecting your application as an event source, you need to configure the corresponding API/SDK for connection.
  
  
  
