## Overview

Nginx Ingress Controller implements the Kubernetes Ingress API based on Nginx. When Nginx, which is a high-performance gateway, runs in the production environment, you need to optimize its parameters to make full use of its high performance. The deployment YAML file in [Deploying Nginx Ingress on TKE](https://intl.cloud.tencent.com/document/product/457/38072) has already optimized some performance parameters for Nginx.
This document introduces the methods and principles for optimizing the global configuration and kernel parameters of Nginx Ingress to better adapt to high-concurrency business scenarios.

## Optimizing Kernel Parameters
You can use the following methods to optimize the kernel parameters of Nginx Ingress and use the initContainers method to configure the kernel parameters. For more information, see [Configuration examples](#.E9.85.8D.E7.BD.AE.E7.A4.BA.E4.BE.8B).
- [Increasing the size of the connection queue](#.E8.B0.83.E9.AB.98.E8.BF.9E.E6.8E.A5.E9.98.9F.E5.88.97.E7.9A.84.E5.A4.A7.E5.B0.8F)
- [Expanding the range of source ports](#.E6.89.A9.E5.A4.A7.E6.BA.90.E7.AB.AF.E5.8F.A3.E8.8C.83.E5.9B.B4)
- [Reusing TIME_WAIT](#time_wait-.E5.A4.8D.E7.94.A8)
- [Increasing the maximum number of file handles](#.E8.B0.83.E5.A4.A7.E6.9C.80.E5.A4.A7.E6.96.87.E4.BB.B6.E5.8F.A5.E6.9F.84.E6.95.B0)
- [Configuration examples](#.E9.85.8D.E7.BD.AE.E7.A4.BA.E4.BE.8B)


### Increasing the size of the connection queue

In a high-concurrence environment, queue overflow may occur if the connection queue is too small, failing to establish some connections. The size of the connection queue of the process listener socket is controlled by the `net.core.somaxconn` kernel parameter. By adjusting the value of this parameter, you can enlarge the Nginx Ingress connection queue.


When a process calls the listen system to listen on ports, it passes in the backlog parameter, which determines the size of the socket connection queue. The value of the backlog parameter is not greater than that of somaxconn. When the Go program standard library listens, it reads and uses the somaxconn value as the queue size by default. However, Nginx does not read somaxconn when listening on the socket, but reads `nginx.conf`. In the listening port configuration items in `nginx.conf`, you can configure the backlog parameter to specify a connection queue size for Nginx port listening. The following shows a sample configuration:
```
server {
    listen  80  backlog=1024;
    ...
```

If the value of backlog is not specified, it defaults to 511. The detailed description of the backlog parameter is as follows:
```
backlog=number
   sets the backlog parameter in the listen() call that limits the maximum length for the queue of pending connections. By default, backlog is set to -1 on FreeBSD, DragonFly BSD, and MacOS, and to 511 on other platforms.
```

By default, even if the set value of somaxconn exceeds 511, the maximum size of the connection queue for Nginx port listening is still 511. For this reason, connection queue overflow may occur in a high-concurrency environment.

Nginx Ingress performs the preceding configuration differently. Nginx Ingress Controller can automatically read and use the value of somaxconn as the backlog value and write it to the generated [nginx.conf](https://github.com/kubernetes/ingress-nginx/blob/controller-v0.34.1/internal/ingress/controller/nginx.go#L592) file. Therefore, the connection queue size of Nginx Ingress is determined by somaxconn only, and the size defaults to 4096 in TKE.
In a high-concurrency environment, we recommend that you run the following command to set the somaxconn value to 65535:
```
sysctl -w net.core.somaxconn=65535
```

### Expanding the range of source ports

In a high-concurrency environment, Nginx Ingress uses large numbers of source ports to establish connections with the upstream. The range of source ports is randomly selected from the range defined in the `net.ipv4.ip_local_port_range` kernel parameter. In a high-concurrency environment, a small port range can easily exhaust source ports, resulting in abnormal connections.
The default source port range of pods created in a TKE environment is 32768 - 60999. We recommend that you run the following command to expand the range to 1024 - 65535:
```
sysctl -w net.ipv4.ip_local_port_range="1024 65535"
```

### Reusing TIME_WAIT

If the concurrency of non-persistent connections is high, the number of connections in the TIME_WAIT state in netns will also be large, By default, connections in the TIME_WAIT state have to wait for a period of 2MSL before being released, and therefore the source ports will be occupied for a long time. When the number of connections in this state exceeds a certain number, new connections may fail to be established.

We recommend that you run the following command to enable TIME_WAIT reuse for Nginx Ingress, which reuses TIME_WAIT connections for new TCP connections:
```
sysctl -w net.ipv4.tcp_tw_reuse=1
```

### Increasing the maximum number of file handles

When Nginx is used as a reverse proxy, each request establishes a connection with the client and upstream server respectively, which occpuies two file handles. Therefore, the theoretical maximum number of connections that Nginx can process simultaneously is half the maximum number of file handles set for the system.

The maximum number of file handles of the system is controlled by the `fs.file-max` kernel parameter, which defaults to 838860 in TKE. We recommend that you run the following command to set the maximum number of file handles to 1048576:
```
sysctl -w fs.file-max=1048576
```

### Configuration examples
Add initContainers for pods of Nginx Ingress Controller and configure the kernel parameters. The following shows a sample code:

```
initContainers:
- name: setsysctl
	image: busybox
	securityContext:
		privileged: true
	command:
	- sh
	- -c
	- |
		sysctl -w net.core.somaxconn=65535
		sysctl -w net.ipv4.ip_local_port_range="1024 65535"
		sysctl -w net.ipv4.tcp_tw_reuse=1
		sysctl -w fs.file-max=1048576
```

## Optimizing the Global Configuration
In addition to optimizing the kernel parameters, you can optimize the global configuration of Nginx by using the following methods:
- [Increasing the maximum number of keepalive connection requests](#.E8.B0.83.E9.AB.98-keepalive-.E8.BF.9E.E6.8E.A5.E6.9C.80.E5.A4.A7.E8.AF.B7.E6.B1.82.E6.95.B0)
- [Increasing the maximum number of keepalive idle connections](#.E8.B0.83.E9.AB.98-keepalive-.E6.9C.80.E5.A4.A7.E7.A9.BA.E9.97.B2.E8.BF.9E.E6.8E.A5.E6.95.B0)
- [Increasing the maximum number of connections for a single worker](#.E8.B0.83.E9.AB.98.E5.8D.95.E4.B8.AA-worker-.E6.9C.80.E5.A4.A7.E8.BF.9E.E6.8E.A5.E6.95.B0)
- [Configuration examples](#.E9.85.8D.E7.BD.AE.E7.A4.BA.E4.BE.8B2)

### Increasing the maximum number of keepalive connection requests

For keepalive connections between Nginx and the client or upstream server, the keepalive_requests parameter controls the maximum number of requests that can be processed by a single keepalive connection, which defaults to 100. When the number of requests for a keepalive connection exceeds the default, the connection will be disconnected and then re-established.

For Ingress in a private network, the QPS of a single client may be high (for example, 10,000 QPS), and Nginx may frequently disconnect its keepalive connections with the client, resulting in large numbers of connections in the TIME_WAIT state. To prevent this issue in a high-concurrency environment, we recommend that you increase the maximum number of requests for keepalive connections between Nginx and clients. This maximum number is determined by the `keep-alive-requests` parameter in Nginx Ingress, and you can set it to 10000. For more information, see [keep-alive-requests](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#keep-alive-requests). 

The number of keepalive connection requests between Nginx and the upstream is determined by `upstream-keepalive-requests`. For more information on the configuration method, see [upstream-keepalive-requests](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#upstream-keepalive-requests). 

>! In non-high-concurrency environments, you do not need to configure this parameter. If you set it to a higher value, load imbalance may occur. This is because, when keepalive connections between Nginx and the upstream are retained too long, the number of connection scheduling times will decrease and the connections will be too "rigid", leading to a traffic load imbalance.

### Increasing the maximum number of idle keepalive connections

For connections between Nginx and the upstream, you can configure the keepalive parameter, which determines the maximum number of idle connections and defaults to 320. In a high-concurrency environment, large numbers of requests and connections exist. However, in an actual production environment, requests are not fully balanced, and some connections may be temporarily idle. When the number of idle connections increases and idle connections are removed, Nginx may frequently disconnect from and reconnect to the upstream, significantly increasing the number of TIME_WAIT connections.
In a high-concurrency environment, we recommend that you set keepalive to 1000. For more information, see [upstream-keepalive-connections](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#upstream-keepalive-connections).

### Increasing the maximum number of connections for a single worker

The `max-worker-connections` parameter controls the maximum number of connections that can be used by each worker process, which defaults to 16384 in TKE. In a high-concurrency environment, we recommend that you set the value of this parameter to a greater value, for example, 65536, so that Nginx can handle more connections. For more information, see [max-worker-connections](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#max-worker-connections).

### Configuration examples

The global configuration of Nginx is implemented through the configmap configuration (Nginx Ingress Controller will read and automatically load the configuration.) The following shows a sample code:
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-ingress-controller
# Nginx Ingress performance optimization: https://www.nginx.com/blog/tuning-nginx/
data:
  # The number of requests that can be processed by a persistent connection between Nginx and the client, which defaults to 100. We recommend that you increase this number in high-concurrency scenarios.
  # Reference: https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#keep-alive-requests
  keep-alive-requests: "10000"
  # The maximum number of idle persistent connections (not the maximum number of connections) between Nginx and the upstream, which defaults to 320. We recommend that you increase this number in high-concurrency scenarios to prevent the frequent establishment of connections from significantly increasing the number of TIME_WAIT connections.
  # Reference: https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#upstream-keepalive-connections
  upstream-keepalive-connections: "200"
  # The maximum number of connections that can be used by each worker process, which defaults to 16384
  # Reference: https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#max-worker-connections
  max-worker-connections: "65536"
```




## References

- [Deploying Nginx Ingress on TKE](https://intl.cloud.tencent.com/document/product/457/38072)
- [ConfigMaps](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/)
- [Tuning NGINX for Performance](https://www.nginx.com/blog/tuning-nginx/)
- [Module ngx_http_upstream_module](http://nginx.org/en/docs/http/ngx_http_upstream_module.html)
