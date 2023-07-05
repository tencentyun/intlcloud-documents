## TkeServiceConfig
`TkeServiceConfig` is a custom resource definition (CRD) provided by TKE to help you manage the various configurations of CLB with an Ingress more flexibly.

### Use cases 
The CLB parameters and features that cannot be defined by the semantics of `Ingress YAML` can be configured through `TkeServiceConfig`.

### Configuration instructions
`TkeServiceConfig` helps you quickly configure CLB. You can specify a target configuration for application to an Ingress through the Ingress annotation **`ingress.cloud.tencent.com/tke-service-config:&lt;config-name&gt;`**.

>! The `TkeServiceConfig` resource needs to be in the same namespace as the Ingress.

`TkeServiceConfig` doesn't help you configure and modify the protocol, port, domain name, and forwarding path; instead, you need to describe them in the configuration to specify the forwarding rule for delivery by the configuration.

There can be multiple domain names under each layer-7 listener and multiple forwarding paths under each domain name. Therefore, you can declare multiple combinations of domain name and forwarding rule configurations in `TkeServiceConfig`. Currently, configurations are mainly provided for CLB health check and backend access.
- The configuration can be accurately delivered to the corresponding listener by specifying the protocol and port:
 - `spec.loadBalancer.l7Listeners.protocol`: layer-7 protocol
 - `spec.loadBalancer.l7Listeners.port`: listening port
