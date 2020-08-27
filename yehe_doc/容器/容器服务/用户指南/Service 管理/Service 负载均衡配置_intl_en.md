
## TkeServiceConfig
TkeServiceConfig is a custom resource definition (CRD) that Tencent Kubernetes Engine (TKE) provides. It can help you flexibly configure services of the LoadBalancer type and manage Cloud Load Balancer (CLB) configurations.

### Use cases
TkeServiceConfig can configure CLB parameters and features that cannot be defined by semantics in the YAML file of a service.


### Configuration instructions
`TkeServiceConfig` helps you quickly configure the CLB. You can use the **service.cloud.tencent.com/tke-service-config:&lt;config-name&gt;** annotation to specify a target configuration and apply it to the service.
> `TkeServiceConfig` needs to be in the same namespace as the service.
>
`TkeServiceConfig` will not configure or modify the protocol or port. You need to describe the protocol and port in the configuration to specify the listener to which the configuration is delivered. In a `TkeServiceConfig` object, you can declare configurations for multiple listeners. Currently, `TkeServiceConfig` only configures CLB health checks and backend access.
After you specify the protocol and port, the configuration can be accurately delivered to the corresponding listener.
  * `spec.loadBalancer.l4Listeners.protocol`: layer-4 protocol
  * `spec.loadBalancer.l4Listeners.port`: listening port

## TkeServiceConfig Synchronization Behavior
* When you add a configuration annotation to a service, the CLB will synchronize the setting.
* When you delete a configuration annotation from a service, CLB will not synchronize the setting.
* When you modify `TkeServiceConfig` configuration, the CLB of the service that references the configuration will synchronize the setting based on the new `TkeServiceConfig`.
* If the listener of the service does not find the corresponding configuration, it will not change the configuration.
* If the listener of the service finds the corresponding configuration but the configuration does not have declarative properties, it will not change the configuration.


## Configuration Reference  
```yaml
apiVersion: cloud.tencent.com/v1alpha1
kind: TkeServiceConfig
metadata:
  name: sample # Configuration name
  namespace: default # Configuration namespace
spec:
  loadBalancer:
    l4Listeners: # Layer-4 rule configuration, which is suitable for configurations for service listeners.
    - protocol: TCP # The protocol and port determine the Layer-4 rules of the service. This is a required parameter. Enumerated values: TCP|UDP.
      port: 80 # Required. The value range is 1 to 65535.
      session: # Configuration related to session persistence, which is optional.
        enable: true # Indicates whether session persistence is enabled. This is a required parameter and takes a Boolean value.
        sessionExpireTime: 100 # Session persistence time, in seconds, which is optional. The default value is 30. The value range is 30 to 3600.
      healthCheck: # Health check related configuration, which is optional.
        enable: true # Indicates whether session persistence is enabled. This is a required parameter and takes a Boolean value.
        intervalTime: 10 # Time interval for health checks in seconds, which is optional. The default value is 5. The value range is 5 to 300.
        healthNum: 2 # Healthy threshold, which is optional. Default value: 3, indicating that if a forward is found healthy three consecutive times, it is considered to be normal. Value range: 2-10.
        unHealthNum: 3 # Unhealthy threshold, which is optional. Default value: 3, indicating that if a forward is found unhealthy three consecutive times, it is considered to be abnormal. Value range: 2-10.
        timeout: 10 # Health check response timeout time, which is optional. The timeout time must be less than the health check interval. The default value is 2. The value range is 2 to 60.
      scheduler: WRR # Request forwarding method, which is optional. WRR, LEAST_CONN, and IP_HASH indicate polling by weight, minimum number of connections, and hash by IP address respectively. Enumerated values: WRR|LEAST_CONN.
    internetMaxBandwidthOut: 100 # Maximum outbound bandwidth in Mbps, which is optional and only applies to public CLBs. The value range is 0 to 2048.
```


## Examples

### Deployment example: jetty-deployment.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: jetty
  name: jetty-deployment
  namespace: default
spec:
  progressDeadlineSeconds: 600
  replicas: 3
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: jetty
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: jetty
    spec:
      containers:
      - image: jetty:9.4.27-jre11
        imagePullPolicy: IfNotPresent
        name: jetty
        ports:
        - containerPort: 80
          protocol: TCP
        - containerPort: 443
          protocol: TCP
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
```

### Service sample: jetty-service.yaml
```yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.cloud.tencent.com/tke-service-config: jetty-service-config
  name: jetty-service
  namespace: default
spec:
  ports:
  - name: tcp-80-80
    port: 80
    protocol: TCP
    targetPort: 80
  - name: tcp-443-443
    port: 443
    protocol: TCP
    targetPort: 443
  selector:
    app: jetty
  type: LoadBalancer
```
This example contains the following configurations:
- The service is of the public LoadBalancer type. Two TCP services are declared. One is on port 80, and the other is on port 443.
- The `jetty-service-config` CLB configuration is used.

### TkeServiceConfig example: jetty-service-config.yaml
```yaml
apiVersion: cloud.tencent.com/v1alpha1
kind: TkeServiceConfig
metadata:
  name: jetty-service-config
  namespace: default
spec:
  loadBalancer:
    l4Listeners:
    - protocol: TCP
      port: 80
      healthCheck:
        enable: false
    - protocol: TCP
      port: 443
      session:
        enable: true
        sessionExpireTime: 3600
      healthCheck:
        enabled: true
        intervalTime: 10
        healthNum: 2
        unHealthNum: 2
        timeout: 5
      scheduler: LEAST_CONN
```
This example contains the following configurations:
The name is `jetty-service-config`. The following configurations are declared in the Layer-4 listener configurations:
 1. The TCP listener on port 80 will be configured.
 Health check is disabled.
 2. The TCP listener on port 443 will be configured.
  - Health check is enabled. The health check interval is 10s, the healthy threshold is 2 times, the unhealthy threshold is 2 times, and the health check response timeout time is 5s.
  - Session persistence is enabled. The session persistence timeout time is 3600s.
  - The forwarding policy is set to the minimum number of connections.

### kubectl configuration commands
```
➜ kubectl apply -f jetty-deployment.yaml
➜ kubectl apply -f jetty-service.yaml
➜ kubectl apply -f jetty-service-config.yaml

➜ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
jetty-deployment-8694c44b4c-cxscn   1/1     Running   0          8m8s
jetty-deployment-8694c44b4c-mk285   1/1     Running   0          8m8s
jetty-deployment-8694c44b4c-rjrtm   1/1     Running   0          8m8s

➜ kubectl get service jetty
NAME              TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)         AGE
jetty   LoadBalancer   10.127.255.209   150.158.220.237   80:31338/TCP,443:32373/TCP   2m47s

# Obtaining the TkeServiceConfig Configuration List
➜ kubectl get tkeserviceconfigs.cloud.tencent.com
NAME                   AGE
jetty-service-config   52s

# Updating the TkeServiceConfig Configuration
➜ kubectl edit tkeserviceconfigs.cloud.tencent.com jetty-service-config
TkeServiceConfig.cloud.tencent.com/jetty-service-config edited
```

