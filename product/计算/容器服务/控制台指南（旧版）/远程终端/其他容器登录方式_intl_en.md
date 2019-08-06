### Logging in to Container via the Web Terminal (Recommended)
1. Log into [TKE Console](https://console.cloud.tencent.com/tke2).
2. Select the node to which the container belongs, click to enter the pod management details page, view the list of pods, select a container, and log in to the remote terminal.
3. For FAQs about the remote terminal, please [view here](https://intl.cloud.tencent.com/document/product/457/31426).

![Alt text](https://main.qcloudimg.com/raw/075fe82f92f02418b467e48e47f6ed84.png)

### Logging in to Container via the Container's Node
1. Obtain the IP address of the node where the container resides and the container's ID.
![Alt text](https://main.qcloudimg.com/raw/315aa6adafe081824c86d827b128dbe6.png)

2. Log in to the node. For more information, see [Logging in to CVM](https://intl.cloud.tencent.com/doc/product/213/5436).

3. Run the `docker ps` command to view the container you want to log into.
```shell
[root@VM_88_88_centos ~]# docker ps | grep 75b3b15af61a  
75b3b15af61a       nginx:latest                                 "nginx -g 'daemon off"   About a minute ago   Up About a minute                       k8s_worid.e8b44cc_worid-24bn2_default_81a59654-aa14-11e6-8a18-52540093c40b_42c0b746
```
4. Run the `docker exec` command to log into the container.
```shell
[root@VM_0_60_centos ~]# docker ps | grep 75b3b15af61a
75b3b15af61a        nginx:latest                                 "nginx -g 'daemon off"   2 minutes ago       Up 2 minutes                            k8s_worid.e8b44cc_worid-24bn2_default_81a59654-aa14-11e6-8a18-52540093c40b_6b389dd2
[root@VM_0_60_centos ~]# docker exec -it 75b3b15af61a /bin/bash
root@worid-24bn2:/# ls
bin  boot  dev	etc  home  lib	lib64  media  mnt  opt	proc  root  run  sbin  srv  sys  tmp  usr  var
```

### Logging in to Container via SSH (When SSH Server is Already Installed on the Container)
1. Obtain the IP address of the container.
![Alt text](https://main.qcloudimg.com/raw/15a173b8b8f7361bc513ba6775b27476.png)

2. Log in to any node in the cluster. For more information, see [Logging in to CVM](https://intl.cloud.tencent.com/doc/product/213/5436).

3. Log in to the container via SSH.



