- gRPC is a high-performance open-source remote procedure call (RPC) framework as well as a language/platform-neutral RPC system designed for mobile devices and HTTP/2. Currently, it supports the following programming languages: C, C++, C#, Node.js, Python, Ruby, Objective-C, PHP, Java, and Go.
- In gRPC, a client application can directly call methods on a server application on a different machine as if it was a local object. gRPC is based around the idea of defining a service, specifying the methods that can be called remotely with their parameters and return types. The server implements this API and runs a gRPC server to handle client calls.
- The gRPC calling method used by GSE is bidirectional streaming RPC.

>?For more information on gRPC, please see [gRPC official documentation](http://doc.oschina.net/grpc) and [gRPC@Linux Foundation](https://www.grpc.io/).

## Integrating gRPC Framework

1. Install gRPC.
2. Define the service.
3. Generate the gRPC code.
4. Integrate the game process.
5. Launch the server for GSE to call.
6. Connect the client to the gRPC server of GSE.

>?
>- For the specific call logic for C++, please see [gRPC - C++ Tutorial](https://intl.cloud.tencent.com/document/product/1055/37408).
>- For the specific call logic for C#, please see [gRPC - C# Tutorial](https://intl.cloud.tencent.com/document/product/1055/37409).
>- For the specific call logic for Go, please see [gRPC - Go Tutorial](https://intl.cloud.tencent.com/document/product/1055/37410).
>- For the specific call logic for Java, please see [gRPC - Java Tutorial](https://intl.cloud.tencent.com/document/product/1055/37411).
>- For the specific call logic for Lua, please see [gRPC - Lua Tutorial](https://intl.cloud.tencent.com/document/product/1055/37412).
>- For the specific call logic for Node.js, please see [gRPC - Node.js Tutorial](https://intl.cloud.tencent.com/document/product/1055/37413).
