## Overview

In this document, we describe how to manage a typical microservice project in multi-cloud and multi-cluster scenarios by a sample of a Dubbo project named “Q Cloud Book Mall” (QCBM). We implement distribution, management, scheduling, migration and canary update of the application among multiple clusters by a few steps, and finally build a complete microservice application with multi-cluster disaster recovery capability.


## Preparations
Please confirm that you have completed the following steps before deploying the service.
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- Check the QCBM project to learn about Dubbo microservice architecture. For more information, see [QCBM Project](https://github.com/TencentCloud/container-demo/tree/main/dubbo-on-tke).
- Learn about basics of TKE. For details, see [TKE Introduction](https://intl.cloud.tencent.com/document/product/457/6759).


## Architecture

QCBM is an online book mall Demo project developed by using microservice architecture and Dubbo framework. For more information, see [QCBM Project](https://github.com/TencentCloud/container-demo/tree/main/dubbo-on-tke).

We deploy QCBM in multiple clusters to manage it in a unified way. The overall architecture is divided into three layers, including access layer, application layer and data layer. With the corresponding control and monitoring add-ons, we can manage QCBM in multiple clusters and implement multi-site active-active disaster recovery.
The figure of overall architecture is as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/88f9e155e4686d30c78e3ffced1f0702.png)

**Access layer** implements traffic access and forwarding by using Tencent Cloud CLBs or LBs provided by other cloud vendors in conjunction with K8s ingress and service. Also, a nginx can be configured for traffic access and forwarding. In this sample, we use [Tencent Cloud CLBs](https://intl.cloud.tencent.com/zh/products/clb).

**Data layer** uses TencentDB for MySQL and TencentDB for Redis or database provided by other cloud vendors. Also, external MySQL and Redis can be integrated. In this sample, we use [TencentDB for MySQL](https://intl.cloud.tencent.com/zh/products/cdb) and [TencentDB for Redis](https://intl.cloud.tencent.com/zh/products/crs).

**Application layer** is composed of the following microservice applications. We deploy and release applications in multiple clusters through [Application Governance](https://intl.cloud.tencent.com/document/product/1144/45545), and perform canary update according to localization configurations of clusters.
- QCBM-Front: It is a frontend developed using react, and it is built and deployed based on 1.19.8 docker image officially provided by nginx.
- QCBM-Gateway: It is the API Gateway that receives HTTP requests from the frontend and converts them into Dubbo requests for the backend.
- User-Service: A microservice based on Dubbo. It provides features such as user registration, login and authentication.
- Favorites-Service: A microservice based on Dubbo. It provides features such as “Favorites”.
- Order-Service: A microservice based on Dubbo. It provides features such as order generation and query.
- Store-Service: A microservice based on Dubbo. It provides features such as book information storage.



## Directions

### Basic environment

1. Deploy the desired basic services (including MySQL, Redis, CLB, Nacos, TSW and others) on the platform by referring to the ways of building basic service clusters.
2. Create clusters for running of QCBM service. In this sample, we create two TKE clusters in **two regions**. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
>! In actual production environment, clusters may be located in different regions, availability zones and even be operated by different cloud vendors. Therefor, users need to ensure that the infrastructures affected by failures are controllable.
>

### Registering the clusters in Tencent Kubernetes Engine Distributed Cloud Center

Register the clusters in Tencent Kubernetes Engine Distributed Cloud Center. For more information, see [Registering a Cluster](https://intl.cloud.tencent.com/document/product/1144/45543).
In this document, we register clusters named “SPG-01” and “SPG-02”. After the registration, we check and find that they are in normal status.
![](https://qcloudimg.tencent-cloud.cn/raw/c3594ee42f039857246ebd78bcd12a99.png)

>! You need to activate **Tencent Kubernetes Engine Distributed Cloud Center** service when you access the Tencent Kubernetes Engine Distributed Cloud Center console for the first time. For more information, see [Getting Started on Tencent Kubernetes Engine Distributed Cloud Center](https://intl.cloud.tencent.com/document/product/1144/45540).


### Deploying multi-cluster applications

Create and manage multi-cluster applications. Deploy the QCBM application in multiple clusters. For more information, see [Application Management](https://intl.cloud.tencent.com/document/product/1144/45546).

#### Creating a distribution policy

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Distribution Policy** in the left sidebar.  
2. Click **Create** to create a distribution policy "qcbm-subscription". Select the target cluster on the page that appears. Here, we select the cluster "SPG-01", as shown in the figure below.
![](https://qcloudimg.tencent-cloud.cn/raw/a77ac7567ebfdb863854abe5cee7af0c.png)
3. Click **Create** to complete the creation. You can see that the distribution policy “qcbm-subscription” is created successfully.


#### Creating a namespace
We create a namespace named “qcbm” with reference to [QCBM Project](https://github.com/TencentCloud/container-demo/tree/main/dubbo-on-tke), and distribute it to the specified cluster according to the distribution policy.
>! The creation process is the same as that of creating a namespace in a single cluster. You should specify a distribution policy such as “qcbm-subscription” on the configuration page.
>

<dx-tabs>
::: Method 1: Via the console
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Namespace** > **Create**. Create a namespace named “qcbm”, and select qcbm-subscription as the distribution policy.
![](https://qcloudimg.tencent-cloud.cn/raw/bd9fdfb548fcbf586327fb293cff6e70.png)
3. Click **Create namespace**. The namespace qcbm is created and distributed to the specified cluster.
:::
::: Method 2: Using YAML
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Create via YAML**, and enter the following YAML configuration.
3. Click **Complete** to complete the creation. Select the distribution policy “qcbm-subscription”.
```yaml
  apiVersion: v1
  kind: Namespace
  metadata:
    name: qcbm
  spec:
    finalizers:
    - kubernetes
```
:::
</dx-tabs>


#### Creating a ConfigMap

You can create a ConfigMap named “qcbm-env” with reference to [QCBM Project](https://github.com/TencentCloud/container-demo/tree/main/dubbo-on-tke), and distribute it to the specified cluster according to the distribution policy.
>! The creation process is the same as that of creating a ConfigMap in a single cluster. You should specify a distribution policy such as “qcbm-subscription” on the configuration page.
>

<dx-tabs>
::: Method 1: Via the console
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Configuration management** > **ConfigMap** > **Create**, create a ConfigMap named “qcbm-env” and select qcbm-subscription as the distribution policy.
![](https://qcloudimg.tencent-cloud.cn/raw/bd3d52935f9b2ff10aa5dc8f3beca399.png)
3. Click **Create ConfigMap**. You can see that the ConfigMap is configured and distributed to the specified cluster.
:::
::: Method 2: Using YAML
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Create via YAML**, and enter the following YAML configuration.
3. Click **Complete** to complete the creation. Select the distribution policy “qcbm-subscription”.
```yaml
  apiVersion: v1
  data:
    MYSQL_HOST: ## Enter the actual value
    MYSQL_PORT: ## Enter the actual value
    NACOS_HOST: ## Enter the actual value
    NACOS_PORT: ## Enter the actual value
    REDIS_HOST: ## Enter the actual value
    REDIS_PORT: ## Enter the actual value
    SW_AGENT_COLLECTOR_BACKEND_SERVICES: ## Enter the actual value
  kind: ConfigMap
  metadata:
    name: qcbm-env
    namespace: qcbm
```
:::
</dx-tabs>

#### Creating a Secret

You can create a Secret named “qcbm-keys” with reference to [QCBM Project](https://github.com/TencentCloud/container-demo/tree/main/dubbo-on-tke), and distribute it to the specified cluster according to the distribution policy.
>! The creation process is the same as that of creating a Secret in a single cluster. You should specify a distribution policy such as “qcbm-subscription” on the configuration page.
>

<dx-tabs>
::: Method 1: Via the console
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Configuration management** > **Secret** > **Create**, create a Secret named “qcbm-keys” and select qcbm-subscription as the distribution policy.
3. Click **Create Secret**. You can see that the Secret is configured and distributed to the specified cluster.
:::
::: Method 2: Using YAML
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Create via YAML**, and enter the following YAML configuration.
3. Click **Complete** to complete the creation. Select the distribution policy “qcbm-subscription”.
```yaml
  apiVersion: v1
  kind: Secret
  metadata:
    name: qcbm-keys
    namespace: qcbm
    labels:
      qcloud-app: qcbm-keys
  data:
    # echo -n xxx | base64. Note: Run the command to generate the following parameters in Base64 format.
    MYSQL_ACCOUNT: ## Enter the actual value
    MYSQL_PASSWORD: ## Enter the actual value
    REDIS_PASSWORD: ## Enter the actual value
    SW_AGENT_AUTHENTICATION: ## Enter the actual value
  type: Opaque
```
:::
</dx-tabs>


#### Creating a Deployment

You can create workloads including user-service, store-service, qcbm-gateway, qcbm-front, order-service and favorites-service with the reference of [QCBM Project](https://github.com/TencentCloud/container-demo/tree/main/dubbo-on-tke), and distribute them to the specified cluster according to the distribution policy.
>! The creation process is the same as that of creating a Deployment in a single cluster. You should specify a distribution policy such as “qcbm-subscription” on the configuration page.
>

<dx-tabs>
::: Method 1: Via the console
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Workload** > **Deployment** > **Create** to create workloads named “user-service”, ”store-service”, “qcbm-gateway”, “qcbm-front”, “order-service” and “favorites-service”. Select qcbm-subscription as the distribution policy.
![](https://qcloudimg.tencent-cloud.cn/raw/78b4c98e8e4c97d6ed0f685612c63bc7.png)
3. Click **Create workload**. You can see that the workload is configured and distributed to the specified cluster.
:::
::: Method 2: Using YAML
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Create via YAML**, and enter the following YAML configuration.
3. Click **Complete** to complete the creation. Select the distribution policy “qcbm-subscription”.
```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: user-service
    namespace: qcbm
    labels:
      app: user-service
      version: v1
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: user-service
        version: v1
    template:
      metadata:
        labels:
          app: user-service
          version: v1
      spec:
        containers:
          - name: user-service
            image: ccr.ccs.tencentyun.com/qcbm/user-service:fdd3edd
            imagePullPolicy: Always
            env:
              - name: NACOS_HOST  # The IP address of Dubbo service registry nacos
                valueFrom:
                  configMapKeyRef:
                    key: NACOS_HOST
                    name: qcbm-env
                    optional: false
              - name: MYSQL_HOST  # MySQL address
                valueFrom:
                  configMapKeyRef:
                    key: MYSQL_HOST
                    name: qcbm-env
                    optional: false
              - name: MYSQL_PORT
                valueFrom:
                  configMapKeyRef:
                    key: MYSQL_PORT
                    name: qcbm-env
                    optional: false
              - name: REDIS_HOST  # The IP address of Redis
                valueFrom:
                  configMapKeyRef:
                    key: REDIS_HOST
                    name: qcbm-env
                    optional: false
              - name: REDIS_PORT
                valueFrom:
                  configMapKeyRef:
                    key: REDIS_PORT
                    name: qcbm-env
                    optional: false
              - name: MYSQL_ACCOUNT
                valueFrom:
                  secretKeyRef:
                    key: MYSQL_ACCOUNT
                    name: qcbm-keys
                    optional: false
              - name: MYSQL_PASSWORD
                valueFrom:
                  secretKeyRef:
                    key: MYSQL_PASSWORD
                    name: qcbm-keys
                    optional: false
              - name: REDIS_PASSWORD
                valueFrom:
                  secretKeyRef:
                    key: REDIS_PASSWORD
                    name: qcbm-keys
                    optional: false
              - name: SW_AGENT_COLLECTOR_BACKEND_SERVICES
                valueFrom:
                  configMapKeyRef:
                    key: SW_AGENT_COLLECTOR_BACKEND_SERVICES
                    name: qcbm-env
                    optional: false
              - name: SW_AGENT_AUTHENTICATION
                valueFrom:
                  secretKeyRef:
                    key: SW_AGENT_AUTHENTICATION
                    name: qcbm-keys
                    optional: false
            ports:
              - containerPort: 20880 # dubbo port name
                protocol: TCP
            volumeMounts:
              - name: dumpath
                mountPath: /app/dumps
              - name: logpath
                mountPath: /app/logs
        volumes:
          - name: dumpath
            hostPath:
              path: /data/dumps/user-service
              type: DirectoryOrCreate
          - name: logpath
            hostPath:
              path: /data/logs/user-service
              type: DirectoryOrCreate
```
:::
</dx-tabs>


#### Creating a Service

You can create services named “qcbm-front” and “api-gateway” with reference to [QCBM Project](https://github.com/TencentCloud/container-demo/tree/main/dubbo-on-tke), and distribute them to the specified clusters according to the distribution policy.
>! The creation process is the same as that of creating a Service in a single cluster. You should specify a distribution policy such as “qcbm-subscription” on the configuration page.
>

<dx-tabs>
::: Method 1: Via the console
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Service and route** > **Service** > **Create** to create services named “qcbm-front” and “api-gateway”. Select qcbm-subscription as the distribution policy.
3. Click **Create service**. You can see that the services are configured and distributed to the specified cluster.
:::
::: Method 2: Using YAML
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Create via YAML**, and enter the following YAML configuration.
3. Click **Complete** to complete the creation. Select the distribution policy “qcbm-subscription”.
```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: qcbm-front
    namespace: qcbm
  spec:
    type: NodePort
    selector:
      app: qcbm-front
      version: v1
    ports:
      - name: http
        port: 80
        targetPort: 80
        nodePort: 30080
  ---
  apiVersion: v1
  kind: Service
  metadata:
    name: api-gateway
    labels:
      app: api-gateway
    namespace: qcbm
    annotations:
      service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: ## Enter the actual value
  spec:
    externalTrafficPolicy: Cluster
    ports:
      - name: http
        port: 8080
        targetPort: 8080
        protocol: TCP
        nodePort: 32500
    selector: # Map qcbm-gateway and the Service
      app: qcbm-gateway
      version: v1
    type: LoadBalancer
```
:::
</dx-tabs>



#### Creating an Ingress

You can create an Ingress named “qcbm-ingress” with reference to [QCBM Project](https://github.com/TencentCloud/container-demo/tree/main/dubbo-on-tke), and distribute it to the specified cluster according to the distribution policy.
>! The creation process is the same as that of creating an Ingress in a single cluster. You should specify a distribution policy such as “qcbm-subscription” on the configuration page.
>

<dx-tabs>
::: Method 1: Via the console
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Service and route** > **Ingress** > **Create** to create an Ingress named “qcbm-ingress”. Select qcbm-subscription as the distribution policy.
3. Click **Create Ingress**. You can see that the Ingress is configured and distributed to the specified cluster.
:::
::: Method 2: Using YAML
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Create via YAML**, and enter the following YAML configuration.
3. Click **Complete** to complete the creation. Select the distribution policy “qcbm-subscription”.
```yaml
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: qcbm-ingress
    namespace: qcbm
    annotations:
      ingress.cloud.tencent.com/direct-access: "false"
      kubernetes.io/ingress.class: qcloud
      kubernetes.io/ingress.extensiveParameters: '{"AddressIPVersion":"IPV4"}'
      kubernetes.io/ingress.http-rules: '[{"host":"qcbm.com","path":"/","backend":{"serviceName":"qcbm-front","servicePort":"80"}}]'
  spec:
    rules:
      - host: qcbm.com
        http:
          paths:
            - path: /
              backend:
                serviceName: qcbm-front
                servicePort: 80
```
:::
</dx-tabs>

### Viewing deployment results

At this time, you have completed the deployment of QCBM in the cluster “SPG-01”. You can view the deployment results by following the steps below:
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Service and route** > **Ingress** to enter the Ingress page, where you can see the created qcbm-ingress. Click **Instance management** to view the instance information.
![](https://qcloudimg.tencent-cloud.cn/raw/69c5a09b67b1129f1f285b2590642257.png)
3. You can access the the Q Cloud Book Mall with your VIP account via Ingress.


### Multi-cluster scheduling management

#### New cluster release

The QCBM application needs to be deployed in another cluster according to business development and disaster recovery requirements. You can do this by editing the distribution policy.

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Distribution Policy** in the left sidebar.  
2. Select the distribution policy “qcbm-subscription”. Click **Associate with cluster** and add the cluster "SPG-02".
3. Click **OK**. The QCBM application will be distributed in the two clusters automatically. Click the policy name to enter the details page, where you can view the details and topology map.
![](https://qcloudimg.tencent-cloud.cn/raw/85ce7c051928447ff6f7555bc0a0e728.png)

#### Localization configuration of instances in clusters

The QCBM application has been deployed in two clusters. You can configure a localization policy to apply localization configuration to it in different clusters.
For example, the **api-gateway** Service need to specify subnet-id for cluster "SPG-02". You can take the following steps to do this.

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.  
2. Click **Service and route** > **Service**. Click the name “api-gateway”. On the page that appears, click **Instance management**. Select the instances in cluster "SPG-02". Create a localization policy.
```yaml
  apiVersion: apps.clusternet.io/v1alpha1
  kind: Localization
  metadata:
    name: qcbm-svc-gateway-override
    namespace: ## Enter the actual value 
  spec:
    priority: 300
    feed:
      apiVersion: v1
      kind: Service
      name: api-gateway
      namespace: qcbm
    overrides: 
      - name: svc-override
        type: JSONPatch
        value: |-
          [
              {
                  "op": "replace",
                  "path": "/metadata/annotations/service.kubernetes.io~1qcloud-loadbalancer-internal-subnetid",
                  "value": ""  ## Enter the actual value
              }
          ]
```
3. Click **OK**. The configuration of the cluster "SPG-02" will be adjusted automatically according to the localization policy.
4. Go to the Ingress page of cluster "SPG-02" and locate the qcbm-ingress address, through which you can access the page of Q Cloud Book Mall under the cluster "SPG-02".



### Verifying the multi-site active-active disaster recovery capability

The QCBM application has been deployed in cluster "SPG-01" and cluster "SPG-02" based on the above steps. The Ingress address is provided to users to access Q Cloud Book Mall.

You can use an existing domain name or [apply for a new domain name](https://console.cloud.tencent.com/domain), and add Ingress address resolution to implement basic multi-site active-active disaster recovery capability. You can follow the steps below to verify the high availability of multiple clusters.

1. Configure the local hosts domain name "tke-demo.cn". The Ingress address of cluster "SPG-01" is accessed by default. The page can be accessed normally.
2. Manually drain the nodes in this cluster or stop the application to simulate environment failure. An error occurs if you access "tke-demo.cn" at this time.
3. Simulate DNS switch by modifying the hosts configurations.
```shell 
# /etc/hosts
#1.14.x.x   tke-demo.cn     # SPG-01 ingress address
129.226.x.x   tke-demo.cn   # SPG-02 ingress address
```
4. Access "tke-demo.cn" in the browser. The page can be accessed normally.

As a result, the QCBM application with multi-site active-active disaster recovery capability deployed through Tencent Kubernetes Engine Distributed Cloud Center achieves multi-cluster high-availability disaster recovery and provides protection for disaster-level events. You can deploy the QCBM application to local clusters, clusters of third-party cloud vendors and edge clusters as per the same processes to implement cross-cloud service and disaster recovery.



