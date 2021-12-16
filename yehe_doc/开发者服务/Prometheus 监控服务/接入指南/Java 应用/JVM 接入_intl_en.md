## Overview

When using the Java programming language, you need to monitor JVM performance. TMP collects the JVM monitoring data exposed by applications and provides an out-of-the-box Grafana dashboard for it.

This document uses deploying a Java application in TKE as an example to describe how to use TMP to monitor the application status.

>?If you have already used Spring Boot as the development framework, please see Spring Boot Integration.

## Prerequisites

- Create a TKE [cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- [Use a private image repository to manage application images](https://intl.cloud.tencent.com/document/product/457/9117).

## Directions

>? As a major programming language, Java has a comprehensive ecosystem, where [Micrometer](https://micrometer.io/) has been widely used as a metric timestamping SDK. This document uses Micrometer as an example to describe how to monitor JVM.


### Modifying application dependencies and configuration

#### Step 1. Modify POM dependencies 

Add Maven dependencies to the `pom.xml` file and adjust the version as needed as follows:

<dx-codeblock>
::: xml 
<dependency>
    <groupId>io.prometheus</groupId>
    <artifactId>simpleclient</artifactId>
    <version>0.9.0</version>
</dependency>
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
    <version>1.1.7</version>
</dependency>
:::
</dx-codeblock>

#### Step 2. Modify the code

When the project is started, add the corresponding monitoring configuration. In addition, Micrometer also provides the collection of some common metrics, which are in the `io.micrometer.core.instrument.binder` package and can be added as needed as follows:

````java
public class Application {
    // It can be used in custom monitoring as a global variable
    public static final PrometheusMeterRegistry registry = new PrometheusMeterRegistry(PrometheusConfig.DEFAULT);
    static {
        // Add a global Prometheus label. We recommend you add the corresponding application name to it
        registry.config().commonTags("application", "java-demo");
    }

    public static void main(String[] args) throws Exception {
        // Add JVM monitoring
        new ClassLoaderMetrics().bindTo(registry);
        new JvmMemoryMetrics().bindTo(registry);
        new JvmGcMetrics().bindTo(registry);
        new ProcessorMetrics().bindTo(registry);
        new JvmThreadMetrics().bindTo(registry);
        new UptimeMetrics().bindTo(registry);
        new FileDescriptorMetrics().bindTo(registry);
        System.gc(); // Test GC
        try {
            // Expose the Prometheus HTTP service. If it already exists, you can use the existing HTTP server
            HttpServer server = HttpServer.create(new InetSocketAddress(8080), 0);
            server.createContext("/metrics", httpExchange -> {
                String response = registry.scrape();
                httpExchange.sendResponseHeaders(200, response.getBytes().length);
                try (OutputStream os = httpExchange.getResponseBody()) {
                    os.write(response.getBytes());
                }
            });

            new Thread(server::start).start();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

>?As monitoring of JVM GC pauses is implemented through the GarbageCollector Notification mechanism, the monitoring data will be generated only after a GC occurs. The above sample actively calls `System.gc()` to make the test more straightforward.

#### Step 3. Perform local verification

After the application is started locally, you can access the metric data of the Prometheus protocol through `http://localhost:8080/metrics`.


### Releasing application to TKE

#### Step 1. Configure a Docker image environment locally

If you have already configured a Docker image environment locally, proceed to the next step; otherwise, configure one as instructed in [Getting Started](https://intl.cloud.tencent.com/zh/document/product/1051/38866).


#### Step 2. Package and upload the image

1. Add `Dockerfile` in the root directory of the project. Please modify it based on your actual project conditions as follows:
<dx-codeblock>
:::  Dockerfile
  FROM openjdk:8-jdk
  WORKDIR /java-demo
  ADD target/java-demo-*.jar /java-demo/java-demo.jar
  CMD ["java","-jar","java-demo.jar"]
:::
</dx-codeblock>
2. Package the image by running the following command in the project root directory. You need to replace `namespace`, `ImageName`, and `image tag` as needed.
<dx-codeblock>
:::  bash
 mvn clean package
  docker build . -t ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[image tag]
  docker push ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[image tag]
:::
</dx-codeblock>
<b>Below is a sample:</b>
<dx-codeblock>
:::  bash
 mvn clean package
  docker build . -t ccr.ccs.tencentyun.com/prom_spring_demo/java-demo:latest
  docker push ccr.ccs.tencentyun.com/prom_spring_demo/-demo:latest
:::
</dx-codeblock>

#### Step 3. Deploy the application

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1) and select the container cluster for deployment.
2. Select *Workload** > **Deployment** to enter the Deployment management page and select the corresponding `namespace` to deploy the service. Use the following YAML configuration to create the corresponding Deployment:
>?If you want to create in the console, please see Spring Boot Integration.
<dx-codeblock>
:::  yaml
apiVersion: apps/v1
kind: Deployment
metadata:
    labels:
      k8s-app: java-demo
    name: java-demo
    namespace: spring-demo
spec:
    replicas: 1
    selector:
      matchLabels:
        k8s-app: java-demo
    template:
      metadata:
        labels:
          k8s-app: java-demo
    spec:
      containers:
      - image: ccr.ccs.tencentyun.com/prom_spring_demo/java-demo
        imagePullPolicy: Always
        name: java-demo
        ports:
        - containerPort: 8080
          name: metric-port
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      imagePullSecrets:
      - name: qcloudregistrykey
      restartPolicy: Always
      schedulerName: default-scheduler
      terminationGracePeriodSeconds: 30
:::
</dx-codeblock>

#### Step 4. Add a scrape task

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click a **cluster ID** in the TKE cluster list to enter the **Integrate with TKE** page.
3. In **Scrape Configuration**, add `Pod Monitor` to define a Prometheus scrape task. Below is a sample YAML configuration:
<dx-codeblock>
:::  yaml
  apiVersion: monitoring.coreos.com/v1
  kind: PodMonitor
  metadata:
    name: java-demo
    namespace: cm-prometheus
  spec:
    namespaceSelector:
      matchNames:
      - java-demo
    podMetricsEndpoints:
    - interval: 30s
      path: /metrics
      port: metric-port
    selector:
      matchLabels:
        k8s-app: java-demo
:::
</dx-codeblock>

#### Step 5. View the monitoring information

1. In **Integration Center** in the target TMP instance, find JVM monitoring, install the corresponding Grafana dashboard, and then you can enable the JVM monitoring dashboard.
2. Access the Grafana address of your TMP instance to view the application monitoring dashboard in **Dashboards > Manage > Application**.
	- **Application JVM**: monitoring data of the status of all instances under an application. If you find a faulty instance, you can view its monitoring information at any time.
	- **Instance JVM**: detailed monitoring data of a single instance JVM.
	![](https://main.qcloudimg.com/raw/e440a4b784bb31d02aafb60cbca929f2.png)
	![](https://main.qcloudimg.com/raw/6472032f91fb7f8081eb61a7a935c9d3.png)
