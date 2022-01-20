## Overview

This document describes how to register and discover a Spring Cloud application service in the TEM console.

## Directions
### Operations in console

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the left sidebar, click **Application Management** to enter the application management page and select a deployment region for your application.
3. Click **Create** to go to the application creation page and enter the application information for deployment. For more information, see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
4. For a Spring Cloud application, if a registry is associated with the selected **release environment**, you can select **Auto Inject Registry Info**.

### Specific configuration

If you selected **Auto Inject Registry Info**, when you submit the service for deployment, TEM will automatically save the default parameters of the registry as a `.properties` file to the `ConfigMap` named `tse-config` in the environment and mount it to the `/config/tse-default-spring-cloud-config.properties` directory of the application in the form of [VolumeMounts](https://kubernetes.io/docs/concepts/storage/volumes/#configmap).

At the same time, TEM will add the directory to the [SPRING_CONFIG_ADDITIONAL-LOCATION](https://docs.spring.io/spring-boot/docs/2.1.8.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-application-property-files) environment variable of the application. If the variable does not exist in the application, it will be created.

The basic configuration is as follows:
<dx-codeblock>
:::  bash
apiVersion: v1
kind: Deployment
metadata:
  name: my-service
spec:
  containers:
    - name: my-service
      image: my-image
      env:
        - name: SPRING_CONFIG_ADDITIONAL-LOCATION
          value: file:/config/tse-default-spring-cloud-config.properties
      volumeMounts:
        - name: tse-config
          mountPath: /config/tse-default-spring-cloud-config.properties
          subPath: tse-default-spring-cloud-config.properties
  volumes:
    - name: tse-config
      configMap:  
        name: tse-config
        items:
          - key: tse-default-spring-cloud-config.properties
            path: tse-default-spring-cloud-config.properties
:::
</dx-codeblock>


TEM will inject different parameters for different registries:
<dx-tabs>
::: ZooKeeper
Suppose the requested ZooKeeper address is `10.0.1.30:2181`:
<dx-codeblock>
:::  bash
apiVersion: v1
data:
  tse-default-spring-cloud-config.properties: |
    spring.cloud.zookeeper.connectString=10.0.1.30:2181
    spring.cloud.zookeeper.discovery.preferIpAddress=true
kind: ConfigMap
metadata:
  name: tse-config
:::
</dx-codeblock>
:::

::: Eureka
Suppose the requested Eureka address is `10.0.1.31:8083`:
<dx-codeblock>
:::  bash
apiVersion: v1
data:
  tse-default-spring-cloud-config.properties: |
    eureka.client.serviceUrl.defaultZone=http://10.0.1.37:8761/eureka/
    eureka.instance.prefer-ip-address=true
kind: ConfigMap
metadata:
  name: tse-config
:::
</dx-codeblock>
:::

:::
</dx-tabs>



## Notes and Precautions

### Notes on preferIpAddress

`xxx.preferIpAddress=true` is added to all injected registry parameters, as when Spring Cloud gets the local server IP (i.e., Pod IP in TEM), it will automatically query the domain name based on the IP; if `preferIpAddress` is determined to be `false` (default value), the service will be registered through the domain name; otherwise, it will be registered through the IP.

If a `PodName` is mapped by the Pod IP in TEM, that is, if `preferIpAddress=true` is not set, then the address registered with the registry will be a `PodName`, which will be the service instance address pulled by other services from the registry, making the instance inaccessible through the `PodName`.

### Notes on Spring Boot additional location

The [SPRING_CONFIG_ADDITIONAL-LOCATION](https://docs.spring.io/spring-boot/docs/2.1.8.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-application-property-files) environment variable automatically added by TEM enables you to externally customize the configuration of a Spring Boot application, but it takes effect only in Spring Boot v2.0 or later.

If you use Spring Boot v1.x, please add the mounted directory `/config/tse-default-spring-cloud-config.properties` to the [SPRING_CONFIG_LOCATION](https://docs.spring.io/spring-boot/docs/1.5.22.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-application-property-files) environment variable on your own.

You can also set this by directly adding the JVM launch parameters as follows:
<dx-tabs>
::: ZooKeeper
```bash
# Suppose the requested ZooKeeper address is `10.0.1.30:2181`
-Dspring.cloud.zookeeper.connectString=10.0.1.30:2181 
-Dspring.cloud.zookeeper.discovery.preferIpAddress=true
```
:::
::: Eureka
```bash
# Suppose the requested Eureka address is `10.0.1.31:8083`
-Deureka.client.serviceUrl.defaultZone=http://10.0.1.31:8083/eureka/ 
-Deureka.instance.preferIpAddress=true
```
:::
</dx-tabs>

