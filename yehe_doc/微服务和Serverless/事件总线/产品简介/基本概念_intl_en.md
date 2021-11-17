### Event

It is a data record of a status change.

### Event Source

It is a source that produces an event. The types of event sources include:
- **Tencent Cloud service**: Tencent Cloud services connected to EventBridge as an event source.
- **Custom application**: your applications.

### Event Bus

It receives events from event sources. The types of event buses include:
- **Tencent Cloud service event bus**: you can choose to create a Tencent Cloud service event bus to receive events from the Tencent Cloud services you use.
- **Custom bus**: it is an event bus that you create and manage by yourself and is used to receive events from your applications. Events of your applications can be published only to custom buses.

### Event Rule

It is used to monitor events of the specified types. When a matched event occurs, it will be routed to the event target associated with the corresponding event rule. A rule can be associated with one or multiple event targets and contains:
- **Event match**: matched **event pattern**, which decides what events can be sent to the associated event targets.
- **Event target**: event processing terminal that consumes events.

### Event Pattern

It is a module that filters events. An event pattern can filter all fields of CloudEvents including `data` and is described in JSON format.

### Event Target

It is an event processing terminal that consumes events. Event targets are generally Tencent Cloud services.

### Connector

It actively pulls events from the specified event sources and pushes them to custom buses in EventBridge.
