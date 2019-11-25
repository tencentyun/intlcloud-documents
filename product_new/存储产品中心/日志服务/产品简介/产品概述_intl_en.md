
Cloud Log Service (CLS) is a centralized logging solution. You can stop worrying about scaling or other resource issues and access CLS within just five minutes. CLS offers solutions for collecting, storing, searching, and analyzing logs, helping you identify business issues, monitor metrics, ensure security, and simplify operations.

CLS is in beta. You can [submit an application form](https://cloud.tencent.com/act/apply/cloudlog) to try it out. Your application will be reviewed within 7 business days.

## Features
CLS has the following features.

- Log collection: collect logs to CLS from different log sources by using LogListener, API, etc.
- Log storage: store log data with CLS.
- Log index: enabling log index for log query can help you quickly identify log problems.
- Log shipping: you can ship specified logs to other cloud products to meet storage or other computing needs. For example, you can ship a log to a specified COS bucket to manage its lifecycle and meet the need for log auditing.

#### Log collection
CLS supports collecting logs by using LogListener and API, enabling you to easily collect log data from different regions, channels, platforms, and data sources in real time and collect logs from various Tencent Cloud products.
- LogListener real-time collection: use LogListener to collect logs. This method is easy to install, reliable, and secure. It supports most mainstream Linux operating systems, delivering high performance while occupying few resources.
- Collection via API: upload logs by calling an API, without the need to install LogListener. Multiple languages are supported.

#### Log index and query
- Real-time index: index collected log data in real time to enable data search.
- Excellent query performance: query results are returned within seconds. 100-million-level log data search and quick data locating are supported.
- Flexible query: features such as full-text search, multi-keyword search, and cross-topic query are supported.

#### Log shipping
- Shipping logs to COS: ship log data to COS buckets under your account to store and manage the log data.