- By specifying the protocol, port, domain name, and access path, you can set configurations at the forwarding rule level, such as for backend health check and load balancing methods.
 - `spec.loadBalancer.l7Listeners.protocol`: layer-7 protocol
 - `spec.loadBalancer.l7Listeners.port`: listening port
 - `spec.loadBalancer.l7Listeners.domains[].domain`: domain name
 - `spec.loadBalancer.l7Listeners.domains[].rules[].url`: forwarding path
 - `spec.loadBalancer.l7listeners.protocol.domain.rules.url.forwardType`: specified backend protocol
    - A backend protocol is the protocol between a CLB instance and the real server. If you select HTTP as the backend protocol, you need to deploy HTTP service for the real server. If you select HTTPS as the backend protocol, you need to deploy HTTPS service for the real server. Encryption and decryption of HTTPS service will consume more resources. For more information, see [Configuring a HTTPS Listener for a CLB Instance](https://intl.cloud.tencent.com/document/product/214/32516).

>?When your domain name is configured as the default value, i.e., public or private VIP, you can configure by entering a null value in the `domain` field.


## Association between Ingress and TkeServiceConfig
1. If you set `**ingress.cloud.tencent.com/tke-service-config-auto:&lt;true&gt;**` when creating an Ingress, `&lt;IngressName>-auto-ingress-config` will be created automatically. You can also specify the `TkeServiceConfig` you created on your own directly through `**ingress.cloud.tencent.com/tke-service-config:&lt;config-name&gt;**`. The two annotations cannot be used at the same time.  
2. The name of the custom configuration you use for a Service/Ingress cannot be suffixed with `-auto-service-config` or `-auto-ingress-config`.
3. The automatically created `TkeServiceConfig` has the following sync behaviors:
  - When a layer-7 forwarding rule is added during Ingress resource update, `Ingress-Controller` will automatically add the corresponding `TkeServiceConfig` configuration segment for the rule if it doesn't exist.
  - When a layer-7 forwarding rule is deleted, the `Ingress-Controller` component will automatically delete the corresponding `TkeServiceConfig` segment.
  - When an Ingress resource is deleted, the `TkeServiceConfig` will also be deleted.
  - When you modify the default `TkeServiceConfig` of the Ingress, the `TkeServiceConfig` content will also be applied to CLB.
4. You can also create the desired CLB configuration as instructed in the following `TkeServiceConfig` configuration reference, which is imported by the Service through the `**ingress.cloud.tencent.com/tke-service-config:&lt;config-name&gt;**` annotation.
5. A manually created `TkeServiceConfig` has the following sync behaviors:
  - When you use a configuration annotation in the Ingress, CLB will immediately set sync.
  - When you delete a configuration annotation in the Ingress, CLB will remain unchanged.
  - When you modify the `TkeServiceConfig` configuration, CLB of the Ingress that imports the configuration will set sync based on the new `TkeServiceConfig`.
  - If the Ingress listener cannot find the corresponding configuration, the listener will not be modified.
  - If the Ingress listener finds the corresponding configuration, but the configuration doesn't contain declared attributes, the listener will not be modified.

## License request example

### Sample deployment: jetty-deployment.yaml
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

### Sample Service: jetty-service.yaml
```yaml
apiVersion: v1
kind: Service
metadata:
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
  type: NodePort
```
This example contains the following configuration:
Service `NodePort` type, with two TCP services declared, one on port 80 and the other on port 443.

### Sample Ingress: jetty-ingress.yaml
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.rule-mix: "true"
    kubernetes.io/ingress.http-rules: '[{"path":"/health","backend":{"serviceName":"jetty-service","servicePort":"80"}}]'
    kubernetes.io/ingress.https-rules: '[{"path":"/","backend":{"serviceName":"jetty-service","servicePort":"443","host":"sample.tencent.com"}}]'
    ingress.cloud.tencent.com/tke-service-config: jetty-ingress-config
    # Specify the existing `tke-service-config`
    # ingress.cloud.tencent.com/tke-service-config-auto: "true"
    # Automatically create a `tke-service-config`
  name: jetty-ingress
  namespace: default
spec:
  rules:
  - http:
      paths:
      - backend:
          serviceName: jetty-service
          servicePort: 80
        path: /health
  - host: "sample.tencent.com"
    http:
      paths:
      - backend:
          serviceName: jetty-service
          servicePort: 443
        path: /
  tls:
  - secretName: jetty-cert-secret
```
This example contains the following configuration:
- Two different protocols are used together. The default domain name (public IP) is used to expose an HTTP service, and the `sample.tencent.com` domain name is used to expose an HTTPS service.
- The forwarding path of the HTTP service is `/health`, and that of the HTTPS service is `/`.
- The `jetty-ingress-config` CLB configuration is used.

### Sample `TkeServiceConfig`: jetty-ingress-config.yaml
```yaml
apiVersion: cloud.tencent.com/v1alpha1
kind: TkeServiceConfig
metadata:
  name: jetty-ingress-config
  namespace: default
spec:
  loadBalancer:
    l7Listeners:
    - protocol: HTTP
      port: 80
      domains:
      - domain: ""     # When `domain` is null, the VIP is used as the domain name
        rules:
        - url: "/health"
          forwardType: HTTP # It specifies HTTP as the backend protocol
          healthCheck:
            enable: false
    - protocol: HTTPS
      port: 443
      defaultServer: "sample.tencent.com" # Default domain name
      keepaliveEnable: 1                  # Enable persistent connection for the listener
      domains:
      - domain: "sample.tencent.com"
        rules:
        - url: "/"
          forwardType: HTTPS # It specifies HTTPS as the backend protocol
          session:
            enable: true
            sessionExpireTime: 3600
          healthCheck:
            enable: true
            intervalTime: 10 # `intervalTime` must be greater than `timeout`; otherwise, an error will occur.
            timeout: 5 # `timeout` must be smaller than `intervalTime`; otherwise, an error will occur.
            healthNum: 2
            unHealthNum: 2
            httpCheckPath: "/checkHealth"
            httpCheckDomain: "sample.tencent.com" # Note: the health check must use a fixed domain name for detection. If you enter a wildcard domain name in `.spec.loadBalancer.l7Listeners.protocol.domains.domain`, be sure to use the `httpCheckDomain` field to specify the domain name that requires health check; otherwise, the wildcard domain name does not support health check.
            httpCheckMethod: HEAD
          scheduler: WRR
```
This example contains the following configuration:
The name of the `TkeServiceConfig` is `jetty-ingress-config`, and in the layer-7 listener configuration, two configuration segments are declared:
1. The HTTP listener of port 80 will be configured, including the configuration of domain name, which is the default domain name and corresponds to the VIP of CLB.
 The health check feature under the `/health` path is disabled.
2. The HTTPS listener of port 443 will be configured, including the configuration of domain name, which is `sample.tencent.com`. Under this domain name, only a forwarding rule configuration with the forwarding path of `/` is described, which contains the following:
 - The health check feature is enabled, with the health check interval set to 10s, the healthy threshold to 2 times, and the unhealthy threshold also to 2 times, health checks are performed through `HEAD` requests, the check path is `/checkHealth`, and the check domain name is `sample.tencent.com`.
 - The session persistence feature is enabled, with the timeout period set to 3,600s.
 - The forwarding policy is configured as "weighted round robin".

### kubectl configuration commands
```
➜ kubectl apply -f jetty-deployment.yaml
➜ kubectl apply -f jetty-service.yaml
➜ kubectl apply -f jetty-ingress.yaml
➜ kubectl apply -f jetty-ingress-config.yaml

➜ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
jetty-deployment-8694c44b4c-cxscn   1/1     Running   0          8m8s
jetty-deployment-8694c44b4c-mk285   1/1     Running   0          8m8s
jetty-deployment-8694c44b4c-rjrtm   1/1     Running   0          8m8s

# Get the `TkeServiceConfig` configuration list
➜ kubectl get tkeserviceconfigs.cloud.tencent.com
NAME                   AGE
jetty-ingress-config   52s

# Update and modify the `TkeServiceConfig` configuration
➜ kubectl edit tkeserviceconfigs.cloud.tencent.com jetty-ingress-config
tkeserviceconfigs.cloud.tencent.com/jetty-ingress-config edited
```
