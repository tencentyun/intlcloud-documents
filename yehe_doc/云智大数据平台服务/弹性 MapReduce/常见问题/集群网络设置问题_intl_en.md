### What should I do if the error "No subnet in the AZ selected for the cluster" is displayed when I try to set the cluster network on the purchase page?
![](https://main.qcloudimg.com/raw/9bbef630ccf7191724de2694bff2bfda.png)
A VPC can be deployed across AZs, and all VPCs in the current region will be loaded by default. A subnet belongs to an AZ, and all existing subnets in the AZ where the cluster resides will be loaded by default. Please check whether there are available subnets in the selected AZ.
