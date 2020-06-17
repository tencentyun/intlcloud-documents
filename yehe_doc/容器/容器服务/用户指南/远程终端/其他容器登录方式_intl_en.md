### Logging In to a Container Through a Web Terminal (Recommended)

1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the "Cluster Management" page, click the cluster ID (cls-xxx) to go to the cluster details page.
3. On the cluster details page, choose **Node Management** > **Nodes** in the left sidebar.
4. On the "Node List" page, select the node to which the target container belongs, and click to go to the details page for pod management. Browse the instance list, select the target container, and log in to the remote terminal, as shown in the following figure.

> For FAQs on the remote terminal, see [here](https://cloud.tencent.com/document/product/457/8638?).
> Containers meeting any of the following conditions do not support remote login:
>
> - The namespace is kube-system.
> - No bash is available in the container image.

### Logging In to a Container Through the Node for the Container

1. Obtain the IP address of the node to which the target container belongs.
2. Log in to the node. For more information, see [Logging In to a CVM](https://cloud.tencent.com/doc/product/213/5436).
3. Run the `docker ps` command to view the target container.

```shell
[root@VM_88_88_centos ~]# docker ps | grep 75b3b15af61a  
75b3b15af61a       nginx:latest       "nginx -g 'daemon off"   About a minute ago   Up About a minute  k8s_worid.e8b44cc_worid-24bn2_default_81a59654-aa14-11e6-8a18-52540093c40b_42c0b746
```

4. Log in to the target container with `docker exec`  command.

```shell
[root@VM_0_60_centos ~]# docker ps | grep 75b3b15af61a
75b3b15af61a        nginx:latest                                 "nginx -g 'daemon off"   2 minutes ago       Up 2 minutes                            k8s_worid.e8b44cc_worid-24bn2_default_81a59654-aa14-11e6-8a18-52540093c40b_6b389dd2
[root@VM_0_60_centos ~]# docker exec -it 75b3b15af61a /bin/bash
root@worid-24bn2:/# ls
bin  boot  dev	etc  home  lib	lib64  media  mnt  opt	proc  root  run  sbin  srv  sys  tmp  usr  var
```

### Logging In to a Container with an SSH Terminal Installed Through SSH

1. Obtain the IP address of the container.
2. Log in to any node in the cluster. For more information, see [Logging In to a CVM](https://cloud.tencent.com/doc/product/213/5436).
3. Log in to the container through SSH.
