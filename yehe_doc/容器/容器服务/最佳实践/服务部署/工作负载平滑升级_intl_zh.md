


解决了服务单点故障和驱逐节点时导致的可用性降低问题后，我们还需要考虑一种可能导致可用性降低的场景，那就是滚动更新。为什么服务正常滚动更新也可能影响服务的可用性呢？可能存在以下原因。

## 业务有损滚动更新

假如集群内存在服务间调用：
![](https://qcloudimg.tencent-cloud.cn/raw/dba18d098d94ef7fdb140b29c851d984.png)


当 server 端发生滚动更新时：

![](https://qcloudimg.tencent-cloud.cn/raw/a715e839cf50a54e36c63899bd06384f.png)

可能发生以下两种情况：
- **情况1：**旧的副本很快销毁，而 client 所在节点 kube-proxy 还没更新完转发规则，仍然将新连接调度给旧副本，造成连接异常，可能会报 “connection refused”（进程停止过程中，不再接受新请求）或 “no route to host”（容器已经完全销毁，网卡和 IP 已不存在）。
- **情况2：**新副本启动，client 所在节点 kube-proxy 很快 watch 到了新副本，更新了转发规则，并将新连接调度给新副本，但容器内的进程启动很慢（如 Tomcat 这种 java 进程），还在启动过程中，端口还未监听，无法处理连接，也造成连接异常，通常会报 “connection refused” 的错误。

## 最佳实践

- 针对**情况1**，可以给 container 加 preStop，让 Pod 真正销毁前先 sleep 等待一段时间，等待 client 所在节点 kube-proxy 更新转发规则，然后再真正去销毁容器。这样能保证在 Pod Terminating 后还能继续正常运行一段时间，这段时间如果因为 client 侧的转发规则更新不及时导致还有新请求转发过来，Pod 还是可以正常处理请求，避免了连接异常的发生。听起来感觉有点不优雅，但实际效果还是比较好的，分布式的世界没有银弹，我们只能尽量在当前设计现状下找到并实践能够解决问题的最优解。

- 针对**情况2**，可以给 container 加 ReadinessProbe（就绪检查），让容器内进程真正启动完成后才更新 Service 的 Endpoint，然后 client 所在节点 kube-proxy 再更新转发规则，让流量进来。这样能够保证等 Pod 完全就绪了才会被转发流量，也就避免了连接异常的发生。
yaml 示例：
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
