


After the problem of decreased availability caused during a Service's single point of failure or node draining is solved, still another scenario that may cause availability decrease needs to be considered, that is, rolling update. A normal rolling update of a Service may affect the Service availability due to the following causes:

## Lossy rolling update of the business

If there is a call between Services in the cluster:
![](https://qcloudimg.tencent-cloud.cn/raw/dba18d098d94ef7fdb140b29c851d984.png)


When a rolling update is performed on the server:

![](https://qcloudimg.tencent-cloud.cn/raw/a715e839cf50a54e36c63899bd06384f.png)

Either of the following cases may occur:
- **Case 1.** The old replica is immediately terminated, but kube-proxy on the client node hasn't updated all the forwarding rules and still schedules the new connection to the old replica. This will result in a connection exception, and the error "connection refused" (the process is being stopped and no longer receives new requests) or "no route to host" (the container is completely terminated, and its ENI and IP no longer exist) may be reported.
- **Case 2.** The new replica starts, and kube-proxy on the client node immediately watches the new replica, updates the forwarding rules, and schedules the new connection to the new replica. However, a process, such as a Java process like Tomcat, starts slowly in the container, the port is not listened on, and thus the connection cannot be processed during startup, which also results in a connection exception, and the error "connection refused" will be reported generally.

## Best practices

- For **case 1**, you can add `preStop` to the container to make the Pod sleep for a while before being truly terminated, during which kube-proxy on the client node will update all the forwarding rules, and then the container will be terminated. In this case, the Pod can still run for a while after being terminated, during which it can still process requests normally if new requests are forwarded to it as forwarding rules are not updated promptly on the client, so as to avoid connection exceptions. This method sounds ungraceful but has a good effect. There is no silver bullet in a distributed architecture, and you can only try to find and implement the best solution under the current design.

- For **case 2**, you can add `ReadinessProbe` to the container to make the Service Endpoint be updated only after all processes in the container are truly started. Then, kube-proxy on the client node will update the forwarding rules to forward the incoming traffic. This ensures that the traffic will be forwarded only after the Pod is completely ready and thus avoids connection exceptions.
Sample YAML configuration:
``` yaml
        readinessProbe:
          httpGet:
            path: /healthz
            port: 80
            httpHeaders:
            - name: X-Custom-Header
              value: Awesome
          initialDelaySeconds: 10
          timeoutSeconds: 1
        lifecycle:
          preStop:
            exec:
              command: ["/bin/bash", "-c", "sleep 10"]
```
