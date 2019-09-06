## Cluster Creation FAQs

### Can I not select a public IP for the CVM instance when creating a cluster?

Yes. A CVM instance with no public IP can only pull images from "My Images" in Image Registry but not Docker Hub images or third-party images.
A CVM instance with no public IP but with internet bandwidth can access the internet by binding an EIP.

### Why do I need to choose a network when creating a cluster?

The selected network and subnet are where the CVM instance resides. You can achieve cross-AZ disaster recovery by adding different CVM instances to subnets in different AZs.

### What CVM models are supported for cluster creation?

All models with pay-as-you-go system disks as cloud disks are supported.

### What operating systems are supported for TKE hosts?

Currently, Ubuntu 16.04 and CentOS 7.2 are supported. If you need other operating systems, please contact us by submitting a ticket.

## CVM Scaling FAQs

### What are the limitations of CVM scaling?

You can only choose a region where your current cluster resides, but you may choose a different AZ. Clusters can be deployed across AZs.

### Is there a limit to the number of CVM instances?

Yes. There is a limit to the number of pay-as-you-go CVMs each user can own. For more information, see [CVM Overview](https://console.cloud.tencent.com/cvm/overview).

## CVM Instance Termination FAQs

### After a CVM instance is terminated, what will happen to the containers deployed in it?

When a CVM instance is terminated, resources in it such as containers will be terminated too. If the number of containers for a certain service drops below the expected number of running containers, the cluster will launch more containers in other CVM instances until the desired number is met.
