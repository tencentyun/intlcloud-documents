## Logging In to the Container Through SSH
If the SSH server is installed on your container, you can log in to the container through SSH.
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the cluster ID (cls-xxx) to go to the cluster details page.
3. On the cluster details page, select **Node Management** > **Node** in the left sidebar.
4. On the **Node List** page, click the node name to go to the Pod management page.
5. In the instance list, obtain the IP address of the instance, as shown below:
![](https://main.qcloudimg.com/raw/15a173b8b8f7361bc513ba6775b27476.png)
6. Log in to any node in the cluster. For more information, see [here](https://www.tencentcloud.com/document/product/213/5436).
7. Log in to the container through SSH.


## Logging In to a Container Through the Container's Node
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the cluster ID (cls-xxx) to go to the cluster details page.
3. On the cluster details page, select **Node Management** > **Node** in the left sidebar.
4. On the **Node List** page, click the node name to go to the Pod management page.
5. In the instance list, obtain the IP address of the node to which the container belongs and the container ID.
![](https://main.qcloudimg.com/raw/315aa6adafe081824c86d827b128dbe6.png)
6. Log in to the node. For more information, see [here](https://www.tencentcloud.com/document/product/213/5436).
7. Run the `docker ps` command to view the container you want to log in to.
```shell
[root@VM_88_88_centos ~]# docker ps | grep 75b3b15af61a  
75b3b15af61a       nginx:latest       "nginx -g 'daemon off"   About a minute ago   Up About a minute  k8s_worid.e8b44cc_worid-24bn2_default_81a59654-aa14-11e6-8a18-52540093c40b_42c0b746
```
8. Run the `docker exec` command to log in to the container.
```shell
[root@VM_0_60_centos ~]# docker ps | grep 75b3b15af61a
75b3b15af61a        nginx:latest                                 "nginx -g 'daemon off"   2 minutes ago       Up 2 minutes                            k8s_worid.e8b44cc_worid-24bn2_default_81a59654-aa14-11e6-8a18-52540093c40b_6b389dd2
[root@VM_0_60_centos ~]# docker exec -it 75b3b15af61a /bin/bash
root@worid-24bn2:/# ls
bin  boot  devetc  home  liblib64  media  mnt  optproc  root  run  sbin  srv  sys  tmp  usr  var
```







