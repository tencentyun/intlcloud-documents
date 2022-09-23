## How It Works

GlobalRouter is a global routing capability provided by TKE based on the underlying VPC instance. It implements a routing policy for mutual access between the container network and the VPC instance. This network mode has the following characteristics:

- Container routing is performed directly through the VPC instance.
- Containers and nodes are located on the same network plane.
- Container IP ranges are dynamically assigned without occupying other IP ranges in the VPC instance.

The GlobalRouter mode is suitable for general use cases and can be seamlessly used with standard Kubernetes features. The following diagram illustrates how it works:
![](https://main.qcloudimg.com/raw/02abbfdd9fe9d6ac01190d53407aae08.png)




## Use Limits

- The IP address ranges of the cluster network and container network cannot overlap.
- The IP address ranges of container networks in different clusters within the same VPC instance cannot overlap.
- If the container network and the VPC route overlap, traffic will be preferentially forwarded within the container network.
- The static pod IP addresses are not supported.


## Container IP Address Assignment Mechanism
For container network terms and quantity calculation, see [Container Network Description](https://intl.cloud.tencent.com/document/product/457/38966#annotation).

### Pod IP Address Assignment
The following diagram illustrates how it works:
![](https://main.qcloudimg.com/raw/5a39d9cd33fe60fea4a343e817f1edf9.png)

- Each node of the cluster will use the specified IP range in the container CIDR for the node to assign IP addresses to Pods.
- The Service IP range of the cluster will select the last segment of the specified IP range in the container CIDR for Service IP addresses assignment.
- After the node is released, the corresponding container IP range will be returned to the IP range pool as well.
- The scale out node will automatically select the available IP range in the CIDR range of the container in a loop and sequentially.
