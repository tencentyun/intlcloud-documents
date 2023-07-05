
## Overview 

In scenarios where a Pod is connected directly at the access layer, when the backend performs a rolling update, or the backend Pod is deleted, if you delete the Pod directly from the CLB backend, unprocessed requests that have been received by it cannot be processed.
Particularly, in persistent connection scenarios, such as meeting business, if the Pod of the workload is updated or deleted directly, the meeting will be interrupted.

## Use Cases

- When a Pod quits gracefully during a workload update, the client will not perceive the jitters and errors generated during the update (if any).
- When a Pod needs to be deleted, it can process the received requests, and inbound traffic is turned off while outbound traffic is still on. Outbound traffic will not be turned off until all existing requests are processed and the Pod is deleted.


>!This is only effective in the [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837). Check whether your cluster supports direct access.


## Directions

### Step 1. Use an annotation to indicate the use of graceful shutdown

The following is an example of using an annotation to indicate the use of graceful shutdown. For detailed Service annotations, see [Service Annotation](https://intl.cloud.tencent.com/document/product/457/39142).

<dx-codeblock>
:::  yaml
kind: Service
apiVersion: v1
metadata: 
  annotations: 
    service.cloud.tencent.com/direct-access: "true" ## Enable CLB-to-Pod direct access
    service.cloud.tencent.com/enable-grace-shutdown: "true"  # Indicate the use of graceful shutdown
  name: my-service
spec: 
  selector: 
    app: MyApp
:::
</dx-codeblock>




### Step 2. Use `preStop` and `terminationGracePeriodSeconds`




Step 2 involves using `preStop` and `terminationGracePeriodSeconds` in the workload that requires graceful shutdown.

#### Container termination process

The following describes the container termination process in a Kubernetes environment:

1. If a deleted Pod contains `DeletionTimestamp` and is in **Terminating** status, the weight of the Pod on the CLB backend is adjusted to `0`.
2. kube-proxy updates the forwarding rule and removes the Pod from the endpoint list of the Service, and new traffic will no longer be forwarded to the Pod.
3. If a `preStop` hook is configured for the Pod, it will be executed.
4. kubelet will send a SIGTERM signal to each container in the Pod to ask the container processes to stop gracefully.
5. Wait for the container processes to stop completely. If a process has not stopped completely after `terminationGracePeriodSeconds` (30s by default) elapses, a SIGKILL signal will be sent to forcibly stop it.
6. All container processes are terminated, and the Pod resources are cleared.




#### Specific steps

1. **Use `preStop`**
  To implement graceful termination, you must process the SIGTERM signal in your business code. The main logic is to stop accepting new traffic, continue to process existing traffic, and quit after all connections are closed. For more information, see [Go by Example: Signals](https://gobyexample.com/signals).
  If the SIGTERM signal is not processed in your business code, or if you cannot control the used third-party library or system to add the logic of graceful termination, you can also try configuring `preStop` for the Pod to implement such logic as shown below:
  <dx-codeblock>
  :::  yaml
  apiVersion: v1
  kind: Pod
  metadata: 
    name: lifecycle-demo
  spec: 
    containers: 
  - name: lifecycle-demo-container
    image: nginx
    lifecycle: 
      preStop: 
        exec: 
          command: 
          - /clean.sh
    ...
    :::
    </dx-codeblock>
    For more information on how to configure `preStop`, see <a href="https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#lifecycle-1">Lifecycle</a>.

 In certain extreme cases, new connections may still be forwarded within a short period of time after the Pod is deleted. This is because kubelet and kube-proxy watch that the Pod is deleted at the same time, and kubelet may have stopped the containers before kube-proxy syncs the rules. Normally, an application will no longer accept new connections after it receives `SIGTERM`, and it will only keep the existing connections for processing, which may cause some requests to fail at the moment when the Pod is deleted.

 In view of the above, you can use `preStop` to make the Pod sleep for a short while first and then start to stop the container processes after kube-proxy completes the rule sync as shown below:
<dx-codeblock>
:::  yaml
apiVersion: v1
kind: Pod
metadata: 
  name: lifecycle-demo
spec: 
  containers: 
  - name: lifecycle-demo-container
    image: nginx
    lifecycle: 
      preStop: 
        exec: 
          command: 
          - sleep
          - 5s 
    :::
    </dx-codeblock>
2. **Use `terminationGracePeriodSeconds` to adjust the termination grace period**
  If you need a long termination grace period (`preStop` and the business process termination may take more than 30s in total), you can customize `terminationGracePeriodSeconds` as shown below based on the actual situation so as to avoid being stopped by SIGKILL prematurely:
  <dx-codeblock>
  :::  yaml
  apiVersion: v1
  kind: Pod
  metadata: 
    name: grace-demo
  spec: 
    terminationGracePeriodSeconds: 60 # The termination grace period is 30s by default, and you can set a longer period.
    containers: 
  - name: lifecycle-demo-container
    image: nginx
    lifecycle: 
      preStop: 
        exec: 
          command: 
          - sleep
          - 5s
    ...
    :::
    </dx-codeblock>

## Capabilities

Graceful shutdown sets the weight on the CLB backend to `0` only when a Pod is deleted. If a running Pod becomes unhealthy, setting the weight to `0` on the backend can reduce the risk of service unavailability.
You can use the `service.cloud.tencent.com/enable-grace-shutdown-tkex: "true"` annotation to implement graceful shutdown.
The annotation will check whether an endpoint in the Endpoint object is `not-ready`, and if so, the annotation will set the weight on the CLB backend to `0`.

## References
- Troubleshooting: [No Graceful Unbinding on the Backend of NGINX Ingress Controller](https://www.tencentcloud.com/document/product/457/48771)
