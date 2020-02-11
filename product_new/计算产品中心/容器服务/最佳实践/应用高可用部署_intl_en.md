
High availability (HA) refers to the ability of an application system to maintain uninterrupted operation, which is usually achieved by improving the fault tolerance of the system. In general, the application fault tolerance can be improved by configuring `replicas` to create multiple replicas of the application, but this does not necessarily mean that the application will have high availability.
This document describes four best practices for deploying applications with high availability. You can choose from them based on your situation.
- [Using anti-affinity to prevent single-point failures](#PodAntiAffinity)
- [Using PodDisruptionBudget to avoid service unavailability caused by node draining](#PodDisruptionBudget)
- [Using preStopHook and readinessProbe to ensure smooth and uninterrupted service update](#update)
- [Addressing service scale-out failures caused by persistent connections](#lapse)


## Using anti-affinity to prevent single-point failures<span ID="PodAntiAffinity"></span>
Kubernetes assumes that nodes are unreliable, so the more nodes there are, the higher the probability of nodes being unavailable due to software or hardware failures will be. Therefore, we usually have to deploy multiple replicas of applications and adjust the `replicas` value based on the actual situation. If its value is 1, there must be risks of single-point failures. Even if its value is greater than 1 but all replicas are scheduled to the same node, the single-point failure risks will still be there.

To prevent single-point failures, we need to have an appropriate number of replicas, and we also need to make sure different replicas are scheduled to different nodes. We can do so with anti-affinity. See the example below:
```
affinity:
 podAntiAffinity:
   requiredDuringSchedulingIgnoredDuringExecution:
   - weight: 100
     labelSelector:
       matchExpressions:
       - key: k8s-app
         operator: In
         values:
         - kube-dns
     topologyKey: kubernetes.io/hostname
```
The relevant configurations in this example are shown below: 
 - **requiredDuringSchedulingIgnoredDuringExecution**
This sets anti-affinity as a required condition that must be met when Pods are scheduled. If no node meets the condition, Pods will not be scheduled to any node (pending).
If you do not want to set anti-affinity as a required condition, you can use `preferredDuringSchedulingIgnoredDuringExecution` to instruct the scheduler to always try to meet the anti-affinity condition. If no node meets the condition, Pods can still be scheduled to certain nodes.

- **labelSelector.matchExpressions**
This marks the keys and values of the labels in the service’s corresponding Pod.

- **topologyKey**
This example uses `kubernetes.io/hostname` to indicate that Pods are prevented from being scheduled to the same node.
If you have higher requirements, such as preventing Pods from being scheduled to nodes in the same availability zone, to achieve remote multi-site active-active, you can use `failure-domain.beta.kubernetes.io/zone`.
Generally, all the nodes in the same cluster are in one region. If there are cross-region nodes, there will be considerable latency even if direct connect is used. If Pods have to be scheduled to nodes in the same region, you can use `failure-domain.beta.kubernetes.io/region`.

## Using PodDisruptionBudget to avoid service unavailability caused by node draining<span id="PodDisruptionBudget"></span>

Node draining involves negative impact. The following describes the process of draing a node:
1. Cordon the node by setting it as unschedulable to prevent new Pods from being scheduled to it.
2. Delete Pods from the node.
3. Once detecting that the number of Pods decreases, ReplicaSet controller will create a new Pod to be scheduled to a new node.

Such a process first deletes the Pods and then creates new Pods instead of using rolling update. Therefore, if all replicas of a service are on the drained node, the service may become unavailable during the updating process. Normally, the service may become unavailable for two reasons:
- The service is exposed to single-point failure risks with all the replicas on the same node. Once the node is drained, the service may become unavailable.
 In such a case, you can refer to [using anti-affinity to prevent single-point failures](#PodAntiAffinity).
- The service is deployed on multiple nodes but these nodes are drained at the same time. All the replicas of the service are deleted simultaneously, which may cause the service to become unavailable.
  In such a case, you can configure PDB (PodDisruptionBudget) to prevent the simultaneous deletion of all replicas. See the example below:
 - Example 1: ensure that zookeeper has at least two available replicas at the time of node draining.
```
		apiVersion: policy/v1beta1
		kind: PodDisruptionBudget
		metadata:
		  name: zk-pdb
		spec:
		  minAvailable: 2
		  selector:
		    matchLabels:
		      app: zookeeper
```
 - Example 2: ensure that zookeeper has no more than one unavailable replica at the time of node draining, which means that only one replica is deleted at a time and is recreated on another node.
```
		apiVersion: policy/v1beta1
		kind: PodDisruptionBudget
		metadata:
		  name: zk-pdb
		spec:
		  maxUnavailable: 1
		  selector:
		    matchLabels:
		      app: zookeeper
```
For more details, please read Kubernetes documentation: [Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).

## Using preStopHook and readinessProbe to ensure smooth and uninterrupted service update<span id="update"></span>
If configuration is not optimized for a service, some traffic errors may occur during the service update with the default configuration. Please refer to the following steps when making deployment.

### Service Update Scenarios
Some service update scenarios include:
- Manually adjusting the number of service replicas.
- Manually deleting Pods to trigger re-scheduling.
- Draining nodes voluntarily or involuntarily where Pods are deleted from the drained nodes and then recreated on other nodes.
- Triggering rolling update, such as modifying the image tag to upgrade the program version.
- HPA (HorizontalPodAutoscaler) automatically scales out or scale in services.
- VPA (VerticalPodAutoscaler) automatically scales up or scale down services.

### Reasons for connection errors during service update
During a rolling update, the Pods corresponding to the service being updated will be created or terminated, and the endpoints of the service will also add and remove `Pod IP:Port` corresponding to the Pods. Then kube-proxy will update the forwarding rules according to the updated `Pod IP:Port` list, but such rules are not updated immediately.

The forwarding rules are not updated immediately because Kubernetes components are decoupled from each other. Each component uses the controller mode to ListAndWatch the resources it is interested in and responds with actions. Therefore, all the steps in the process, including Pod creation or termination, endpoint update, and forwarding rules update, happen in an asynchronous manner.

When forwarding rules are not immediately updated, some connection errors could occur during the service update. The following describes two possible scenarios to analyze the reasons behind the connection errors:


- <span id="CaseOne"></span>Scenario 1: Pods have been created but have not fully started yet. Endpoint controller adds the Pods to the`Pod IP:Port` list of the service. kube-proxy watches the update and updates the service forwarding rules (iptables/ipvs). If there is a request made at this point, it could be forwarded to a Pod that has not fully started yet. An connection error may occur because the Pod is not able to properly process the request yet.

- <span id="CaseTwo"></span>Scenario 2: Pods have been terminated, but since all the steps in the process are asynchronous, the forwarding rules have not been updated when the Pods have been fully terminated. In such a case, new requests can still be forwarded to the terminated Pods, leading to connection errors.

### Smooth Update
- To address problems in [scenario 1](#caseone), you can add readinessProbe to the containers in the Pods. After a container fully starts, it will listen to an HTTP port to which kubelet will send readiness probe packets. If the container can respond normally, it means the container is ready, and the container’s status will be modified to Ready. Only when all the containers in a Pod are ready will the Pod be added to the `IP:Port` list. Then, kube-proxy will update the forwarding rules. In this way, even if a request is immediately forwarded to the new Pod, it will be able to normally process the request, thereby avoiding connection errors.

- To address problems in [scenario 2](#casetwo), you can add preStop hook to the containers in the Pods so that before the Pods are fully terminated, they will sleep for some time during which the endpoint controller and kube-proxy can update the endpoints and the forwarding rules. During that time, the Pods will be in the Terminating state. Even if a request is forwarded to a terminating Pod before the forwarding rules are fully updated, the Pod can still normally process the request because it has not been terminated yet.

Below is a YAML sample:
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      component: nginx
  template:
    metadata:
      labels:
        component: nginx
    spec:
      containers:
      - name: nginx
        image: "nginx"
        ports:
        - name: http
          hostPort: 80
          containerPort: 80
          protocol: TCP
        readinessProbe:
          httpGet:
            path: /healthz
            port: 80
            httpHeaders:
            - name: X-Custom-Header
              value: Awesome
          initialDelaySeconds: 15
          timeoutSeconds: 1
        lifecycle:
          preStop:
            exec:
              command: ["/bin/bash", "-c", "sleep 30"]
```
For more information, please see Kubernetes documentation: [Container probes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes) and [Container Lifecycle Hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/).


## Addressing service scale-out failures caused by persistent connections<span id="lapse"></span>

In many scenarios, persistent connections are used in requests for higher efficiency. If the client uses persistent connections to request the server, the auto scale-out of Kubernetes will not work. The reason is that the client persistent connections will stay in the existing Pod containers and does not extend to the new Pod containers. In such a case, Kubernetes will only scale once. At the same time, the new Pods will not be able to receive requests, which may lead to service overload.

Our solution is to use non-persistent connections instead of persistent connections. It is similar to the design of nginx keepalive in which the `keepalive_requests` configuration item can set a maximum for the number of requests that one TCP connection can process. When the configuration item reaches the pre-set value (e.g., 1,000), the server will mark `“Connection:close”` on the HTTP header and notify the client that the connection will be closed after the current request is processed and that a new TCP connection needs to be established for any new requests. Therefore, requests will not fail and non-persistent connections are used instead of persistent connections. In this way, the client and the cloud Kubernetes server will constantly update the TCP connection after fully processing a batch of requests, and the new Pods created by auto scale-out will be able to receive the latest connection requests, thereby solving the problem of auto scale-out failures.

Golang does not provide a method for obtaining the number of requests processed by each connection, so we rewrote `net.Listener` and `net.Conn` by inserting a request counter that counts the requests processed by each connection and obtains the total number using `net.Conn.LocalAddr()`. After the maximum 1,000 is reached, it inserts `“Connection:close”` in the response header to notify the client of the connection closure and the need of a new connection for any new request.

The following is a code sample which uses Golang to achieve this processing logic:
```
package main

import (
    "net"
    "github.com/gin-gonic/gin"
    "net/http"
)

// Redefine net.Listener
type counterListener struct {
    net.Listener
}

// Rewrite net.Listener.Accept(), insert request counter into received connection
func (c *counterListener) Accept() (net.Conn, error) {
    conn, err := c.Listener.Accept()
    if err != nil {
        return nil, err
    }
    return &counterConn{Conn: conn}, nil
}

// Define counter and counting method Increment()
type counter int

func (c *counter) Increment() int {
    *c++
    return int(*c)
}

// Redefine net.Conn, insert counter ct
type counterConn struct {
    net.Conn
    ct counter
}

// Rewrite net.Conn.LocalAddr(), return total number of requests processed by this connection along with the local network address
func (c *counterConn) LocalAddr() net.Addr {
    return &counterAddr{c.Conn.LocalAddr(), &c.ct}
}

// Define TCP connection counter, direct to total request counter
type counterAddr struct {
    net.Addr
    *counter
}

func main() {
    r := gin.New()
    r.Use(func(c *gin.Context) {
        localAddr := c.Request.Context().Value(http.LocalAddrContextKey)
        if ct, ok := localAddr.(interface{ Increment() int }); ok {
            if ct.Increment() >= 1000 {
                c.Header("Connection", "close")
            }
        }
        c.Next()
    })
    r.GET("/", func(c *gin.Context) {
        c.String(200, "plain/text", "hello")
    })
    l, err := net.Listen("tcp", ":8080")
    if err != nil {
        panic(err)
    }
    err = http.Serve(&counterListener{l}, r)
    if err != nil {
        panic(err)
    }
}
```
