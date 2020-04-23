## Cluster Creation FAQ

### Can I choose not to set a public IP address for the CVM when creating a cluster?

Yes. A CVM without a public IP address can only pull images from "My Images" in Image Repository but not Docker Hub images or third-party images.
A CVM without a public IP address but with Internet bandwidth can access the Internet by binding an EIP.

### Why do I need to choose a network when creating a cluster?

The selected network and subnet are where the CVM resides. You can add different CVMs to subnets in different AZs for cross-AZ disaster recovery.

### What CVM models are supported when creating a cluster?

All models that use cloud disks for their pay-as-you-go system disks are supported.

### What operating systems are supported for TKE hosts?

Currently, Ubuntu 16.04 and CentOS 7.2 are supported. If you need other operating systems, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

## CVM Scaling FAQ

### What are the limitations on CVM scaling?

You can only choose the region where your current cluster resides, but you may choose a different AZ. Clusters can be deployed across AZs.

### Is there a limit on the number of CVMs?

Yes. There is a limit on the number of pay-as-you-go CVMs each user can own. For details, see [CVM Overview](https://console.cloud.tencent.com/cvm/overview).

## CVM Termination FAQ

### After a CVM is terminated, what will happen to the containers deployed in it?

When a CVM instance is terminated, the resources it contains, such as containers, will also be terminated. If the number of containers for a service drops below the expected number of running containers, the cluster will launch more containers in other CVM instances until the desired number is met.
