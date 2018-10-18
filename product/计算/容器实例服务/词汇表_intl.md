

<div class="tab_list">
<ul>
    <li><a href="#A-J">A-J</a></li>
    <li><a href="#K-O">K-O</a></li>
    <li><a href="#P-Z">P-Z</a></li>
</ul>
</div>


<span id="A-J"></span>
## A-J 
### Restart policy 
Three restart policies are available. never: the container instance will not restart automatically after it exits; on-failure: the container instance restarts when it exits with a non-zero status code; always: the container instance always restarts regardless of its exit code.
### Region 
It is a region where resources reside. Each region contains multiple availability zones.



<span id="K-O"></span>
## K-O 
### Kubernetes
Kubernetes, an open source container orchestration and scheduling engine based on Google's Borg, is one of the most important components of CNCF (Cloud Native Computing Foundation). It provides production-level application orchestration, container scheduling, service discovery, automatic scaling, and other capabilities.
For more information, see [official Kubernetes documentation](https://kubernetes.io/docs/home).
### Availability zone 
Availability zones are Tencent Cloud's physical IDCs with power facilities and networks independent of each other within the same region. They are designed to ensure that the failures within an availability zone can be isolated without spreading to and affecting other zones so that users' businesses can provide continuous online services.

<span id="P-Z"></span>
## P-Z 
### Container and image 
Container is a lightweight virtualization technology at the operating system level for isolating and controlling system resources, making global resources only usable in the container processes.

Similar to a CVM snapshot but more lightweight, a container image can be construed as a static form of a container. Image defines all files and dependencies needed to run a container, ensuring the container runs in a consistent manner.
### Container image 
It is a Docker image required to start a container, which contains all the dependencies needed by the container's main process and runtime.
### Container instance name 
It is composed of lowercase letters, numbers and "-", with a length not more than 63 characters. It begins with a lowercase letter and ends with a lowercase letter or a number.
### Container status 
There are three types of container status. Waiting: creating; Running: running; Terminated: ended and the cause of which is subject to the ExitCode.
### VPC ID
VPC is a user-defined network space isolated logically.
### VPC subnet ID
Subnets are the IP address blocks within a VPC, and all cloud resources in a VPC must be deployed in subnets.
### Instance status 
There are five types of instance status. Pending: creating; Running: running; Successed: execution succeeded and terminated; Failed: execution failed and terminated; Unknown: exceptional status.






