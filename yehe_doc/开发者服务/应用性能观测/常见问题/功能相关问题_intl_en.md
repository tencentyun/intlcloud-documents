[](id:que1)
### What programming languages does APM support?
APM supports Java, PHP, Go, Python, and C++, with more to come.

[](id:que2)
### What frameworks does APM support?
APM supports Tomcat, Spring Boot, gRPC, and Dubbo. If you use other frameworks, you can collect and report data with other open-source SDKs and view it in APM.

[](id:que3)
### Can APM monitor clusters at other cloud vendors?
APM supports hybrid deployment. As long as the agent can access the public network, it can report service information at the public network reporting address provided by APM. In this way, you can monitor applications deployed in clusters at other cloud vendors.

[](id:que4)
### How does distributed tracing work?
It generates a trace ID for each request, passes through the entire call process, and then forms a complete call trace based on trace IDs.

[](id:que5)
### Will the probe intrude business code?
APM's probe does not intrude business code. For different languages, you need to install the corresponding agent or import the corresponding plugin to start monitoring your service.


### How do I access a Java application in APM?
You only need to download and install the Java agent in your service runtime environment. Then, configure the reporting token, reporting address, and application name to start monitoring.


### How do I access a Go application in APM?
Install the instrumentation plugin in your Go project and download the agent. Then, configure the reporting token, reporting address, and application name to start monitoring.

### How do I access a PHP application in APM?
You only need to download and install the PHP agent in your service runtime environment. Then, configure the reporting token, reporting address, and application name to start monitoring.

### What are the differences between access methods?
Access via the probe (agent) is non-intrusive to the code and only requires modifying the configuration file.
For certain programming languages, no probe is currently available in the open-source ecosystem, which makes access via the SDK necessary. Specifically, you need to import the SDK, instrument remote calls, and modify the reporting configuration.
If you use SkyWalking or other open-source products, you only need to modify the configuration to report monitoring data, with no further component Ops needed.


### Is APM compatible with the OpenTracing protocol?
Yes. You can directly report monitoring data through the agent if you have custom OpenTracing instrumentation.

### Is the APM agent installed on a node or in a container?
Either will do.

### What is trace storage?
It refers to each request trace stored in APM.

### How long is the trace retention period in APM?
It is 3 days by default during the trial and can be 3, 7, 15, or 30 days after billing officially starts.



