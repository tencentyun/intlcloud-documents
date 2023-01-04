This document describes how to implement network isolation between containers in common scenarios based on container network policies.

## Scenario 1. Set to allow requests only between specified Pods
#### Policy description
Set to allow requests only between Pod applications with the `app=web` label and reject requests from other Pods. This is commonly used to control the access between resources in a project.
<img src="https://qcloudimg.tencent-cloud.cn/raw/992263ad22f7b79438f1e43936791cbf.png" style="zoom:50%;" />

#### Verification steps
1. Create a Pod application with the `app=web` label and start the service.
```js.
kubectl run --generator=run-pod/v1 apiserver --image=nginx --labels app=web --expose --port 80
```
 - Check whether the Pod is created successfully.
```js.
[root@VM-0-11-centos ~]# kubectl get pods web
NAME   READY   STATUS    RESTARTS   AGE
web    1/1     Running   0          4s
```
 - Check whether the svc is created successfully.
```js.
[root@VM-0-11-centos ~]# kubectl get svc web
NAME   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
web    ClusterIP   172.18.255.217   <none>        80/TCP    16s
```
3. Verify that the web service can be accessed from any source by default.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.255.217
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
4. Create and enable the container network policy.
Set the label of the protected Pod as `app=web`, use custom inbound rules, configure the source type as the Pod, and specify the Pod with the `app=web` label as the allowed inbound source. The configuration is the same for outbound rules as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/851add08541b807aad4ed2959ff76b66.png)
>! If no namespace is specified, the policy takes effect for the current namespace (default). In this case, requests from Pods in other namespaces will be rejected, even if their label is `app=web`.

5. Verify the effect of the network policy, i.e., only the Pod with the `app=web` label can access the web service.
 - The application with the `app=web` label in the current namespace can send requests to the web service.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb --labels app=web -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.255.217
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - Applications without the `app=web` label in the current namespace cannot send requests to the web service.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb --labels app2=web2 -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.255.217
wget: can't connect to remote host (172.18.255.217): Connection refused
```
 - Applications with the `app=web` label in other namespaces can send requests to the web service.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb --labels app=web -n secondary -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.255.217
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
5. Clear the environment.
```js.
kubectl delete pod web 
kubectl delete service web 
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case1`.)
```

## Scenario 2. Set to reject inbound requests to a Pod application
#### Policy description
Set to reject inbound requests to the Pod with the `app=web` label. This doesn't affect outbound requests.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2a8fb540235596290f1e489da4f37b30.png" style="zoom:50%;" />

#### Verification steps
1. Create a Pod application with the `app=web` label and start the service.
```js.
[root@VM-0-11-centos ~]# kubectl run web --image=nginx --labels app=web --expose --port 80
service/web created
pod/web created
[root@VM-0-11-centos ~]# kubectl get pods web
NAME   READY   STATUS    RESTARTS   AGE
web    1/1     Running   0          4s
[root@VM-0-11-centos ~]# kubectl get svc web
NAME   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
web    ClusterIP   172.18.255.217   <none>        80/TCP    16s
```
2. Verify that the web service can be accessed from any sources by default.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.255.217
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
3. Create and enable the container network policy.
Set the label of the protected Pod as `app=web` and set to reject all inbound requests as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ddf4ea6f125d4c57e61bbe0c625dd80a.png)
4. Verify the effect of the network policy, i.e., the application with the `app=web` label cannot be accessed from any external sources.
```js.
kubectl run --rm -i -t --image=alpine testweb -- sh 
If you don't see a command prompt, try pressing enter.
/ # wget -qO- --timeout=2 http://web
wget: can't connect to remote host (172.18.255.217): Connection refused
```
5. Clear the environment.
```js.
kubectl delete pod web 
kubectl delete service web 
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case2`.)
```

## Scenario 3. Set to reject requests from other namespaces
#### Policy description
Set to reject requests from other namespaces to the applications with the `app=web` label and allow requests only from the current namespace as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/48fe64751ceb68e2471260b9a56b9b96.png" style="zoom:50%;" />

#### Verification steps
1. Create a Pod application with the `app=web` label and start the service.
```js.
[root@VM-0-11-centos ~]# kubectl run web --image=nginx --labels app=web --expose --port 80
service/web created
pod/web created
[root@VM-0-11-centos ~]# kubectl get pods web
NAME   READY   STATUS    RESTARTS   AGE
web    1/1     Running   0          5s
[root@VM-0-11-centos ~]# kubectl get svc web
NAME   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
web    ClusterIP   172.18.255.217   <none>        80/TCP    13s
```
2. Verify that requests can be sent from other namespaces to the application with the `app=web` label by default.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb --labels app=web -n secondary -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.255.217
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
3. Create and enable the container network policy.
Set the label of the protected Pod as `app=web`, use custom inbound rules, configure the source type as the Pod, leave the namespace empty, and specify any Pod as the allowed inbound source. The configuration is the same for outbound rules as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/049e3156692eb7bbcd78abf0c0a99617.png)
4. Verify the effect of the network policy.
 - The Pod with the `app=web` label can be accessed from the current namespace.
```js.
[root@VM-0-11-centos ~]# kubectl run testweb --namespace=default --rm -it --image=alpine  -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- --timeout=2 http://web.default
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - The Pod with the `app=web` label cannot be accessed from other namespaces.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb --labels app=web -n secondary -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- --timeout=2 http://web.default
wget: can't connect to remote host (172.18.255.217): Connection refused
```
5. Clear the environment.
```js.
kubectl delete pod web 
kubectl delete service web 
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case3`.)
```

