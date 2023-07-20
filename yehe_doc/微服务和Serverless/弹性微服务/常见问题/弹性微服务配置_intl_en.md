### Which languages does TEM support?
TEM currently supports microservice applications written in Java. You can make Docker images for non-microservice applications and uploading them to TEM. In this way, you can deploy applications written in any programming language in TEM.


### All my businesses are in CVM. Do I need to modify the code when migrating them to TEM?
TEM features non-intrusive integration with no business code changes required, which greatly reduces the migration costs. Taking Spring Cloud applications with ZooKeeper as the registry as an example, when you migrate them to TEM, you don't need to make any changes, which implements smooth migration imperceptible to users.


### How does TEM implement Ops-free operations?
TEM makes resources serverless, so that you no longer need to estimate the capacity or purchase machine resources. In addition, it also enables quick application deployment, automated monitoring, service governance, and other capabilities, lowering the Ops threshold of your microservices and thus implementing Ops-free operations.


### At what granularities can TEM automatically scale resources?
TEM supports auto scaling at finer resource granularities down to 0.25 CPU cores, which greatly reduces you resource costs.


### What monitoring metrics does TEM provide?
TEM currently provides basic monitoring capabilities (in the CPU and memory dimensions) and will add more metrics in business dimensions such as QPS, response delay, and slow query in the future.

### If I use TEM, can I still use other Tencent Cloud services such as TencentDB for Redis and CKafka?
TEM is perfectly compatible with other Tencent Cloud services such as TencentDB for Redis and CKafka for unrestricted access.


### What are the differences between TEM and TSF?
<table>
    <thead>
    <tr>
        <th>Comparison Dimension</th>
        <th>TSF</th>
        <th>TEM</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Positioning</td>
        <td>A microservice PaaS platform.</td>
        <td>A serverless microservice application PaaS platform.</td>
    </tr>
    <tr>
        <td>Supported programming languages and frameworks</td>
        <td>It supports Spring Cloud and Dubbo microservices through SDKs or in a non-intrusive way and is compatible with various programming languages based on Service Mesh.</td>
        <td>It supports mainstream programming languages and development frameworks.</td>
    </tr>
    <tr>
        <td>Openness</td>
        <td>Low. By encapsulating each component, it provides an out-of-the-box service.</td>
        <td>High. It supports applications in various programming languages and integrates TSE, TAPM, Promethues, CLS, and CFS for you to select microservice and observability components flexibly.</td>
    </tr>
    <tr>
        <td>Migration costs</td>
        <td>High costs for migrating your microservice as a whole.</td>
        <td>Low costs for component replacement. It is cloud native and requires zero code modifications of your applications.</td>
    </tr>
    <tr>
        <td>Product features</td>
        <td>Service deployment, service lifecycle management, microservice registration and discovery, service governance, configuration management, etc.</td>
        <td>Application release, application hosting, microservice registration and discovery, microservice governance, elastic scalability, configuration management, and development efficiency management.</td>
    </tr>
    <tr>
        <td>Coupling degree of each feature</td>
        <td>High</td>
        <td>Low</td>
    </tr>
    <tr>
        <td>Strengths</td>
        <td>It integrates service governance, application deployment, and log monitoring to provide comprehensive features at one stop.</td>
        <td>It is flexible and lightweight based on pluggable components. It is open source-oriented, Ops-free, and serverless and requires no modifications of your applications.</td>
    </tr>
    </tbody>
</table>

### How do I migrate a business deployed in TSF Serverless to TEM?
You can deploy the business again in TEM, which involves no zero code modifications. If you have any questions or need technical support, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

### When did TEM start to be billed?
It started to be billed on April 30, 2022.
