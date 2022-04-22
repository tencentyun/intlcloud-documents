## Overview

This document describes how to deploy Gitlab as a private code hosting platform on TKE.

## Prerequisites


- You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637), and you can [connect to the cluster](https://intl.cloud.tencent.com/document/product/457/30639) through Kubectl.



## Directions

### Installing Gitlab


Use Helm to install Gitlab and pass in the recommended [values.yaml](https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/gitlab/values-gitlab-ce.yaml) configuration (image synchronization + TKE adaption). This document describes the following two methods to deploy Helm applications on TKE:

>?
- When deploying with the console, you do not need to install the Helm command.
- When deploying with Helm commands, it is applicable to CI/CD process.





#### Deploying with the console
1. Log in to the TKE console and click **[Marketplace](https://console.cloud.tencent.com/tke2/market)** in the left sidebar.
2. Search for Gitlab on the **Marketplace** page and go to the Gitlab Application page.
3. Click **Create Application**, select the cluster to install the application in the pop-up window, and paste the configuration of [values.yaml](https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/gitlab/values-gitlab-ce.yaml) to the **Parameter**.
4. Click **Create**.

#### Deploying with Helm commands

1. You have installed [Helm](https://helm.sh/docs/intro/install/).
2. You have installed Jenkins through Helm commands. For details, see [Install Jenkins with Helm](https://www.jenkins.io/doc/book/installing/kubernetes/#install-jenkins-with-helm-v3).


>? When running the “helm install” command, you need to add `-f values-gitlab-ce.yaml` to replace the deployment configuration.


### Obtaining access entry and login method

After Gitlab is installed, a CLB will be created by default and a layer-4 listener will be used as the access entry of Gitlab. You can find the corresponding CLB and its public IP on the console through the following steps:
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2)** in the left sidebar.
2. On the **Cluster Management** page, click the desired cluster ID to go to the **Deployment** page.
3. Select **Services and Routes** > **Service** in the left sidebar, and go to the **Service** page.
 The CLB port defaults to 8181, and the username is root. The initial password can be found from the pod standard output of gitlab-migrations, or from the secret of `gitlab-initial-root-password`.



## Custom Configuration Instructions

 You can custom the parameters in the recommended [values.yaml](https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/gitlab/values-gitlab-ce.yaml) configuration based on the actual environment and needs. The details are as follows:

### Disabling dependencies

There are many selectable applications of other dependencies in the Chart package of Gitlab, which do not need to be installed in most scenarios. Different environments have different configurations. If you install all applications, it may bring more uncertainty and increase the difficulty of maintenance. It is recommended to install the required dependencies according to the actual environment. Many applications of other dependencies in the recommended configuration are disabled. The YAML sample file is as follows:


``` yaml
certmanager: 
  install: false 
nginx-ingress: 
  enabled: false 
prometheus: 
  install: false 
gitlab-runner: 
  install: false 
registry: 
  enabled: false 
  ingress: 
    enabled: false
```


### Installing Redis and PostgreSQL

In the test environment, you can install the dependent Redis and PostgreSQL at the same time. In the production environment, it is recommended that you use the corresponding Tencent Cloud services. In the recommended configuration [values.yaml](https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/gitlab/values-gitlab-ce.yaml), Redis and PostgreSQL are installed by default. Since TKE’s default StorageClass is to create a CBS, and the minimum capacity is 10Gi, Redis and PostgreSQL will apply for 10Gi capacity by default for data persistence. The YAML sample file is as follows:


``` yaml
redis: 
  install: true 
  usePassword: true 
  password: "123456" 
  cluster: 
    enabled: false 
  master: 
    persistence: 
      size: 10Gi
postgresql: 
  install: true 
  postgresqlUsername: gitlab
  postgresqlPostgresPassword: "123456"
  persistence: 
    size: 10Gi
```




### Configuring traffic entry

After Gitlab is installed, a CLB will be created by default and a layer-4 listener (port 8181) will be used as the access entry for Gitlab. The YAML file is as follows:

```yaml
gitlab: 
  webservice: 
    service: 
      type: LoadBalancer # Open via layer-4 LB
      workhorseExternalPort: 8181 # Public port of Gitlab interface
```
>? You can enter `http://<public IP>:8181` in the browser to access.

In the production environment, it is recommended to use Ingress to open traffic. If you need to use HTTPS, configure the certificate on Ingress. Nginx-ingress is recommended for TKE, which requires additional installation. For details, see [Nginx Ingress Introduction](https://intl.cloud.tencent.com/document/product/457/38980).

1. If you need to use Nginx-ingress to open Gitlab services, you only need ClusterIP, and Gitlab's own Service does not need to be LoadBalancer. The sample YAML file is as follows:
```yaml
gitlab: 
    webservice: 
    service: 
      type: ClusterIP # CLB is not automatically created for Gitlab.
```
2. Create Ingress. You can create Ingress via TKE console or YAML.
#### Creating an Ingress via console
See [Creating an Ingress](https://intl.cloud.tencent.com/document/product/457/30673) for more information on how to create an Ingress in the console.

-  **Ingress Type**: select **Nginx Load Balancer** to specify the use of Nginx Ingress.
-  **Class**: specify the IngressClass name used by the Nginx Ingress instance.
- **Listener Port**: select **Https:443**.
- **Forwarding Configuration**: enter the relevant information. You need to select the service of Gitlab webservice for **Backend Service**.
-  **TLS Configuration**: enter the relevant information. If HTTPS is used, you need to create the certificate Secret in advance.

#### Creating an Ingress via YAML
See [Creating an Ingress](https://intl.cloud.tencent.com/document/product/457/306732) for more information on how to create an Ingress via YAML. The YAML sample file is as follows:
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata: 
  annotations: 
    kubernetes.io/ingress.class: nginx
  name: gitlab
  namespace: devops
spec: 
  rules: 
  - host: gitlab.xxxx.io
    http: 
      paths: 
      - backend: 
          serviceName: gitlab-webservice-default
          servicePort: 8181 
        path: /
        pathType: ImplementationSpecific
        tls: 
  - hosts: 
    - gitlab.xxxx.io
    secretName: gitlab-crt-secret
```
3. After the Ingress is created, the traffic entry IP is the public IP of the selected Nginx Ingress instance.
4. The default HTTP port of Nginx Ingress instance is 80 and HTTPS port is 443. If Nginx Ingress is deployed in Chinese mainland, you need to obtain an ICP filing before using these two standard ports for access. During the test, if you need to use a non-standard port for access, you can modify the service of the Nginx Ingress instance by running the following command, and change 80 or 443 to another port.
```bash
kubectl -n kube-system edit svc nginx-ingress-nginx-controller # svc name with ingressClass name prefix
```
5. If you need to open the SSH protocol of Gitlab, you can modify the configuration of the Nginx Ingress instance to open port 22. Run the following command to modify the configmap that opens TCP, as shown below:
```bash
$ kubectl -n kube-system get cm | grep nginx-ingress
nginx-ingress-nginx-controller             6      8d
nginx-ingress-nginx-tcp                    0      8d
nginx-ingress-nginx-udp                    0      8d
qcloud-tke-nginx-ingress-controller        0      14d
$ kubectl -n kube-system edit cm nginx-ingress-nginx-tcp
```
6. Open port 22 of the Gitlab shell to port 22 of the nginx ingress controller. The YAML sample file is as follows:
```yaml
data: 
    22: "devops/gitlab-gitlab-shell:22"
```
7. Run the following command to modify the service of nginx ingress controller, as shown below:
```bash
$ kubectl -n kube-system get svc
nginx-ingress-nginx-controller             LoadBalancer   172.21.252.133   49.233.238.230   8888:30443/TCP,8443:32345/TCP   8d
$ kubectl -n kube-system edit svc nginx-ingress-nginx-controller
```
8. Open port 22 of the controller to CLB, as shown below:
``` yaml
  - name: git-ssh
    port: 22
    protocol: TCP
    targetPort: 22
```

 At this point, you can use the address starting with `git@` (SSH protocol) when you clone the code through the git clone command.


### Configuring a domain name

The domain name configuration of Gitlab is mainly used for information display. For example, the URL displayed in git clone code can be set through the following YAML configuration:
``` yaml
global: 
  hosts: 
    gitlab: 
      name: gitlab.example.com # The domain name displayed on the page
      https: true # Whether https is used in the displayed URL. If a certificate is configured for ingress, set true here.
```