## Scenario 4. Set to allow access only to specified Pods in the namespace
#### Policy description
Set to allow external requests only to the Pod with the `app=web` label in the namespace.
<img src="https://qcloudimg.tencent-cloud.cn/raw/82285a03b9198689a3b0d19ab4f744c7.png" style="zoom:50%;" />

#### Verification steps
1. Create a Pod application with the `app=web` label and another with the `app=web1` label and start the services.
  1. Create the application with the `app=web` label.
```js.
[root@VM-0-11-centos ~]# kubectl run web --image=nginx --namespace default --labels=app=web --expose --port 80
service/web created
pod/web created
[root@VM-0-11-centos ~]# kubectl get svc web
NAME   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
web    ClusterIP   172.18.255.217   <none>        80/TCP    5s
```
  2. Create the application with the `app=web1` label.
```js.
[root@VM-0-11-centos ~]# kubectl run  web1 --image=nginx --namespace default --labels=app=web1 --expose --port 80
service/web1 created
pod/web1 created
[root@VM-0-11-centos ~]# kubectl get svc web1
NAME   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
web1   ClusterIP   172.18.255.39   <none>        80/TCP    7s
```
2. Verify that the Pods with the `app=web` and `app=web1` labels can be accessed by default.
 1. The Pod with the `app=web` label can be accessed.
 ```js.
 [root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.255.217
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
 ```
 2. The Pod with the `app=web1` label can be accessed.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.255.39
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
3. Create and enable the container network policy.
  1. Create policy A to allow all inbound requests to the Pod with the `app=web` label, specifically, by specifying the current namespace (default) and the `app=web` label.

  ![](https://qcloudimg.tencent-cloud.cn/raw/fe4b414ed5d3b7b02aad86be3079b45c.png)
  2. Create policy B to allow requests to all Pods only from the current namespace (default) and reject requests from other namespaces.

  ![](https://qcloudimg.tencent-cloud.cn/raw/46da9fc13a1e3bec8a4f470c3101ae73.png)
4. Verify the effect of the network policy. In the `default` namespace, only the Pod with the `app=web` label can be accessed from other namespaces, and other Pods (such as that with the `app=web1` label) cannot.
 - The Pod with the `app=web` label can be accessed from other namespaces.
```js.
[root@VM-0-11-centos ~]# kubectl create namespace secondary 
[root@VM-0-11-centos ~]# kubectl run  testweb --namespace=secondary --rm -i -t --image=alpine -- sh 
/ # wget -qO- --timeout=2 http://web.default
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - The Pod with the `app=web1` label cannot be accessed from other namespaces.
```js.
[root@VM-0-11-centos ~]# kubectl create namespace secondary 
[root@VM-0-11-centos ~]# kubectl run  testweb --namespace=secondary --rm -i -t --image=alpine -- sh 
/ # wget -qO- --timeout=2 http://web1.default
wget: can't connect to remote host (172.18.255.39): Connection refused
```
5. Clear the environment.
```js.
kubectl delete pod web -n default 
kubectl delete service web -n default 
kubectl delete namespace secondary 
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case4`.)
```

## Scenario 5. Set to allow access to a Pod only from the specified namespace
#### Policy description
Set to allow access to the Pod with the `app=web` label only from the specified namespace.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9b575cc976c3951c86319ba41326675b.png" style="zoom:60%;" />

#### Verification steps
1. Create a Pod application with the `app=web` label and start the service.
```js.
[root@VM-0-11-centos ~]# kubectl run web --image=nginx --namespace default --labels=app=web --expose --port 80
service/web created
pod/web created

[root@VM-0-11-centos ~]# kubectl get svc web
NAME   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
web    ClusterIP   172.18.255.217   <none>        80/TCP    5s
```
2. Create the test namespaces `dev` and `production` and verify that the web application can be accessed from all namespaces by default.
```js.
[root@VM-0-11-centos ~]# kubectl create namespace dev 
namespace/dev created
[root@VM-0-11-centos ~]# kubectl label namespace/dev env=dev 
namespace/dev labeled
[root@VM-0-11-centos ~]# kubectl create namespace production 
namespace/production created
[root@VM-0-11-centos ~]# kubectl label namespace/production env=production 
namespace/production labeled
[root@VM-0-11-centos ~]# 
```
 - By default, the web application can be accessed from the `dev` namespace.
```js.
kubectl run  testweb --namespace=dev --rm -i -t --image=alpine -- sh 
If you don't see a command prompt, try pressing enter.
/ # wget -qO- --timeout=2 http://web.default
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - By default, the web application can be accessed from the `production` namespace.
```js.
kubectl run  testweb --namespace=production --rm -i -t --image=alpine -- sh 
If you don't see a command prompt, try pressing enter.
/ # wget -qO- --timeout=2 http://web.default
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
3. Create and enable the container network policy.
Set the label of the protected Pod as `app=web`, configure the source type as the namespace, and set to allow requests only from the namespace with the `env=production` label. The configuration is the same for outbound rules as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3c9b3d68c79d3c44a54c25dc12aad2fd.png)
4. Verify the effect of the network policy.
 - The web service cannot be accessed from the `dev` namespace.
```js.
kubectl run  testweb --namespace=dev --rm -i -t --image=alpine -- sh 
If you don't see a command prompt, try pressing enter.
/ # wget -qO- --timeout=2 http://web.default
wget: can't connect to remote host (172.18.255.217): Connection refused
```
 - The web service can be accessed from the `production` namespace.
```js.
kubectl run  testweb --namespace=production --rm -i -t --image=alpine -- sh 
If you don't see a command prompt, try pressing enter.
/ # wget -qO- --timeout=2 http://web.default
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
5. Clear the environment.
```js.
kubectl delete pod web 
kubectl delete service web 
kubectl delete namespace {prod,dev}
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case5`.)
```

## Scenario 6. Set to allow requests to a Pod only from the cluster
#### Policy description
Set to allow requests to the application with the `app=web` label only from the cluster and reject those from outside the cluster.
#### Verification steps
1. Create a Pod application with the `app=web` label and another with the `app=web1` label and start the services. `web1` simulates a service in the cluster.
```js.
[root@VM-0-11-centos ~]# kubectl run web --image=nginx  --labels=app=web --expose --port 80
service/web created
pod/web created
[root@VM-0-11-centos ~]# kubectl run web1 --image=nginx  --labels=app=web1 --expose --port 80
service/web created
pod/web created
[root@VM-0-11-centos ~]# kubectl get svc web
NAME   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
web    ClusterIP   172.18.255.217   <none>        80/TCP    5s
[root@VM-0-11-centos ~]# kubectl get svc web1
NAME   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
web1   ClusterIP   172.18.255.39   <none>        80/TCP    7s
```
2. Verify that the web service can access the service in the cluster and external IPs by default.
 - The web application can access the `web1` service in the cluster.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 172.18.255.39:80
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - The web application can access external IPs.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 220.181.38.148:80
<html>
<meta http-equiv="refresh" content="0;url=http://www.baidu.com/">
</html>
```
3. Create and enable the network policy.
Set the label of the protected Pod as `app=web` and allow requests from any namespace in the cluster. The configuration is the same for outbound rules as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/53604b05acf42e87aab1319e3554642e.png)
4. Verify the effect of the network policy.
  - The web application can access the `web1` service in the cluster.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 172.18.255.39:80
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - The web application cannot access external IPs.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 220.181.38.148:80
curl: (: not foundo connect to 220.181.38.148 port 80: Connection refused
```
5. Clear the environment.
```js.
kubectl delete pod web 
kubectl delete service web 
kubectl delete pod web1
kubectl delete service web1
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case6`.)
```

## Scenario 7. Set to allow access to a Pod only through the specified port
#### Policy description
Set to allow access to the application with the `app=web` label only from TCP port 5000 and reject requests from other ports (this doesn't affect UDP access).
![](https://qcloudimg.tencent-cloud.cn/raw/a7605d5579038b52d65b742e6b2d98aa.png)

#### Verification steps
1. Create a Pod application with the `app=web` label and open ports 5000 and 8000.
```js.
kubectl run web --image=ahmet/app-on-two-ports --labels app=web
pod/web created
[root@VM-0-11-centos ~]# kubectl get pod web -o wide
NAME   READY   STATUS    RESTARTS   AGE    IP            NODE          NOMINATED NODE   READINESS GATES
web    1/1     Running   0          117s   172.18.0.42   172.16.0.11   <none>           <none>
```
2. Verify that ports 5000 and 8000 of the web application can be accessed by default.
```js.
[root@VM-0-11-centos ~]# kubectl run  testweb --namespace=dev --rm -i -t --image=alpine -- sh 
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.0.42:5000/metrics
http.requests=2
go.goroutines=5
go.cpus=4
/ # wget -qO- http://172.18.0.42:8000
Hello from HTTP server.
```
3. Create and enable the network policy.
Set the label of the protected Pod as `app=web`, allow requests only from TCP port 5000 in any namespace in the cluster, and allow requests only from TCP port 5000 at any endpoint outside the cluster as shown below:
>! To set access only through the specified UDP port, you need to add UDP port rules.

![](https://qcloudimg.tencent-cloud.cn/raw/7f04dc509f65dc5d39b44c48345dbadc.png)
4. Verify the effect of the network policy.
 Port 5000 of the web application can be accessed, but port 8000 of the web application cannot.
```js.
[root@VM-0-11-centos ~]# kubectl run  testweb --namespace=dev --rm -i -t --image=alpine -- sh 
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://172.18.0.42:5000/metrics
http.requests=2
go.goroutines=5
go.cpus=4
/ # wget -qO- http://172.18.0.42:8000
wget: can't connect to remote host (172.18.0.42): Connection refused
```
5. Clear the environment.
```js.
kubectl delete pod web 
kubectl delete service web 
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case7`.)
```

