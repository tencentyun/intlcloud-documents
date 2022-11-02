
## Inaccessibility After Private Network Access Is Enabled
You can [enable private network access](https://intl.cloud.tencent.com/document/product/457/30639) in the TKE console. If resources still cannot be accessed, check the following based on your cluster type:

#### Managed cluster[](id:ManagedCluste)
Check whether the security group of the node in the cluster correctly opens the port range of 30000–32768 as instructed in "Viewing node security group configurations".

#### Self-deployed cluster
1. Check whether the security group of the node in the cluster correctly opens the port range of 30000–32768 as instructed in "Viewing node security group configurations".
- When enabling private network access, you set the VPC subnet IP range in the console. Check whether the Master node in the cluster allows this VPC subnet IP range.
- Check whether the security group of the Master node in the cluster correctly opens the VPC IP range and VPC subnet IP range where the Master node is located.

## Inaccessibility After Public Network Access Is Enabled
You can [enable public network access](https://intl.cloud.tencent.com/document/product/457/30639) in the TKE console. If resources still cannot be accessed, check the following based on your cluster type:

#### Managed cluster
Check whether the source CIDR block of the security group is configured correctly. You can also set the source `0.0.0.0/0` to be fully open to the public network, and test the Internet access again.

#### Self-deployed cluster
When public network access is enabled for the self-deployed cluster, the `default/kubelb-internet` Service object will be automatically created in the cluster. This Service will be automatically bound to a public network CLB instance. By default, this CLB instance will not be bound to a security group (that is, fully open to the internet), and the `EXTERNAL-IP` field shows the VIP of the CLB instance.
```
$ kubectl get service kubelb-internet
NAME              TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)         AGE
kubelb-internet   LoadBalancer   172.16.252.94   152.136.8.98   443:32750/TCP   3m4s
```
1. Check whether the CLB bound to the `default/kubelb-internet` Service object has a security group configured correctly.
- Check whether the security group of the master node in the cluster correctly opens the port range of 30000–32768 as instructed in "Viewing node security group configurations".
- Check whether the security group of the Master node in the cluster correctly opens the VPC IP range and VPC subnet IP range where the Master node is located.
