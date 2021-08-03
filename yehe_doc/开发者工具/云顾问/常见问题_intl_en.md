### Will authorization obtain the customer managed CMKs?

No. No. Based on the authorization mechanism of CAM [Service Role](https://intl.cloud.tencent.com/document/product/598/19421), Tencent Cloud Advisor obtains only temporary keys to read cloud resource configurations. Information about your keys will not be obtained.

### Will assessments affect service performance?

No. No. Advisor uses cloud APIs to obtain resource configurations for resource assessments, and business data stream is not involved. Therefore, service performance will not be affected.

### Will Advisor modify the resource configurations?

No. No. Advisor only reads the resource configurations for risk assessment using the minimum permissions. It does not modify your resource configurations.

### How can I ignore an assessment item?

Go to **Settings** > **Assessment Item Configurations** and click the switch button to disable the item you want to ignore.

### How can I ignore a cloud resource?

In the assessment detail page, click **Ignore** for the cloud resource you want to ignore. In this way, this resource will be ignored in the next assessment.

### 云顾问的巡检频率？
开通云顾问后，系统会每天做一次自动巡检，客户可在控制台下载最近一天的巡检报告，也可以在控制台页面操作“开始评估”，手工发起巡检。
