### What are the differences between web function and event function?
  As a new function type, web function can be directly triggered by HTTP requests, breaking through the limit of JSON event format required by the current event function type. It has more flexible application scenarios and delivers a development experience much similar to that of native web services.

### What are the use cases of web function?
  Web function focuses on optimization of web service scenarios and can directly send HTTP requests to URLs to trigger function execution. You can use SCF to develop web services or quickly migrate your local web framework to Tencent Cloud.

### How is web function billed?
  As a new type of SCF function, web function is billed in the same way as event function. Both of them are billed by the number of invocations, resource usage, and public network outbound traffic. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).

### What is a bootstrap file? How do I write it?
  A web function runs in the image environment built in it based on the standard programming language. You must create an executable file `scf_bootstrap` to start your web server, and then package the file with your code files for deployment to create a web function. During actual request processing, your `scf_bootstrap` file will start the service first, after which your web server will receive all HTTP requests by listening on the specified `9000` port, forward them to the backend service for logic processing, and return the responses to end users.

### Can I simulate the cloud environment during local development?
  Currently, the standard SCF runtime environment image has been opened up. For directions on how to use it, please see [Using Container Image](https://cloud.tencent.com/document/product/583/50826). You can select an appropriate image tag for local development and testing based on your actual development scenario. Before deploying a web function, please make sure that your project can be normally started in the local image.

### Why don't some header requests work?
  When an HTTP request is sent, certain header fields will be entered automatically by API Gateway and cannot be customized, because information exchange between the function and gateway has certain requirements and capability limits. Such fields mainly include the following:
  - `connection` field
  - Custom fields starting with `X-SCF-`

### How do I quickly troubleshoot function execution failures?
  You can quickly identify the cause of failure and find the solution based on the returned error code. For more information, please see [Common Error Codes and Solutions](https://cloud.tencent.com/document/product/583/56125#.E5.B8.B8.E8.A7.81.E9.94.99.E8.AF.AF.E7.A0.81.E8.A7.A3.E5.86.B3.E6.96.B9.E6.B3.95).


