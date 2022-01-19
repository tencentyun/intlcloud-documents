

The function processing service allows you to quickly complete complex log processing tasks such as execution log collection, ETL, and message dumping for various Tencent Cloud services like CVM. Function processing is an async process. All data collected into CLS can be delivered to SCF for consumption and processing through configurations. You only need to complete simple configurations in the CLS console to connect CLS to SCF.

The overall data processing flow is as follows:

![](https://main.qcloudimg.com/raw/b1502b1adad1baf4ecc8a2a599d746df.svg)

The source log data can be submitted to SCF through a CLS function trigger, and then data processing and analysis, event triggering, and auto scaling can be implemented through function computing of Serverless Framework. The entire workflow requires no OPS and is pay-as-you-go.

## Advantages of Function Processing

- Data can be collected, stored, processed, analyzed, and displayed in a one-stop manner
- Log processing tasks are fully managed and can be triggered regularly and retried automatically
- More and more built-in function templates are added to reduce the development costs for log processing in popular use cases
- Data processing logic and custom code logic are provided based on SCF
- Computing power is provided based on SCF, with features such as auto scaling, OPS-free usage, and pay-as-you-go billing

## Function Processing Practices

CLS can send data in a log topic to SCF for processing through a [CLS trigger](https://intl.cloud.tencent.com/document/product/583/38845)  to satisfy the needs of various use cases, such as log processing and log cleansing as detailed below:


| Function Processing Scenario | Description |
| ------------------------------------------------------------ | --------------------------------------- |
| [Log ETL](https://intl.cloud.tencent.com/document/product/614/38884) | Log data is cleansed, processed, or transformed through SCF |



>! Data is delivered to SCF, which incurs corresponding computation fees. For billing details, please see SCF [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
