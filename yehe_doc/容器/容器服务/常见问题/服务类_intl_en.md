## FAQs on Service Creation

### Why must a service name be unique?

The service name is a unique identifier of a service in the current cluster. Services use the service name+access port combination to access one another.

### Can I use a third-party image instead of a Tencent Cloud or Docker Hub image when creating services?

Yes. To do this, you can log in to your CVM and run the `docker login` command to log in to the third-party image repository and pull the image.

### What are the prerequisites for using public network services?

Ensure that the CVMs in the cluster have public network bandwidth. Otherwise, public network services cannot be created.

### How do I configure the memory and CPU limits?

For more information, see [Setting Limit on Service Resources](https://intl.cloud.tencent.com/document/product/457/30667).

### What does the "Privileged" option mean during service creation?

Applications in the container will have true root permissions when this option is enabled. We recommend that you enable this option when you need to perform higher-level system operations on applications in the container, for example, building an NFS server.

## FAQs on Updating the Number of Service Containers

### What are the issues to note when updating the number of containers?

Check that there are sufficient CPU and memory resources. The container cannot be created if there are insufficient resources.

### Can I set the number of containers to 0?

Yes. You can set the number of containers to 0 to release the resources and retain the service configurations.

## FAQs on Updating Service Configurations

### Is rolling update supported?

Yes. Both rolling update and quick update are supported.

## FAQs on Deleting Services

### Is the CLB created by a service automatically terminated when the service is deleted?

Yes. All containers and public CLBs for a service are terminated upon service deletion. Therefore, always back up the data in advance.

## FAQs on Service Operations

### How do I set the container system time to UTC+8 time?

Containers use UTC by default. To solve the problem of an 8-hour difference between the container system time and the time you use the container, you can create a time zone file in Dockerfile.
```
RUN echo "Asia/shanghai" > /etc/timezone;
```

### What should I do when there is a TKE exception for certain Docker Hub images, such as ubuntu, php, and busybox?

If you have not set a startup command or the default startup command is `bash`, the container will exit once the startup procedure is completed. The process with PID 1 must be a resident process in the container to keep the container running. Otherwise, the container exits when this procedure ends. For some images such as centos, you can create services by running the `/bin/bash` command with the `-c sleep 800000` parameter. Here, `-c` and `sleep 800000` must be placed in different rows when you specify the parameters in the console.

Currently, certain images cannot start when the default parameters are used. These include clearlinux, ros, mageia, amazonlinux, ubuntu, clojure, crux, gcc, photon, java, debian, oraclelinux, mono, bash, buildpack-deps, golang, sourcemage, swift, openjdk, centos, busybox, docker, alpine, ibmjava, php, and python.

