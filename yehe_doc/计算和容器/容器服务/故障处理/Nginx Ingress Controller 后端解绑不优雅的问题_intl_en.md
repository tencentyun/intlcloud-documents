
## Symptom

When you are using NGINX Ingress and reducing the number of NGINX Ingress Controller replicas, the problem of "Connection Refused" may occur. In this case, RSs are unbound from CLB instances in batches, and TCP/UDP listeners stop forwarding existing connections.




## Possible Causes

View the source code of [NGINX Ingress](https://github.com/kubernetes/ingress-nginx/blob/main/cmd/waitshutdown/main.go) and you can see that the workloads of NGINX Ingress Controller have no graceful shutdown capabilities. Therefore, a Pod directly exits after receiving the kill signal.
![](https://qcloudimg.tencent-cloud.cn/raw/5f0c9f052d67d6e25d249c0c88a633c6.png)



## Solutions

If you use TKE's [graceful service shutdown](https://intl.cloud.tencent.com/document/product/457/42070) capabilities, when a Pod needs to be deleted, it can process the received requests, and inbound traffic is turned off while outbound traffic is still on. Outbound traffic will not be turned off until all existing requests are processed and the Pod is deleted. The Pod is deleted after the graceful shutdown period ends.
![](https://qcloudimg.tencent-cloud.cn/raw/c86a0aab1d6f4d3be656b2267a6678f5.png)





## Troubleshooting
>! This is only effective in the [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837). Check whether your cluster supports direct access.

#### Step 1
Use an annotation to indicate the use of graceful shutdown in the `****-ingress-nginx-controller` Service in the `kube-system` namespace.

The following is an example of using an annotation to indicate the use of graceful shutdown. For more information on Service annotations, see [Service Annotation](https://intl.cloud.tencent.com/document/product/457/39142).


```
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
```


#### Step 2
Add a sleep period before the `wait-shutdown` of the `****-ingress-nginx-controller` Deployment in the `kube-system` namespace.
```
  lifecycle:
          preStop:
            exec:
              command:
              - sleep                        # Add a sleep period
              - 30s                          # Add a sleep period
              - /wait-shutdown      # Add a sleep period before this line
```

For more information, see [Graceful Service Shutdown](https://intl.cloud.tencent.com/document/product/457/42070). If the problem persists, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
