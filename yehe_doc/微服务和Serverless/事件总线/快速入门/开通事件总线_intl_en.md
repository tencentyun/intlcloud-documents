Before using EventBridge, you need to activate it on the product page. This document describes how to activate and use EventBridge.




## Directions

1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb) and activate the service and create a role as prompted (these operations must be performed with the **root account**).
2. After creating a service role, you can use the EventBridge features to create relevant resources.




## EventBridge Overview

The workflow of message processing in EventBridge is as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/dcfee21b28ead491bff4f68e9cc986a1.png)

#### Event source

An event source publishes produced events to EventBridge. A connector is a method to capture events and can pull event information after simple configuration. For more information, please see [Event Source](https://intl.cloud.tencent.com/document/product/1108/42274).

#### Event bus

It receives events from event sources. There are two types of event buses:

- Tencent Cloud service event bus: it can automatically capture Tencent Cloud service events and cannot be manually created by yourself.
- General event bus: it does not capture Tencent Cloud service events by default, which needs to be implemented through a connector or the `PutEvent` API.

For more information, please see [Event Bus](https://intl.cloud.tencent.com/document/product/1108/42284).

#### Event rule

An event rule is used to filter, convert, and route events to the specified event targets. It is the main carrier as well as an indispensable step of event target configuration. For more information, please see [Event Rule](https://intl.cloud.tencent.com/document/product/1108/42287).
