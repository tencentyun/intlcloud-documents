## FAQ on Service Creation

### Why must a service name be unique?

A service name is a unique service identifier under the current cluster. Services access each other by entering service names + access ports.

### Can I use a third-party image instead of Tencent Cloud or Docker Hub image when creating services?

Yes. You can log in to your CVM and execute the command `docker login` to log in to the third-party image repository and pull the image.

### What are the prerequisites for using internet services?

Ensure that CVM’s in the cluster have internet bandwidth. Otherwise the creation of internet services may fail.

### How do I configure memory and CPU limits?

For more information, see [Setting Limit on Service Resources](https://intl.cloud.tencent.com/document/product/457/9099).

### What does "Privilege" mean?

If this option is enabled, applications in the container can have true root permission. We recommend that enable this option when you need to perform higher-level system operations on the applications in the container; for example, building NFS server.

## FAQ on Updating Number of Service Containers 

### What should I take note of when I update the number of containers?

Confirm if CPU and memory resources are sufficient. Otherwise container creation will fail.

### Can I set the number of containers to 0?

Yes. You can set the number to 0. In this case, the service configuration is retained but the resources will be freed up.

## FAQ on Service Configuration Updating

### Is rolling update supported?

Both rolling update and quick update are supported.

## FAQ on Service Deletion 

### When I delete a service, will the load balancer created by the service also be terminated?

All containers and internet load balancers under a service are terminated upon service deletion. Back up the data in advance.

## FAQ on Service Operation

### How do I set the container system time to Beijing time?

Containers use UTC by default. If the problem of an 8-hour difference between the container system time and Beijing time always occurs when you use a container, create a time zone file in Dockerfile.
```
RUN echo "Asia/shanghai" > /etc/timezone;
```

### What can I do when some Docker Hub images, such as ubuntu, php and busybox, encounter exceptions in TKE?

If the startup command is not set or the default startup command is `bash`, the container will exit after the startup procedure is completed. To keep the container running, the process in the container with PID set to 1 must be the permanent process. Otherwise, the container exits when this process ends. For some images like CentOS, you can create services by using `/bin/bash` as the running command and `-c sleep 800000` as the running parameter. `-c` and `sleep 800000` must be entered in different rows in the console.

Currently, the images that cannot be started using default parameters include: clearlinux, ros, mageia, amazonlinux, ubuntu, clojure, crux, gcc, photon, java, debian, oraclelinux, mono, bash, buildpack-deps, golang, sourcemage, Swift, openjdk, centos, busybox, docker, alpine, ibmjava, php, and python.

