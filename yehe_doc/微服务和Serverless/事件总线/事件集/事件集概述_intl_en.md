An event bus receives events from event sources and can be used normally after being bound to a specific event rule. This document describes the types of event buses.



The types of event buses in EventBridge include:

- Tencent Cloud service event bus: You can choose to use the Tencent Cloud service event bus during event bus creation to receive events from Tencent Cloud services. It cannot be manually created by yourself. Tencent Cloud service events can be published only to this event bus.
- Custom event bus: It is an event bus that you create and manage by yourself and is used to receive events from your applications. Events of your applications can be published only to custom buses.

To ensure the traceability of each event, you can enable the [linkage tracing]() feature when creating an event bus.
