## 函数处理

日志服务（Cloud Log Service，CLS）可以将日志主题中的数据通过 [CLS 日志触发器](https://intl.cloud.tencent.com/document/product/583/38845) 投递至云函数进行处理，以满足日志处理/日志清洗等应用场景需求，如下：


| 函数处理场景                                               | 描述说明                                |
| ------------------------------------------------------------ | --------------------------------------- |
| [ETL 日志处理](https://www.tencentcloud.com/document/product/614/38884) | 日志数据通过云函数进行日志清洗，日志处理，格式转换等操作。  |


>! 数据投递至云函数，云函数侧将产生相应的计算费用，计费详情请参见云函数 [计费概述](https://intl.cloud.tencent.com/document/product/583/17299)。
>


通过 CLS 函数触发器将日志源信息提交到云函数，再通过 serverless 无服务架构的函数计算提供数据处理、分析，事件触发，弹性伸缩，无需运维，按需付费。

## 使用函数处理优势

- 提供一站式采集、存储、处理、分析和展示。
- 全托管日志处理任务，按时间周期进行触发执行，自动重试。
- 持续增加内置函数模板，降低主流需求下的日志处理开发成本。
- 基于云函数提供数据处理及自定义代码逻辑。
- 基于云函数提供计算能力，拥有弹性伸缩，免运维，按需付费等特性。

