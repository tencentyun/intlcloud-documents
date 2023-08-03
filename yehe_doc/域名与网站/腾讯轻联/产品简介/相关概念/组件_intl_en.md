Key concepts of iPaaS include integration apps, messages, components, and security gateways. This document describes components.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/35Iz615_%E7%BB%84%E4%BB%B6.jpg)

## Overview
Components are the minimum units in flow orchestration and include logical components and connectors. Each node in a flow is a component. You can enter parameters or use other methods to configure the component as needed. 

## Components
### Logical components
Logical components encapsulate common coding logic, such as Set Variable (variable creation) and Choice (conditional branch execution). If you want to add a logic to a business process, you only need to add the corresponding component on the node and configure it. For example, after adding the Set Variable component, you only need to enter the variable name and value; after adding the Choice component, you can add and delete conditional branches and configure the execution condition for each branch.

Currently, logical components cover five logic scenarios: flow control, data processing, errors and logs, parallelism and concurrency, and functionality. 

| Logical Component | Description |
|:-: | :------ |
|Async|**Async** is a flow control component, where you can configure a subflow to execute an async task, which is similar to creating a thread. |
|Break|Break needs to be used together with the **For Each** or **While** component to break a loop. |
|Cache|**Cache** is used to cache the intermediate data generated during flow execution. Different flows in the same application can share the data cached in the **Cache** component. |
|Choice|**Choice** is a branch selection statement. Similar to if-else, it is used to execute actions by condition. |
|Continue|Similar to the **Break** component, **Continue** also needs to be used together with the **For Each** or **While** components. It is used to jump out of the current loop and execute the next loop. |
|Flow Reference|**Flow Reference** is used to reference other flows in the current application. Different from **Async**, **Flow Reference** is a sync action. It will continue to execute the next action only after the execution of the referenced flow is completed. |
|For Each|**For Each** is a loop control structure, which is similar to for/foreach in programming languages. In **For Each**, you can configure a subflow to process the specified data set in a loop but cannot specify the number of loops. |
|Logger|**Logger** is used to output logs in the console. Currently, it supports four log levels: **DEBUG**, **INFO**, **WARN**, and **ERROR**. |
|Parallel Foreach|**Parallel Foreach** is used to execute parallel tasks. It executes the same processing on data set elements in parallel. The number of parallel elements is subject to the configured maximum number of parallel elements. If the number of elements is less than or equal to the maximum number of parallel elements, the number of parallel elements is equal to the number of elements; otherwise, it is the configured maximum number. |
|Raise Error|**Raise Error** is used to report exceptions and stop flow execution. This component can be used alone or together with the **Try** component. |
|Remove Variable|The opposite of the **Set Variable** component, **Remove Variable** is used to delete the specified variable in `message`. |
|Scatter Gather|**Scatter Gather** can execute multiple tasks in parallel. This component has two core configuration items: the number of parallel tasks (2–8 currently) and worker. In each worker, a task to be executed can be configured. |
|Scheduler|**Scheduler** is used to trigger a flow at the scheduled time according to the configured rule. Its configuration contains one or more cron rules. When any cron rule matches the current time, the flow where the **Scheduler** component resides will be triggered. |
|Set Payload| **Set Payload** is used to set the `payload` attribute in `message`. It supports expressions and literal values. To enter a literal value, select the data type and enter the literal value in the input box. To enter an expression, select the `any` type and write an expression. |
|Set Variable| **Set Variable** is used to declare a variable and save it in `variables` in `message`, so that subsequent nodes can import it in the form of `msg.vars.get('name')`. |
|Synchronized| **Synchronized** is a distributed lock used to lock and protect concurrent requests. It can be used in scenarios with conflicting resource access requests. |
|Transform| **Transform** is used to orchestrate and convert the format of the data in `message`. It can modify `payload`, `attribute`, and `variable`. |
|Try| **Try** is used to capture errors. It can capture errors reported by a subflow executed in **Try** as well as system errors. It can also be used together with the **Raise Error** component to capture custom errors. |
|Until Successful| In **Until Successful**, you can configure a subflow to retry the subflow execution. It supports three retry modes: unconditional retry, retry based on success condition, and retry based on failure condition. |
|While| **While** is a loop component, which supports up to 10,000 loops. Unlike the **For Each** component, the **While** component doesn't rely on a data set for loop but uses conditional statements to determine whether the loop should continue. If the loop condition is `True`, the loop will continue until `False` is returned or the maximum number of loops is reached. |
|Compress| **Compress** is used to compress and decompress the data. It supports the following compression and decompression formats: DEFLATE, GZIP, and ZLIB. |

### Connectors
A connector is a comprehensive encapsulation of a system interaction protocol (common connectors such as Database) or a specific business system (application connectors such as Tencent Meeting), which contains authentication, protocol conversion, and feature APIs. You can use the Database connector to directly access a database or use the Tencent Meeting connector to directly call the APIs of Tencent Meeting with no need to understand how Tencent Meeting interacts with external systems or how API authentication works. A connector enables you to connect to your business systems at zero costs.

<dx-tabs>
::: Common connectors
A common connector is an encapsulation of a protocol such as HTTP, SOAP, Kafka, or MQ. You can select a protocol for system connection based on the actual conditions of your business system.
:::
::: Application connectors
An application connector is an encapsulation of a business system such as Tencent Meeting or WeCom, which contains the interaction protocols, authentication methods, and specific features (APIs) of the business system. It enables you to call the business system APIs at zero costs with no need to understand the connection content irrelevant to the business.

:::
::: Custom connectors
iPaaS provides a wide variety of preset connectors. If you cannot find the connector you want in the connector list, you can create your own connector and submit it for review. If it is approved, it will be published to iPaaS for use by you and other users.
:::
::: Connections
A connection is the dependency used by a connector. Different connectors require different configuration items. For example, for the HTTP Listener connector, you need to enter a listener domain name to specify the listener object; for the Tencent Meeting connector, you need to enter tenant credential information like `AppID` and `SecretKey` for third-party development to specify the user the connector belongs to. Moreover, connections can be used globally in an application. When creating a connector, you can select an existing connection as needed. 
:::
::: Actions
An action encapsulates the interactions that are initiated by an integration app, so as to complete process orchestration and message processing in a flow and output a new message after processing is completed.
:::
::: Triggers
A trigger encapsulates the interactions initiated by a third-party system and listened for by an integration app. It serves as the source in a flow and generates a message when receiving an interaction event from a third-party system. A trigger is used basically in the same way as an action.
:::
::: Expressions
An expression enables you to set variable values dynamically when executing a created flow. When creating a flow, you can use an expression in almost all text boxes during the flow configuration. It helps you import any system status value during flow execution. It can also be used to perform complex data processing and calculation to generate the expected result for further processing by downstream components.

:::
</dx-tabs>


