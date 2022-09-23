
## TkeServiceConfig
TkeServiceConfig is a Custom Resource Definition (CRD) provided by TKE. TkeServiceConfig can help you configure LoadBalancer-type Services more flexibly and manage various CLB configurations in them.

### Use cases
CLB parameters and features that cannot be defined by Service YAML semantics can be configured through TkeServiceConfig.


### Configurations
TkeServiceConfig can help you quickly perform CLB configuration. Through the Service annotation **service.cloud.tencent.com/tke-service-config:&lt;config-name&gt;**, you can specify the target configuration to be applied in the Service.
>! TkeServiceConfig resources and the Service need to be in the same namespace.

TkeServiceConfig does not help you directly configure or modify protocols and ports. You need to describe protocols and ports in the configuration in order to specify the listener for forwarding the configuration. You can declare multiple sets of listener configurations in a single TkeServiceConfig. Currently, configurations are mainly provided CLB health check and backend access.
When the protocol and port are specified, the configuration will be accurately forwarded to the corresponding listener:
  * `spec.loadBalancer.l4Listeners.protocol`: Layer-4 protocol
  * `spec.loadBalancer.l4Listeners.port`: listening port

## Associated Actions Between Service and TkeServiceConfig
1. During the creation of a Loadbalancer-type Service, if you set the annotation **service.cloud.tencent.com/tke-service-config-auto: "true"**, &lt;ServiceName&gt;-auto-service-config will be automatically created. Alternatively, you can specify your own created TkeServiceConfig through **service.cloud.tencent.com/tke-service-config:&lt;config-name&gt;**. These two annotations cannot be used at the same time. 
2. The synchronization actions of an automatically created TkeServiceConfig are as follows:
  - When a Layer-4 listener is added during Service resource update, if there is no corresponding TkeServiceConfig configuration segment for the listener or forwarding rule, Service-Controller will automatically add the corresponding TkeServiceConfig configuration segment.
  - When a Layer-4 listener is deleted, Service-Controller will automatically delete the corresponding TkeServiceConfig segment.
  - When Service resources are deleted, the corresponding TkeServiceConfig will also be deleted.
  - When you modify the default TkeServiceConfig of the Service, the TkeServiceConfig content will also be applied to the CLB.
3. You can also refer to the following complete TkeServiceConfig configuration and create your own desired CLB configuration. Services will import the configuration through the annotation **service.cloud.tencent.com/tke-service-config:&lt;config-name&gt;**.
4. The synchronization actions of a manually created TkeServiceConfig are as follows:
  - When you add a configuration annotation in the Service, the CLB will immediately set synchronization.
  - When you delete a configuration annotation in the Service, the CLB will remain unchanged.
  - When you modify the TkeServiceConfig configuration, the CLB of the Service that imported the configuration will set synchronization based on the new TkeServiceConfig.
  - If the Service listener does not find the corresponding configuration, the listener will not be modified.
  - If the Service listener finds the corresponding configuration but the configuration does not contain specified attributes, the listener will not be modified.


## Complete configuration reference  
```yaml
apiVersion: cloud.tencent.com/v1alpha1
kind: TkeServiceConfig
metadata:
  name: sample # configuration name
  namespace: default # configuration namespace
spec:
  loadBalancer:
    l4Listeners: # Layer-4 rule configuration, applicable to Service listener configuration
    - protocol: TCP # Layer-4 rule for protocol ports anchoring the Service. Required. Enumerated value: TCP|UDP.
      port: 80 # Required. Value range: 1-65535.
      session: # Configuration related to session persistence. Optional.
        enable: true # Indicates whether to enable session persistence. Required. Boolean.
        sessionExpireTime: 100 # Session persistence duration. Optional. Default value: 30. Value range: 30-3600. Unit: second.
      healthCheck: # Configuration related to health check. Optional.
        enable: true # Indicates whether to enable health check. Required. Boolean.
        intervalTime: 10 # Health check probe interval. Optional. Default value: 5. Value range: 5-300. Unit: second.
        healthNum: 2 # Healthy threshold, indicating the number of consecutive healthy health check results that it takes to indicate normal forwarding. Optional. Default value: 3. Value range: 2-10. Unit: times.
        unHealthNum: 3 # Unhealthy threshold, indicating the number of consecutive unhealthy health check results that it takes to indicate a forwarding exception. Optional. Default value: 3. Value range: 2-10. Unit: times.
        timeout: 10 # Health check response timeout threshold. This should be less than the health check interval. Optional. Default value: 2. Value range: 2-60. Unit: second.
      scheduler: WRR # Request forwarding method. WRR, LEAST_CONN, and IP_HASH indicate polling by weight, least connections, and hashing by IP address, respectively. Optional. Enumerated value: WRR | LEAST_CONN.
    internetMaxBandwidthOut: 100 # Max egress bandwidth, valid only for public network LBs. Optional. Value range: 0-2048. Unit: Mbps.
```


## Samples

### Deployment sample: jetty-deployment.yaml
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
    # Specify existing tke-service-config
    # service.cloud.tencent.com/tke-service-config-auto: true 
    # Automatically create tke-service-config
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
This sample includes the following configurations:
- The Service is of the public network LoadBalancer type, with two TCP services declared: one on port 80 and the other on port 443.
- The `jetty-service-config` CLB configuration is used.

### TkeServiceConfig sample: jetty-service-config.yaml
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
        enable: true
        intervalTime: 10
        healthNum: 2
        unHealthNum: 2
        timeout: 5
      scheduler: LEAST_CONN
```
This sample includes the following configurations:
The name is `jetty-service-config`, and in the Layer-4 listener configuration, two configuration segments are declared:
 1. The TCP listener of port 80 will be configured.
 Health check is disabled.
 2. The TCP listener of port 443 will be configured.
  - Health check is enabled, with the health check interval set to 10s, the healthy threshold set to 2 times, the unhealthy threshold also set to 2 times, and the timeout threshold set to 5s.
  - The session persistence feature is enabled, with the timeout threshold set to 3600s.
  - The forwarding policy is set to least connections.

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
NAME    TYPE           CLUSTER-IP       EXTERNAL-IP       PORT(S)                      AGE
jetty   LoadBalancer   10.127.255.209   150.158.220.237   80:31338/TCP,443:32373/TCP   2m47s

# Obtain the TkeServiceConfig Configuration List
➜ kubectl get tkeserviceconfigs.cloud.tencent.com
NAME                   AGE
jetty-service-config   52s

# Update and Modify the TkeServiceConfig Configuration
➜ kubectl edit tkeserviceconfigs.cloud.tencent.com jetty-service-config
TkeServiceConfig.cloud.tencent.com/jetty-service-config edited
```

