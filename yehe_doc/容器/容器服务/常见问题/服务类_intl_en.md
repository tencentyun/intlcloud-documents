## FAQs on Service Creation

### Why must a service name be unique?

A service name uniquely identifies a service in a cluster. Services can use service name + access port to access each other.

### Can I use a third-party image instead of a Tencent Cloud or Docker Hub image to create services?

Yes. You can log in to your CVM and run the `docker login` command to log in to the third-party image repository and pull the image.

### What are the prerequisites for using Internet services?

CVM instances in the cluster must be configured with Internet bandwidth. Otherwise, Internet services will fail to be created.

### How do I configure memory and CPU limits?

For more information, please see [Setting the Resource Limit of Workload](https://intl.cloud.tencent.com/document/product/457/30667).

### What does the "Privileged" option mean when I create a service?

If this option is enabled, applications in a container will have true root permissions. We recommend that you enable this option when you need to perform high-level system operations on the applications in the container, for example, when building an NFS server.


### Can I specify a security group when a CLB is created?

Yes. You can use either of the following solutions to specify a security group when a service uses a CLB:
- Use existing CLBs. First, create a CLB and configure a security group and then mount them to a service. For more information, see "Using Existing CLBs".
- Use `TkeServiceConfig` in a service to configure a security group. When a CLB is created, the CLB will use the corresponding security group based on the configuration. To use this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1).

> Do not access a service in a cluster using the CLB IP address to prevent an access failure.
> Usually a Layer-4 CLB will bind multiple nodes as real servers (RSs). Ensure that the client and RS are not on the same CVM. Otherwise, packets may fail to be sent out due to the loopback.
When a pod accesses a CLB, the pod IP address is the source IP address. When the packet is routed to the private network, the CLB will not convert the source IP address to a node IP address using SNAT. As a result, the CLB cannot identify the source node of the packet, the CLB's loopback avoidance policy will not take effect, and the packet may be forwarded to any RS. When the packet is forwarded to the node where the client is located, the CLB cannot receive the response, leading to an access failure.





## FAQs on Updating the Number of Service Containers

### What should I take note of when I update the number of containers?

Confirm whether the CPU and memory resources are sufficient. Otherwise, container creation will fail.

### Can I set the number of containers to 0?

Yes. When you set the number of containers to 0, the service configuration is retained and the resources will be freed up.


## FAQs on Updating Service Configuration

### Is rolling update supported?

Yes. Both rolling update and quick update are supported.

### Can I change a public CLB to a private CLB?

Yes. Currently, you can change the service access mode from Via Internet to Via VPC or from Via VPC to Via Internet or switch the VPC subnet. For more information, see "Service lifecycle management".
>
> - If the service manages the CLB lifecycle, the CLB and its public IP address will be released.
> - It takes time to switch from the Internet to a VPC. This means that it takes some time from when the public CLB goes offline to when the private CLB starts to provide service. We recommend that you first configure a private service in the cluster and test it. Then, delete the original public service after traffic is switched over to the new service.


<span id="service"></span>
## FAQs on Service Deletion

### Will the CLB created by a service be destroyed after the service is deleted?
If a CLB is automatically created when you create a service, the CLB will be deleted when the service is deleted. If you select an existing CLB when you create a service, the CLB will not be deleted.

### Will service data be affected when a service is deleted?
No. When a service is deleted, the service container will not be deleted and data will not be affected. You do not need to back up data before deleting a service.



## FAQs on Service Operation

### How do I set the container system time to Beijing time?

The default system time of containers is Universal Time Coordinated (UTC). If the container system time is different from the local time zone when a container is used, you can create a time zone file in Dockerfile to solve this problem. For more information, see [Solve the inconsistent time zone problem in the container](https://intl.cloud.tencent.com/document/product/457/35292). 


### What can I do when some Docker Hub images, such as ubuntu, php, and busybox, encounter exceptions in TKE?

If the startup command is not set or the default startup command is `bash`, the container will exit after the startup procedure is completed. To keep the container running, the process in the container with PID set to 1 must be the permanent process. Otherwise, the container exits when this process ends. For some images like CentOS, you can create services by using `/bin/bash` as the running command and `-c sleep 800000` as the running parameter. `-c` and `sleep 800000` must be entered in different rows in the console.

Currently, the images that cannot be started using default parameters include clearlinux, ros, mageia, amazonlinux, ubuntu, clojure, crux, gcc, photon, java, debian, oraclelinux, mono, bash, buildpack-deps, golang, sourcemage, Swift, openjdk, centos, busybox, docker, alpine, ibmjava, php, and python.

