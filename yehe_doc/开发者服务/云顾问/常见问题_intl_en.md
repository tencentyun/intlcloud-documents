### Will authorization obtain the customer managed CMKs?

No. Based on the authorization mechanism of CAM [Service Role](https://intl.cloud.tencent.com/document/product/598/19421), Tencent Smart Advisor obtains only temporary keys to read cloud resource configurations. Information about your keys will not be obtained.

### Will assessments affect service performance?

No. Tencent Smart Advisor uses cloud APIs to obtain resource configurations for resource assessments, and business data stream is not involved. Therefore, service performance will not be affected.

### Will Tencent Smart Advisor modify the resource configurations?

No. Tencent Smart Advisor only reads the resource configurations for risk assessment using the minimum permissions. It does not modify your resource configurations.

### How can I ignore an assessment item?

Go to **Assessment Settings** > **Assessment Items** and click the switch button to disable the item you want to ignore.

### How can I ignore a cloud resource?

In the **Assessment Items** page, click **Ignore** for the cloud resource you want to ignore. In this way, this resource will be ignored in the next assessment.

### How often does Tencent Smart Advisor conduct inspections?
After Tencent Smart Advisor is activated, it will conduct an automatic inspection once a day. You can download yesterday's inspection report or click **Start Assessment** to manually initiate an inspection in the [Tencent Smart Advisor console](https://console.cloud.tencent.com/advisor).
