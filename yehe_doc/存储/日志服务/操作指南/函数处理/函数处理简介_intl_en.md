## Function processing

CLS can send data in a log topic to SCF for processing through a [CLS trigger](https://intl.cloud.tencent.com/document/product/583/38845) to satisfy the needs of various use cases, such as log processing and log cleansing as detailed below:


| Function Processing Scenario | Description |
| ------------------------------------------------------------ | --------------------------------------- |
| [ETL log processing](https://www.tencentcloud.com/document/product/614/38884) | Log data is cleansed, processed, or transformed through SCF.  |


>! Data is shipped to SCF, which incurs corresponding computing fees. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
>


The source log data can be submitted to SCF through a CLS function trigger, and then data processing and analysis, event triggering, and auto scaling can be implemented through function computing of Serverless Framework. The entire workflow requires no Ops and is pay-as-you-go.

## Advantages of function processing

- Data can be collected, stored, processed, analyzed, and displayed in a one-stop manner
- Log processing tasks are fully managed and can be triggered regularly and retried automatically
- More and more built-in function templates are added to reduce the development costs for log processing in popular use cases
- Data processing logic and custom code logic are provided based on SCF
- Computing power is provided based on SCF, with features such as auto scaling, Ops-free usage, and pay-as-you-go billing

