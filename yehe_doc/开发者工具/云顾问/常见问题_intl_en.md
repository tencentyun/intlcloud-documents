### Will the authorization get customer managed CMKs?

No. Based on the authorization mechanism of CAM [service role](https://intl.cloud.tencent.com/document/product/598/19421), Advisor gets only temporary keys to read cloud resource configurations. Information about your keys will not be obtained.

### Will assessments affect service performance?

No. Advisor uses TencentCloud APIs to get resource configurations for resource assessments, and business data stream is not involved. Therefore, service performance will not be affected.

### Will Advisor modify resource configurations?

No. Advisor only reads the resource configurations for risk assessment under the principle of least privilege. It does not modify your resource configurations.

### How do I ignore an assessment item?

Go to **Settings** > **Assessment Item Configurations** and click the switch button to disable the item you want to ignore.

### How do I ignore a cloud resource?

On the assessment detail page, click **Ignore** for the cloud resource you want to ignore. Then, this resource will be ignored in the next assessment.

### How often does Advisor conduct inspections?
After Advisor is activated, it will conduct an automatic inspection once a day. You can download yesterday's inspection report or click **Start Assessment** to manually initiate an inspection in the console.
