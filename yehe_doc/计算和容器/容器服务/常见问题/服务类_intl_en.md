## FAQs About Service Creation

### Why must a service name be unique?

A service name is a unique identifier of a service in the current cluster. Services access each other through the service name and access port.

### Can I use a third-party image instead of a Tencent Cloud or Docker Hub image when creating services?

Yes. You can log in to your CVM instance and run the `docker login` command to log in to the third-party image repository and pull the image.

### What are the prerequisites for using public network services?

Make sure that the CVM instances in the cluster have public bandwidth; otherwise, public network services may fail to be created.

### How do I configure memory and CPU limits?

For more information, see [Setting the Resource Limit of Workload](https://intl.cloud.tencent.com/document/product/457/30667).

### What does the "Privileged" option mean when I am creating a service?

If this option is enabled, applications in the container will have true root permission. We recommend you enable it when you need to perform higher-level system operations on applications in the container, such as building an NFS server.


### Can I specify the security group for a CLB instance when creating it?

Yes. Currently, you can use the following two options to specify the security group for a CLB instance when a service uses it:
- Use an existing CLB instance. You can create a CLB instance, configure the security group, and then mount it to the service. For more information, see [Using Existing CLBs](https://intl.cloud.tencent.com/document/product/457/36835).
- You can configure the security group through `TkeServiceConfig` in the service. A CLB instance will use a security group according to the configuration at the time of creation. If you need to use this feature, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.

>?To avoid access failure, we recommend you not access a service in the cluster over the CLB IP.
>In general, a layer-4 CLB instance will bind multiple nodes as real servers (RS). In this case, make sure that the client and RS are not on the same CVM instance; otherwise, there will be a certain probability that the packet will fail to loop back.
When a Pod accesses a CLB instance, the Pod is the source IP. When it is transferred to the private network, the CLB instance will not translate the source IP to the Node IP via SNAT. Therefore, the CLB instance cannot identify the source node of the packet. The CLB instance's loopback avoidance policy will not take effect, and the packet may be forwarded to any RS. When the packet is forwarded to the Node where the client is located, the CLB instance will be unable to receive the response, leading to access failure.





## FAQs About Updating the Number of Service Containers

### What should I pay attention to when I update the number of containers?

Confirm whether CPU and memory resources are sufficient. If the resources are insufficient, a container may fail to be created.

### Can I set the number of containers to 0?

Yes. You can set the number of containers to 0 to release the resources while retaining service configurations.


## FAQs About Service Configuration Update

### Is rolling update supported?

Both rolling update and quick update are supported.

### Can I switch from a public network CLB instance to a private network CLB instance?

Yes. You can switch from the public network to a VPC, from a VPC to the public network, or between different subnets of a VPC. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/457/36832).
>!
> - If the service is responsible for lifecycle management of the CLB instance, the CLB instance and its public network IP will be released.
> - The process of switching from the public network to the private network is not instantaneous. It takes a certain amount of time to deactivate the public network CLB instance and activate the private network CLB instance. We recommend you configure a private network service resource in the cluster, conduct a test, and delete the original public network service resource after the traffic switch is completed.



## FAQs About Service Deletion[](id:service)

### Will the CLB instance auto-created by a service be terminated after I delete the service?
When a service is deleted, the CLB instance auto-created at the time of the service creation will be deleted simultaneously. If an existing CLB instance is selected at the time of service creation, the CLB instance will not be affected at all.

### Is business data affected by deleting a service?
The business container will not be deleted and business data will not be affected if the service is deleted. No need to back up data in this regard.



## FAQs About Service Running

### How do I set the container system time to UTC+8 time?

The container uses UTC time by default. Users often encounter the problem of eight hours difference between the container system time and UTC+8 time. You can create a time zone file in `dockerfile` to solve this problem. For more information, see [Solve the inconsistent time zone problem in the container](https://intl.cloud.tencent.com/document/product/457/35292).  


### What should I do when some Docker Hub images, such as Ubuntu, PHP, and BusyBox, encounter exceptions in TKE?

If no start command is set or the default start command is `bash`, the container will exit after start. To keep the container running, make sure that the process whose PID is `1` in the container is a resident process; otherwise, the container will exit when this process ends. For some images such as CentOS, you can create services by using `/bin/bash` as the running command and `-c sleep 800000` as the running parameter. `-c` and `sleep 800000` must be entered in different rows in the console.

Currently, images that cannot be started when default parameters are used include Clear Linux, ROS, Mageia, Amazon Linux, Ubuntu, Clojure, CRUX, GCC, Photon, Java, Debian, Oracle Linux, Mono, Bash, buildpack-deps, Go, Source Mage, Swift, OpenJDK, CentOS, BusyBox, Docker, Alpine, IBM Java, PHP, and Python.

### What should I do if an error message "Operation not permitted" appears when a container is executing `perf top -p` to check the process CPU status?
When a container is executing `perf top -p` to check the process CPU status, an error message "Operation not permitted" appears as shown below:
![](https://main.qcloudimg.com/raw/ba1cef19dd1ab83a91e082425b588744.png)
The default configuration file of Docker prevents important system calls. `perf_event_open` is disabled because it may leak a large amount of information on the host. If you need to call it, configure a privileged container or change the value of the Pod YAML field `privileged` to `true`. You need to assess the security risks yourself.

