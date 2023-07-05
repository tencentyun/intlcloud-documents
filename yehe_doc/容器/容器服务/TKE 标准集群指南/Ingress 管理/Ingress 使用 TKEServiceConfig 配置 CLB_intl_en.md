## TKEServiceConfig
TkeServiceConfig is a Custom Resource Definition (CRD) provided by TKE. TkeServiceConfig can help you manage various Ingress CLB configurations more flexibly.

### Use cases
CLB parameters and features that cannot be defined by Ingress YAML semantics can be configured through TkeServiceConfig.

### Configuration instructions
TkeServiceConfig can help you quickly configure CLBs. Through the Ingress annotation **ingress.cloud.tencent.com/tke-service-config:&lt;config-name&gt;**, you can specify the target configuration to be applied in the Ingress.
>! TkeServiceConfig resources and the Ingress need to be in the same namespace.

TkeServiceConfig does not help you configure or modify protocols, ports, domain names, or forwarding paths. You need to describe protocols, ports, domain names, and forwarding paths in the configuration to specify the forwarding rules for configuration forwarding.

There can be multiple domain names under each Layer-7 listener, and multiple forwarding paths under each domain name. Therefore, you can declare multiple sets of domain names and forwarding rule configurations in a single `TkeServiceConfig`. Currently, configurations are mainly provided for CLB health check and backend access.
- When the protocol and port are specified, the configuration will be accurately forwarded to the corresponding listener:
 - `spec.loadBalancer.l7Listeners.protocol`: Layer-4 protocol
 - `spec.loadBalancer.l7Listeners.port`: listening port
- By specifying the protocol, port, domain name, and access path, you can set configurations at the forwarding rule level, such as for backend health check and load balancing methods.
 - `spec.loadBalancer.l7Listeners.protocol`: Layer-4 protocol
 - `spec.loadBalancer.l7Listeners.port`: listening port
 - `spec.loadBalancer.l7Listeners.domains[].domain`: domain name
 - `spec.loadBalancer.l7Listeners.domains[].rules[].url`: forwarding path

>? When your domain name is set to the default value, namely the public or private VIP, you can configure domain with a blank value.


## Associated Actions Between Ingress and TkeServiceConfig
1. During the creation of an Ingress, if you set **ingress.cloud.tencent.com/tke-service-config-auto:&lt;true&gt;**, &lt;IngressName>-auto-ingress-config will be automatically created. Alternatively, you can specify the TkeServiceConfig you created through **ingress.cloud.tencent.com/tke-service-config:&lt;config-name&gt;**. These two annotations cannot be used at the same time. 
2. The name of the custom configuration that you use for Service\Ingress cannot be suffixed with `-auto-service-config` or `-auto-ingress-config`.
3. The synchronization actions of the automatically created TkeServiceConfig are as follows:
  - When a Layer-7 forwarding rule is added during Ingress resource update, if there is no corresponding TkeServiceConfig configuration segment for the rule, Ingress-Controller will automatically add the corresponding TkeServiceConfig configuration segment.
  - When a Layer-7 forwarding rule is deleted, Ingress-Controller will automatically delete the corresponding TkeServiceConfig segment.
  - When Ingress resources are deleted, the corresponding TkeServiceConfig will also be deleted.
  - When you modify the default TkeServiceConfig of the Ingress, the TkeServiceConfig content will also be applied to the CLB.
4. You can also refer to the following complete TkeServiceConfig configuration and create your own desired CLB configuration. Services will import the configuration through the annotation **ingress.cloud.tencent.com/tke-service-config:&lt;config-name&gt;**.
5. The synchronization actions of a manually created TkeServiceConfig are as follows:
  - When you use a configuration annotation in the Ingress, the CLB will immediately set synchronization.
  - When you delete a configuration annotation in the Ingress, the CLB will remain unchanged.
  - When you modify the TkeServiceConfig configuration, the CLB of the Ingress that imported the configuration will set up synchronization based on the new TkeServiceConfig.
  - If the Ingress listener does not find the corresponding configuration, the listener will not be modified.
  - If the Ingress listener finds the corresponding configuration but the configuration does not contain declared attributes, the listener will not be modified.

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
This sample includes the following configurations:
Service NodePort type, with two TCP services declared: one on port 80 and the other on port 443.

### Ingress：jetty-ingress.yaml
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.rule-mix: "true"
    kubernetes.io/ingress.http-rules: '[{"path":"/health","backend":{"serviceName":"jetty-service","servicePort":"80"}}]'
    kubernetes.io/ingress.https-rules: '[{"path":"/","backend":{"serviceName":"jetty-service","servicePort":"443","host":"sample.tencent.com"}}]'
    ingress.cloud.tencent.com/tke-service-config: jetty-ingress-config
    # Specify existing tke-service-config
    # service.cloud.tencent.com/tke-service-config-auto: true 
    # Automatically create tke-service-config
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
This sample includes the following configurations:
- Two different protocols are used. An HTTP service is opened by using the default domain name (public IP address), and an HTTPS service is opened by using the `sample.tencent.com` domain name. <!-- For more information, see [Ingress Using HTTP and HTTPS Protocols Together]().-->
- The forwarding path of the HTTP service is `/health`, and that of the HTTPS service is `/`.
- The `jetty-ingress-config` CLB configuration is used.

### TkeServiceConfig sample: jetty-ingress-config.yaml
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
      - domain: ""
        rules:
        - url: "/health"
          healthCheck:
            enable: false
    - protocol: HTTPS
      port: 443
      domains:
      - domain: "sample.tencent.com"
        rules:
        - url: "/"
          session:
            enable: true
            sessionExpireTime: 3600
          healthCheck:
            enable: true
            intervalTime: 10
            healthNum: 2
            unHealthNum: 2
            httpCheckPath: "/checkHealth"
            httpCheckDomain: "sample.tencent.com"
            httpCheckMethod: HEAD
          scheduler: WRR
```
This sample includes the following configurations:
The name of the TkeServiceConfig is `jetty-ingress-config`, and in the Layer-7 listener configuration, two configuration segments are declared:
1. The HTTP listener of port 80 will be configured. The domain name configured is the default domain name, corresponding to the VIP of the CLB.
 The health check feature under the `/health` path is disabled.
2. The HTTPS listener of port 443 will be configured. The domain name configured is `sample.tencent.com`. Under this domain name, only a forwarding rule configuration, with the forwarding path of `/`, is described. The configuration contains the following content:
 - Health checks are enabled, with the health check interval set to 10s, the healthy threshold set to 2 times, and the unhealthy threshold also set to 2 times. Health checks are performed through a HEAD request. The check path is `/checkHealth`, and the checked domain name is `sample.tencent.com`.
 - The session persistence feature is enabled, with the timeout threshold set to 3600s.
 - The forwarding policy configured is: polling by weight.

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

# Obtain the TkeServiceConfig Configuration List
➜ kubectl get tkeserviceconfigs.cloud.tencent.com
NAME                   AGE
jetty-ingress-config   52s

# Update and Modify the TkeServiceConfig Configuration
➜ kubectl edit tkeserviceconfigs.cloud.tencent.com jetty-ingress-config
tkeserviceconfigs.cloud.tencent.com/jetty-ingress-config edited
```