## Scenario 8. Set to allow access to a Pod only from the specified IP
#### Policy description
Set to allow access to the Pod with the `app=web` label only from the specified IP.

#### Verification steps
1. Create a Pod application with the `app=web` label and start the service.
```js.
[root@VM-0-11-centos ~]# kubectl run web --namespace default --image=nginx --labels=app=web
pod/web created
[root@VM-0-11-centos ~]# kubectl get svc web
NAME   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
web    ClusterIP   172.18.255.217   <none>        80/TCP    6s
```
2. Bind the public network IP to the web service.
  1. On the [**Cluster**](https://console.cloud.tencent.com/tke2/cluster?rid=1) page, create the public network LB service and bind the web service. For more information, see [Basic Features](https://intl.cloud.tencent.com/document/product/457/36833).
<img src="https://qcloudimg.tencent-cloud.cn/raw/002b66a516bae4ddd27173c4cb7a1eba.png" width=700px>
  2. The public network LB is created successfully, and the access address is `106.xx.xx.61`.
![](https://qcloudimg.tencent-cloud.cn/raw/3fb10d23e073fbd2d7b5f54970e704c4.png)
3. Verify that the web application can be accessed from any IP by default.
 - Any Pod can access the web application.
```js.
[root@VM-0-11-centos ~]# kubectl run --rm -it --image=alpine testweb -- sh
If you don't see a command prompt, try pressing enter.
/ # wget -qO- http://web.default
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - The web application can be accessed from any IP.
```js.
 ~/workspace/networkpolicy_test  curl cip.cc
IP: 113.xx.xx.70
Address: Shenzhen, Guangdong Province, China
ISP: China Telecom
Data 2: Shenzhen, Guangdong Province | Tencent Cloud
Data 3: Shenzhen, Guangdong Province, China | China Telecom
URL: http://www.cip.cc/113.xx.xx.70
 ~/workspace/networkpolicy_test  curl 106.xx.xx.61
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...

[root@VM-0-11-centos ~]# curl cip.cc
IP: 175.xx.xx.176
Address: China China
Data 2: Guangzhou, Guangdong Province | Tencent Cloud
Data 3: Xiamen, Fujian Province, China | Tencent
URL: http://www.cip.cc/175.xx.xx.176
[root@VM-0-11-centos ~]# curl --connect-timeout 5 106.xx.xx.61
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
3. Create and enable the network policy.
Set the label of the protected Pod as `app=web` and allow requests only from the specified IP outside the cluster as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d7ccfb8894d19accc0cceb58700d0723.png)
4. Verify the effect of the network policy.
 - The web application can be accessed only from the specified IP.
```js.
  ~/workspace/networkpolicy_test  curl 106.xx.xx.61
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - The web application cannot be accessed from other IPs.
```js.
[root@VM-0-11-centos ~]# curl cip.cc
IP: 175.xx.xx.176
Address: China China
Data 2: Guangzhou, Guangdong Province | Tencent Cloud
Data 3: Xiamen, Fujian Province, China | Tencent
URL: http://www.cip.cc/175.xx.xx.176
[root@VM-0-11-centos ~]# curl --connect-timeout 5 106.xx.xx.61
curl: (28) Connection timed out after 5001 milliseconds
```
6. Clear the environment.
```js.
kubectl delete pod web 
kubectl delete service web 
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case8`.)
```


## Scenario 9. Set to allow a Pod to access only the specified port and IP
#### Policy description
Set to allow the Pod with the `app=web` label to access only port 80 of the Pod with the `app=db` label and the specified IP.

#### Verification steps
1. Create a Pod application with the `app=web` label and another with the `app=db` label and start the services.
```js.
[root@VM-0-11-centos ~]# kubectl run web --image=nginx  --labels=app=web --expose --port 80
service/web created
pod/web created
[root@VM-0-11-centos ~]# kubectl get svc web
NAME   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
web    ClusterIP   172.18.255.217   <none>        80/TCP    5s

[root@VM-0-11-centos ~]# kubectl run db --image=nginx --port 80 --expose --labels app=db
service/db created
pod/db created
[root@VM-0-11-centos ~]# kubectl get svc db
NAME   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
db     ClusterIP   172.18.254.45   <none>        80/TCP    6s
```
2. Verify that the web service can access any Pod application and any IP by default.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 172.18.254.45
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
# curl 220.181.38.148:80
<html>
<meta http-equiv="refresh" content="0;url=http://www.baidu.com/">
</html>

# curl 103.41.167.234:80
<!DOCTYPE html>
<html lang="zh">
...
```
3. Create and enable the network policy.
Set the label of the protected Pod as `app=web`, allow outbound requests only from the specified IP outside the cluster, and allow TCP requests only through port 80 of the Pod with the `app=db` label in any namespace as shown below:
>! This policy doesn't take effect for UDP, as it is not configured.

![](https://qcloudimg.tencent-cloud.cn/raw/824d178993dbacd476d3468073b7402c.png)
4. Verify the effect of the network policy.
 - The web service can access port 80 of the service with the `app=db` label.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 172.18.254.45:80
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```
 - The web service cannot access other ports of the service with the `app=db` label.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 172.18.254.45:81
curl:（7）Failed to connect to 172.18.254.45 port 81: Connection refused
```
 - The web service cannot access other Pod services.
```js.
[root@VM-0-11-centos ~]# kubectl get svc web1
NAME   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
web1   ClusterIP   172.18.255.39   <none>        80/TCP    55m
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 172.18.255.39:80
curl:（7）Failed to connect to 172.18.255.39 port 80: Connection refused
```
 - The web service can access the specified IP.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 220.181.38.148:80
<html>
<meta http-equiv="refresh" content="0;url=http://www.baidu.com/">
</html>
```
  - The web service cannot access other IPs.
```js.
[root@VM-0-11-centos ~]# kubectl exec -it web -- sh
# curl 103.xx.xx.234
curl:（7）Failed to connect to 103.xx.xx.234 port 80: Connection refused
```
5. Clear the environment.
```js.
kubectl delete pod web 
kubectl delete service web
kubectl delete pod db
kubectl delete service db1  
Disable the network policy in the console// (This can also be done by running `kubectl delete networkpolicy case9`.)
```
