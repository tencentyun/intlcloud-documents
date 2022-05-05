A connector is mainly used to proactively pull events from event sources and push them to a custom event bus in **standard format**. With it, you don't need to care about the underlying consumer delivery logic. You can bind one or more connectors in the event bus to automatically pull event content from message queues and gateways and push the content to the specified event bus.



- EventBridge connectors support the following event sources:
  - TDMQ. For the configuration method, see [TDMQ Connector](https://intl.cloud.tencent.com/document/product/1108/42278).
  - API Gateway over HTTP. For the configuration method, see [API Gateway Connector](https://intl.cloud.tencent.com/document/product/1108/42279).
  - CKafka. For the configuration method, see [CKafka Connector](https://intl.cloud.tencent.com/document/product/1108/42280).
  - SaaS event delivery (provided by EIS). For the configuration method, see [SaaS Connector](https://intl.cloud.tencent.com/document/product/1108/42281).
- EventBridge provides the following connector management capabilities:
  - Creating connectors
  - Viewing connectors
  - Editing connectors
  - Starting connectors
  - Stopping connectors
  - Deleting connectors
