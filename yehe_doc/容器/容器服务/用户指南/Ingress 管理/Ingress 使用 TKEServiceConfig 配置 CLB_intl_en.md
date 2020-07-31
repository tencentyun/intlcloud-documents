## TKEServiceConfig
TkeServiceConfig is a custom resource definition (CRD) that Tencent Kubernetes Engine (TKE) provides. It can help you flexibly configure ingresses to manage Cloud Load Balancer (CLB) configurations.

### Use cases
TkeServiceConfig can configure CLB parameters and features that cannot be defined by semantics in the YAML file of an ingress.

### Configuration instructions
`TkeServiceConfig` helps you quickly configure the CLB. You can use the **ingress.cloud.tencent.com/tke-service-config:&lt;config-name&gt;** annotation to specify a target configuration and apply it to the ingress.
>! `TkeServiceConfig` needs to be in the same namespace as the ingress.
>
`TkeServiceConfig` will not configure or modify the protocol, port, domain name, or forwarding path. You need to describe the protocol, port, domain name, and forwarding path in the configuration to specify the forwarding rule for delivering the configuration.

Each layer-7 listener can have multiple domain names, and each domain name may have multiple forwarding paths. You can declare configurations of multiple domain names and forwarding rules in one `TkeServiceConfig` object. Currently, `TkeServiceConfig` can only configure CLB health check and backend access.
- After you specify the protocol and port, the configuration can be accurately delivered to the corresponding listener.
 - `spec.loadBalancer.l7Listeners.protocol`: layer-4 protocol
 - `spec.loadBalancer.l7Listeners.port`: listening port
- You can specify the protocol, port, domain name, and access path to configure the forwarding rule, such as backend health check and load balancing mode.
 - `spec.loadBalancer.l7Listeners.protocol`: layer-4 protocol
 - `spec.loadBalancer.l7Listeners.port`: listening port
 - `spec.loadBalancer.l7Listeners.domains[].domain`: domain name
 - `spec.loadBalancer.l7Listeners.domains[].rules[].url`: forwarding path

>? If your domain name is set to the default value, which is the public or private virtual IP address, you can set the domain field to null.

## TkeServiceConfig Synchronization Behavior
- When you add a configuration annotation to an ingress, the CLB will synchronize the setting.
- When you delete a configuration annotation from an ingress, the CLB will not synchronize the setting.
- When you modify the `TkeServiceConfig` configuration, the CLB of the ingress that references the configuration will synchronize the setting based on the new `TkeServiceConfig`.
- If the listener of the ingress does not find the corresponding configuration, it will not change the configuration.
- If the listener of the ingress finds the corresponding configuration but the configuration does not have declarative properties, it will not change the configuration.

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
This sample contains the following configurations:
The service is of the NodePort type. Two TCP services are declared. One is on port 80, and the other is on port 443.

### Ingress: jetty-ingress.yaml
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.rule-mix: "true"
    kubernetes.io/ingress.http-rules: '[{"path":"/health","backend":{"serviceName":"jetty-service","servicePort":"80"}}]'
    kubernetes.io/ingress.https-rules: '[{"path":"/","backend":{"serviceName":"jetty-service","servicePort":"443","host":"sample.tencent.com"}}]'
    ingress.cloud.tencent.com/tke-service-config: jetty-ingress-config
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
This sample contains the following configurations:
- A hybrid protocol is used. The default domain name (public IP address) exposes an HTTP service, and the `sample.tencent.com` domain name exposes an HTTPS service. <!-- For more information, please see [HTTP and HTTPS Used for an Ingress]().-->
- The HTTP service forwarding path is `/health`, and the HTTPS service forwarding path is `/`.
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
            enabled: false
    - protocol: HTTPS
      port: 443
      domains:
      - domain: "sample.tencent.com"
        rules:
        - url: "/"
          session:
            enabled: true
            sessionExpireTime: 3600
          healthCheck:
            enabled: true
            intervalTime: 10
            healthNum: 2
            unHealthNum: 2
            httpCheckPath: "/checkHealth"
            httpCheckDomain: "sample.tencent.com"
            httpCheckMethod: HEAD
          scheduler: IP_HASH
```
This sample contains the following configurations:
The TkeServiceConfig name is `jetty-ingress-config`. The following configurations are declared in the layer-7 listener configurations:
1. The HTTP listener on port 80 will be configured, including the domain name configuration, which is the virtual IP address of the CLB corresponding to the default domain name.
 Health check in the `/health` path is disabled.
2. The HTTPS listener on port 443 will be configured, including the domain name configuration, which is `sample.tencent.com`. The domain name only describes the configuration of a forwarding rule with the forwarding path set to `/`. The configuration contains the following content:
 - Health check is enabled. The health check interval is 10s, the healthy threshold is 2 times, and the unhealthy threshold is 2 times. Health checks are performed using a HEAD request. The checked path is `/checkHealth`, and the checked domain name is `sample.tencent.com`.
 - Session persistence is enabled. The session persistence timeout period is 3600s.
 - The forwarding policy is set to hash based on the source IP address.

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

# Obtaining the TkeServiceConfig Configuration List
➜ kubectl get tkeserviceconfigs.cloud.tencent.com
NAME                   AGE
jetty-ingress-config   52s

# Updating and Modifying TkeServiceConfig Configuration
➜ kubectl edit tkeserviceconfigs.cloud.tencent.com jetty-ingress-config
tkeserviceconfigs.cloud.tencent.com/jetty-ingress-config edited
```
