## Kubectl Introduction  
`kubectl` is a command line interface for running commands against Kubernetes clusters. This overview covers `kubectl` syntax, common command operations, and examples. For more information on each command (including all main commands and subcommands), please see [kubectl Reference Documentation](https://kubernetes.io/docs/reference/generated/kubectl/kubectl/), or execute the `kubectl help` command to get detailed information. For more information on installation, see [Installing `kubectl`](http://intl.cloud.tencent.com/document/product/457/31086).

## Using `kubectl` to Create an NGINX Service
The examples below will help you get familiar with common `kubectl` operations:
### kubectl create
Create the resource from a file or standard output to avoid an NGINX naming conflict.
```shell
$ kubectl create -f nginx.yaml # see nginx-test.yaml file below
```
nginx-test.yaml file is shown below:
```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: nginx-test
  labels:
    qcloud-app: nginx-test
spec:
  replicas: 1
  revisionHistoryLimit: 5
  selector:
    matchLabels:
      qcloud-app: nginx-test
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        qcloud-app: nginx-test
    spec:
      containers:
      - image: nginx:latest
        imagePullPolicy: Always
        name: nginx-test
        resources:
          limits:
            cpu: 200m
            MEM: 128Mi
          requests:
            cpu: 200m
            MEM: 128Mi
        securityContext:
          privileged: false
      serviceAccountName: ""
      volumes: null
      imagePullSecrets:
      - name: qcloudregistrykey
status: {}
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-test
  labels:
    qcloud-app: nginx-test
spec:
  ports:
  - name: tcp-80-80-ogxxh
    nodePort: 0
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    qcloud-app: nginx-test
  type: LoadBalancer
status:
  loadBalancer: {}
```
![Alt text][create]
Use the following command to obtain the public IP access address:
```
kubectl get services
```
![Alt text][get]
Enter this IP address into your browser to directly access the NGINX service.
![Alt text][show]

### kubectl logs
Print a container log in the container.
```shell
// Return a snapshot of the logs from pod <pod-name>.
$ kubectl logs <pod-name>
```
![Alt text][logs]


[create]:https://mc.qcloudimg.com/static/img/a33b8f47e796374d5c457542c1569a9c/image.png
[get]:https://main.qcloudimg.com/raw/364d4b12fa90db3f6cbf663eb5406a8f.png

[show]:https://mc.qcloudimg.com/static/img/e09ab193d3f1732cc435ba53235094c1/image.png
[logs]:https://main.qcloudimg.com/raw/f9db9c5e098b2cf5359688bead0c7f7b.png
