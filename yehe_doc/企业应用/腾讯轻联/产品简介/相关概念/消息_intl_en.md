Key concepts of iPaaS include integration apps, messages, components, and security gateways. This document describes messages.

A message is a carrier of runtime data such as metadata in iPaaS. Messages are transferred between components in a flow according to the predefined logic. When a trigger begins the execution of a flow, it will encapsulate the raw input data into a message and pass it in to a component as parameters. After processing the message, the component will return a new message, which will be the input to the next component, and so on until the last component in the flow ends its execution and returns a message with the returned values of the entire flow. A message consists of the following parts:
- **Message content**: Contains the body of the message (`payload`) and metadata (`attribute`). The former is the core information, while the latter is auxiliary information.
- **Message variable**: Indicates the intermediate value stored temporarily during message transfer in the flow.
- **Error content**: An error.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/LwBP053_%E6%B6%88%E6%81%AF_03.jpg)
