By using an event rule, you can deliver collected events to the specified delivery target for processing and consumption. Currently, EventBridge allows you to set [SCF](https://intl.cloud.tencent.com/zh/products/scf) as a delivery target and provides multiple preconfigured templates to help you deliver events.

### Template Function-based Delivery
Select a function template, and EventBridge will create a target function for event delivery for you based on the provided default template. Currently, two function templates are available: CKafka and EIS delivery templates. You can select and configure them in **Event Rule** > **Event Target**.
<dx-tabs>
::: CKafka Delivery Template
<dx-alert infotype="notice" title="">
If your target CKafka instance has a username and password, please ensure that the entered information is correct; otherwise, event delivery may fail.
</dx-alert>
![](https://qcloudimg.tencent-cloud.cn/raw/cc505031a1692e49461ff8ed7b980867.png)
:::
::: SaaS Delivery Template
:::
</dx-tabs>



### Custom Function Delivery
In addition to using templates, you can deliver events to your created custom functions to implement more business logic.
![](https://qcloudimg.tencent-cloud.cn/raw/0c5cadf332064f4b21802891093637a0.png)

### Enabling Batch Delivery
If the delivery target is SCF, EventBridge will support batch delivery, and you can select a delivery method based on your actual business requirements:
![](https://qcloudimg.tencent-cloud.cn/raw/99bab9b7109c0def1fbfdaf386ad88f1.png)
Batch delivery parameter description:

- **Maximum waiting time:** The maximum waiting time for each function trigger. Value range: 0–60s. Default value: 0.
- **Maximum messages**: The maximum number of messages that can be pulled and batch delivered to the current function at a time, which can be up to 10,000 currently. According to the message size and writing speed, the number of messages delivered when the function is triggered each time may not always reach the maximum number; instead, it is a variable value between 1 and the maximum number.




>! After the batch delivery feature is enabled, events will be delivered together as an array. Please ensure that the event consumer is compatible with such format.
<dx-tabs>
::: Event format with batch delivery not enabled
<dx-codeblock>
:::  json
{
    "specversion": "1.0.2",
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
    "type": "connector:apigw",
    "source": "apigw.cloud.tencent",
    "subject": "qcs::apigw:ap-guangzhou:uid1250000000/appidxxx:Serverid/Appid",
    "time": "1615430559146",
    "region": "ap-guangzhou",
    "datacontenttype": "application/json;charset=utf-8",
    "data":{
            $data_value
         }
}
:::
</dx-codeblock>
:::
::: Event format with batch delivery enabled
<dx-codeblock>
:::  json
{
   "EventList":[
      {
        "specversion": "1.0.2",
        "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
        "type": "connector:apigw",
        "source": "apigw.cloud.tencent",
        "subject": "qcs::apigw:ap-guangzhou:uid1250000000/appidxxx:Serverid/Appid",
        "time": "1615430559146",
        "region": "ap-guangzhou",
        "datacontenttype": "application/json;charset=utf-8",
        "data":{
              $data_value
         }
      },
      {
        "specversion": "1.0.2",
        "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
        "type": "connector:apigw",
        "source": "apigw.cloud.tencent",
        "subject": "qcs::apigw:ap-guangzhou:uid1250000000/appidxxx:Serverid/Appid",
        "time": "1615430559146",
        "region": "ap-guangzhou",
        "datacontenttype": "application/json;charset=utf-8",
        "data":{
              $data_value
         }
      }
   ]
}
:::
</dx-codeblock>
:::
</dx-tabs>

