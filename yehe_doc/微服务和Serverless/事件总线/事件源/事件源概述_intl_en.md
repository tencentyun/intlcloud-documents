Event sources publish produced events complying with CloudEvents - Version 1.0 to EventBridge. For more information, see [Event Structure](https://intl.cloud.tencent.com/document/product/1108/42275).

EventBridge supports the following event source connection methods:



#### Tencent Cloud services

If you want to use the **Cloud Monitor events** and **CloudAudit events** generated by Tencent Cloud services as event sources, you only need to activate the corresponding Tencent Cloud services, and then the Tencent Cloud services will be automatically connected to EventBridge. By configuring the predefined event pattern and targets, you can publish events to the Tencent Cloud service event bus with ease. Then the events are filtered based on the event pattern and routed to the event targets. Currently, EventBridge supports the delivery and management of Cloud Monitor events and CloudAudit events. For more information, see [Tencent Cloud Service Event](https://intl.cloud.tencent.com/document/product/1108/46256).

#### Custom applications

If you want to connect a custom business as an event source, you need to configure your application for connection to EventBridge through the corresponding API/SDK. By creating a custom event bus and configuring a custom event pattern and event target, you can publish events generated by your application to the custom event bus, use the custom event pattern to filter them, and route them to the custom event target.



#### Connector

A connector is used to proactively pull events from event sources such as **message queue TDMQ** and push them to a custom event bus in **standard format**. With it, you don't need to care about the underlying consumption delivery logic. You can bind one or more connectors to a custom event bus to automatically pull event content from message queues and gateways and push the event content to the specified event bus. For more information about connectors, see [here](https://intl.cloud.tencent.com/document/product/1108/42277).



