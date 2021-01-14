### How do I access my TencentDB for Tendis instance?
TencentDB for Tendis can be accessed with private network addresses, the data management console (DMC), and programing languages. For more information, please see [Accessing Tendis Instances](https://intl.cloud.tencent.com/document/product/1083/39268).

### What should I do if my TencentDB for Tendis instance is unpingable? 
Tendis prohibits `ping` by default. You can use `telnet` to check connectivity.

### How do I enable access to TencentDB for Tendis over a public network? 
TencentDB for Tendis does not support public network access for the time being. If you want to access it over a public network, you can do so through the port forwarding with [iptables](https://intl.cloud.tencent.com/document/product/1083/39269) on a CVM instance that enables public network access.
>?Port forwarding with iptables is not stable, so we do not recommend this public network access solution in a production environment.
