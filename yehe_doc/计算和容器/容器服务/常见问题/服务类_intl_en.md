## FAQs on service creation

### Why must a service name be unique?

A service name is a unique identifier of a service in the current cluster. Services access each other by service name+access port.

### Can I use a third-party image instead of a Tencent Cloud or Docker Hub image when creating services?

Yes. You can log in to your CVM and execute the `docker login` command to log in to the third-party image repository and pull the image.

### What are the prerequisites for using public network services?

Ensure that the CVMs in the cluster have public bandwidth. Otherwise, public network services may fail to be created.

### How do I configure memory and CPU limits?

For more information, see [Setting the Resource Limit of Workload](https://intl.cloud.tencent.com/document/product/457/30667).

### What does the "Privileged" option mean when I am creating a service?

If this option is enabled, applications in the container can have true root permission. It is recommended that you enable this option when you need to perform higher-level system operations on applications in the container; for example, building an NFS server.

### 负载均衡可以在创建时就指定安全组吗？

可以，目前支持以下两个方案，实现服务使用负载均衡时指定安全组：
- 使用已有负载均衡。先创建负载均衡并配置安全组，再挂载给服务。详情请参见 [Service 使用已有 CLB](https://intl.cloud.tencent.com/document/product/457/36835)。
- 可在服务中通过 `TkeServiceConfig` 配置安全组，负载均衡创建时会根据配置使用对应安全组。如需使用此功能，请 [提交工单](https://console.intl.cloud.tencent.com/workorder) 进行申请。

>Please do not access Service in the cluster via the load balancer IP to avoid access failure.
Usually a layer-4 load balancer (LB) will bind multiple nodes as real servers (RS). In this case, please make sure that the client and RS are not on the same CVM, otherwise the packets will not be able to sent out due to the loopback.
When a Pod accesses an LB, Pod is the source IP. When it is transmitted to the private network, LB will not transfer the source IP to the Node IP via SNAT. Therefore the LB cannot identify the source node of the packet. The LB’s loopback avoidance policy will not take effect, and packet may be forwareded to any RS. When the packet is forwarded to the Node where the client is located, LB will be unable to receive the response, leading to access failure.





## FAQs on updating the number of service containers

### What should I pay attention to when I update the number of containers?

Confirm whether CPU and memory resources are sufficient. If the resources are insufficient, a container may fail to be created.

### Can I set the number of containers to 0?

Yes. You can set the number of containers to 0 to release the resources while retaining service configurations.


## FAQs on updating service configurations

### Is rolling update supported?

Both rolling update and quick update are supported.

### 公网负载均衡可以切换为内网负载均衡吗？

可以，目前支持公网切换至 VPC 内网、VPC 内网切换至公网及 VPC 不同子网间切换。详情请参见 [Service 生命周期管理](https://intl.cloud.tencent.com/document/product/457/36832)。
>!
> - 若为服务负责负载均衡资源的生命周期管理，则负载均衡及其公网 IP 将会被释放。
> - 公网切换内网的过程并不是瞬间的，公网负载均衡服务下线到内网负载均衡并提供服务，此过程需要一定的时间。建议您先在集群中配置一个内网服务资源，并进行测试。等到流量切换完成之后，再删除原有公网服务资源。



## 删除服务常见问题[](id:service)

### Is the CLB created by a service automatically terminated after I delete the service?
删除服务时，将会同时删除创建该服务时自动创建的负载均衡。若在创建服务时选用的是已有负载均衡，则该负载均衡将不会受到任何影响。

### 删除服务是否会影响业务数据？
删除服务不会删除业务容器，数据不会受到影响，该操作无需提前备份数据。



## FAQs on service running

### How do I set the container system time to UTC+8 time?

容器默认使用 UTC 时间，使用容器时经常碰到容器系统时间和北京时间差8小时的问题，解决方法是在 dockerfile 中创建时区文件。详情请参见 [ 解决容器内时区不一致问题](https://intl.cloud.tencent.com/document/product/457/35292 )。 


### What should I do when some Docker Hub images, such as ubuntu, php, and busybox, encounter exceptions in TKE?

If no startup command is set or the default startup command is `bash`, the container will exit after the startup procedure is completed. To keep the container running, ensure that the process whose PID is 1 in the container is a permanent process. Otherwise, the container exits when this process ends. For some images such as centos, you can create services by using `/bin/bash` as the run command and `-c sleep 800000` as the run parameter. `-c` and `sleep 800000` must be entered in different rows in the console.

Currently, images that cannot be started when default parameters are used include clearlinux, ros, mageia, amazonlinux, ubuntu, clojure, crux, gcc, photon, java, debian, oraclelinux, mono, bash, buildpack-deps, golang, sourcemage, swift, openjdk, centos, busybox, docker, alpine, ibmjava, php, and python.

### 容器执行 perf top -p 查看进程 CPU 情况提示 “Operation not permitted”
容器执行 `perf top -p` 查看进程 CPU 情况提示 “Operation not permitted”，如下图所示：
![](https://main.qcloudimg.com/raw/ba1cef19dd1ab83a91e082425b588744.png)
Docker 默认配置文件阻止了重要的系统调用，perf_event_open 可能会泄漏主机上的大量信息所以被禁止使用。如果您需要调用请配置特权容器或者直接修改 Pod yaml 字段 privileged 为 true，您需自行评估安全风险。

