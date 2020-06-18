## Cluster Creation

### Can I choose not to set a public IP address for the CVM when creating a cluster?

Yes. A CVM without a public IP address can only pull images from "My Images" in Image Repository but not Docker Hub images or third-party images.
A CVM without a public IP address but with Internet bandwidth can access the Internet by binding an EIP.

### Why do I need to choose a network when creating a cluster?

The selected network and subnet are where the CVM resides. You can add different CVMs to subnets in different AZs for cross-AZ disaster recovery.

### What CVM models are supported when creating a cluster?

All pay-as-you-go models that use cloud disks as system disks are supported.

### What operating systems are supported for TKE hosts?

Currently, Ubuntu 16.04 and CentOS 7.2 are supported. If you need other operating systems, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

## Adding CVMs

### What are the limitations on adding CVMs to a cluster?

You can only choose the CVMs in the same region as the cluster. But you may choose a different AZ to implement cross-AZ deployment of the cluster.

### Is there a limit on the number of CVMs?

Yes. The number of pay-as-you-go CVMs cannot exceed the usage quota of the current account. For details, see [CVM Overview](https://console.cloud.tencent.com/cvm/overview).

## CVM Termination

### After a CVM is terminated, what will happen to the containers deployed in it?

When a CVM instance is terminated, the resources it contains, such as containers, will also be terminated. If the number of containers for a service drops below the expected number of running containers, the cluster will launch more containers in other CVM instances until the desired number is met.
