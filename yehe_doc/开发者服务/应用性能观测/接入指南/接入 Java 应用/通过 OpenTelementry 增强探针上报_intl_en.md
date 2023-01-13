The Java agent is developed based on the bytecode enhancement technology and supports automatic instrumentation for data reporting. It includes and redistributes opentelemetry-java-instrumentation, an open-source project of CNCF, follows Apache License 2.0, and references the OpenTelemetry license.

OpenTelemetry is a set of tools, APIs, and SDKs used to monitor, generate, collect, and export telemetry data (metrics, logs, and traces) to help you analyze the performance and behaviors of your application. The OpenTelemetry community is active with rapid technology iterations and wide compatibility with mainstream programming languages, components, and frameworks, and its tracing capabilities constructed for cloud-native microservices and containers are very popular. Based on the Java bytecode enhancement technology, opentelemetry-java-instrumentation can implement automatic instrumentation for data reporting. APM is developed on top of opentelemetry-java-instrumentation to help you get more comprehensive call data and corresponding line number information.

This document describes how to report the data of a Java application with opentelemetry-java-instrumentation.


### Step 1. Get the endpoint and token
Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Java language and the OpenTelemetry data collection method.
Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)
<dx-alert infotype="explain" title="Reporting method description">
- Reporting over the private network: To use this reporting method, your service must run in a Tencent Cloud VPC. Direct connection through VPC can reduce the reporting traffic fees while avoiding the security risks in public network communication.
- Reporting over the public network: If your service is deployed locally or not in a Tencent Cloud VPC, you can report data in this method. However, it involves security risks in public network communication and incurs reporting traffic fees.
  </dx-alert>


### Step 2. Download opentelemetry-javaagent.jar 
>? opentelemetry-java-instrumentation supports automatic instrumentation in dozens of frameworks. For more information, see [Supported libraries, frameworks, application servers, and JVMs](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md?spm=a2c4g.11186623.0.0.1e455765eR4tEn&file=supported-libraries.md).

Download the Java agent [opentelemetry-javaagent.jar](https://github.com/TencentCloud/tencentcloud-opentelemetry-java.git).
![](https://qcloudimg.tencent-cloud.cn/raw/6176ee3745ffe0ad7c60c33ded2a4bf3.png)

### Step 3. Modify the reporting parameters
Report the trace data by modifying the VM startup parameters of Java.
```
-javaagent:/path/to/opentelemetry-javaagent.jar    // Change the path to the actual address of the downloaded file.
-Dotel.resource.attributes=service.name=<appName>,token=<token> // service.name: Service name. If the service is a Spring Cloud/Dubbo service, use the service name for this parameter.
-Dotel.exporter.otlp.endpoint=<endpoint>
```
>?
>- If you choose to directly report data, replace < token > with the token obtained in the prerequisites section, and replace <endpoint> with the endpoint of the corresponding region. When replacing parameter values, be sure to remove "<" and ">" and keep only the text.
>- If you choose to use the OpenTelemetry collector to forward data, delete -Dotel.exporter.otlp.headers=Authentication=< token > and change <endpoint> to your local service address.

### Step 4. Start your application
### Viewing application data
Log in to the [APM console](https://console.cloud.tencent.com/apm) to view the performance data in the application list.

