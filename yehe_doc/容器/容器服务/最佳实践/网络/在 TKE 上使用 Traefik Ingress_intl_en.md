## Operation Scenario

[Traefik](https://doc.traefik.io/traefik/) is an excellent reverse proxy tool. Compared with Nginx, Traefik offers the following advantages:

- Native support for the dynamic configuration of, for example, Kubernetes CRD resources such as Ingress and IngressRoute (Nginx requires reloading of the full configuration each time, which may affect connections in some cases).
- Native support for service discovery. After dynamic configuration, such as by using Ingress and IngressRoute, Traefik will automatically watch the backend endpoint and synchronize it to the backend list of the CLB.
- Elegant Dashboard management page.
- Native support for metrics and seamless integration with Prometheus and Kubernetes.
- More advanced features, such as multi-version canary release, traffic replication, automatic generation of free HTTPS certificates, and middleware.

This document introduces how to install Traefik in a TKE cluster and provides use cases for Ingress and IngressRoute via Traefik.


## Prerequisites

- You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637) and can [connect to the cluster](https://intl.cloud.tencent.com/document/product/457/30639) via Kubectl.
- You have installed [Helm](https://helm.sh/docs/intro/install/).




## Directions

### Installing Traefik

This document describes the installation of Traefik in a TKE cluster as an example. For the detailed installation method, see the [official documentation](https://doc.traefik.io/traefik/getting-started/install-traefik/#use-the-helm-chart).

1. Run the following command to add the Helm chart repo source of Traefik. See the sample below:
```bash
 helm repo add traefik https://helm.traefik.io/traefik
```
2. Prepare the installation configuration file `values-traefik.yaml`. See the sample below:
```
providers: 
    kubernetesIngress: 
    publishedService: 
      enabled: true # Display the external IP address of Ingress as the LB IP address of Traefik.
additionalArguments: 
 - "--providers.kubernetesingress.ingressclass=traefik" # Indicates the ingress class name. 
 - "--log.level=DEBUG" 
service: 
  annotations: 
    service.cloud.tencent.com/direct-access: "true" # For gateway applications, we recommend that you use direct connection between the LB and pods (bypassing NodePort). If you use the VPC-CNI and Global Router network modes at the same time, use this annotation to display the declaration of direct binding of the LB to pods (bypassing NodePort). If you selected the VPC-CNI network mode during cluster creation, the declaration need not be displayed (because, by default, the LB is directly connected to pods). For more information, see the official documentation at https://intl.cloud.tencent.com/document/product/457/38408.
    service.kubernetes.io/tke-existed-lbid: lb-lb57hvgl # Use this annotation to bind the LB created in advance, so that even if Traefik is rebuilt in the future, the traffic entry will remain unchanged. If you do not specify this annotation, a new LB will be automatically created by default. For more information, see the official documentation at https://intl.cloud.tencent.com/document/product/457/36835.
ports: 
  web: 
    expose: true
    exposedPort: 80 # HTTP port number that is externally exposed. To use a standard port number in the Chinese mainland, ICP filing is required.
  websecure: 
    expose: true
    exposedPort: 443 # HTTPS port number that is externally exposed. To use a standard port number in the Chinese mainland, ICP filing is required.
deployment: 
  enabled: true
  replicas: 1
  podAnnotations: 
    tke.cloud.tencent.com/networks: "tke-route-eni" # When VPC-CNI and Global Router network modes are used at the same time, display a statement to indicate the ENI to be used by pods. This should be used together with the request and limit of eni-ip below.
resources: 
  requests: 
    tke.cloud.tencent.com/eni-ip: "1"
  limits: 
    tke.cloud.tencent.com/eni-ip: "1"
```

 >? To view the full default configuration, run `helm show values traefik/traefik`.
3. Run the following command to install Traefik to your TKE cluster. See the sample below:
```bash
kubectl create ns ingress
helm upgrade --install traefik -f values-traefik.yaml traefik/traefik
```
4. Run the following command to obtain the IP address of the traffic entry (for example, EXTERNAL-IP as shown below). See the sample below:
```bash
$ kubectl get service -n ingress
NAME      TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                      AGE
traefik   LoadBalancer   172.22.252.242   49.233.239.84   80:31650/TCP,443:32288/TCP   42h
```



### Using an Ingress

Traefik allows you to use the Ingress resources of Kubernetes as a dynamic configuration. You can directly create Ingress resources in your cluster and use them to externally open your cluster. You need to add the specified Ingress class (defined during Traefik installation). See the sample below:

```
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata: 
  name: test-ingress
  annotations: 
    kubernetes.io/ingress.class: traefik # Indicates the ingress class name.
spec: 
  rules: 
  - host: traefik.demo.com
    http: 
      paths: 
      - path: /test
        backend: 
          serviceName: nginx
          servicePort: 80
```

>! At present, TKE does not display Traefik as a product, so you cannot use the TKE console to create an Ingress in a visualized manner. Instead, you need to use YAML to create the Ingress.

### Using IngressRoute

Traefik not only supports standard Kubernetes Ingress resources but also supports the unique CRD resources of Traefik, such as IngressRoute. It can support more advanced features that an Ingress does not provide. See the IngressRoute usage example below:

```
apiVersion: traefik.containo.us/v1alpha1
kind: IngressRoute
metadata: 
  name: test-ingressroute
spec: 
  entryPoints: 
    - web
  routes: 
    - match: Host(`traefik.demo.com`) && PathPrefix(`/test`)
      kind: Rule
      services: 
        - name: nginx
          port: 80
```

>? For more information on the usage of Traefik, see the [Traefik Official Documentation](https://doc.traefik.io/traefik/routing/providers/kubernetes-crd/).
