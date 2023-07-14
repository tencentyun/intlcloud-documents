### Are there any additional charges for adding components after a cluster is created?
EMR charges you fees based on the nodes used in the cluster deployment, with no additional charge for adding components.

### Why the EMR on CVM console shows node auto-renewal, but the associated CVM instance in the CVM console does not?
EMR cluster nodes are composed of CVM instances, and their billing type and auto-renewal are managed in the EMR console.

### Does renewing an EMR on CVM node renew the associated cloud disk (CBS)?
A system disk has a renewal period same as the nodes and does not need to be renewed separately. The renewal of a cloud data disk depends on how the node renewal is set. If nodes are renewed manually or automatically in the EMR console, the associated cloud data disks do not need to be renewed separately; if they are renewed through the Billing Center, the cloud data disks need to be renewed separately.

