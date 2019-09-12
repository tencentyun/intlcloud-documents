## docker run Parameter Adaptation

  This document describes how to match the parameters of `docker run` and TKE console when you migrating a container that has been debugged in local Docker to TKE. Here, we use the creation of a simple GitLab service as an example.

### 1. Sample of GitLab Container Parameter

We can create a simple GitLab container by using the `docker run` command, as follows:

```shell
docker run \
-d \
-p 20180:80 \
-p 20122:22 \
--restart always \
-v /data/gitlab/config:/etc/gitlab \
-v /data/var/log/gitlab:/var/log/gitlab \
-v /data/gitlab/data:/var/opt/gitlab \
--name gitlab \
gitlab/gitlab-ce:8.16.7-ce.0

```



`-d`: Specifies to run containers in the backend. As TKE always runs containers in backend, you don’t need to specify this parameter in TKE console.

`-p`: Specifies the port mapping. We have mapped two ports here, the container ports are 80 and 22, and the externally exposed ports are 20180 and 20122 respectively. And in the console, we need to add two port mapping rules and enter the corresponding target port and service port. Since gitlab container needs to provide public network access, please select the **Via Internet** in access mode.
![](https://mc.qcloudimg.com/static/img/cf73ee3d941a768491d52af56a386db4/image.png)

`--restart`: Specifies whether to restart the container when the container exits. All containers created by TKE will be restarted when they exit, so this parameter does not need to be specified in the TKE console.

`-v`: Specifies the container volume. The previous command specifies three volumes, and, correspondingly, in TKE console, we need to add three **Volumes**, then mount the three volumes into the container through**Advanced Settings**.

First, create three volumes:
![](https://mc.qcloudimg.com/static/img/c5b11b2c717c263aa68a2aab12234fad/volume.png)

Then, mount the three volumes into the container through **Advanced Settings**:
![](https://mc.qcloudimg.com/static/img/d4130bd91b37fd76b6de759c2f8a1075/mount.png)

Note: We selected **Local Disk** as the volume type, so the data generated during the running process of the container will be saved to the node where the container is located. If the container is switched to another node, the data will be lost. We can use **Cloud Disk** volumes to save the container’s data to the cloud disk, preventing data loss if the container is scheduled to another node.

`--name`: The name of the running container. This parameter corresponds to the service name in the TKE console. Of course, the container name can be the same as the service name.

### 2. Other Parameters

This section describes other common parameters used for executing `docker run`:

`-i`: Specifies to execute containers interactively. The TKE console only supports running containers in the backend, so this parameter is not supported.

`-t`: This parameter is not supported by TKE.

`-e`: The environment variable of the running container. For example, the user executes the following `docker run` command:

```
docker run -e FOO='foo' -e BAR='bar' --name=container_name container_image
```

Container environment variables can be added through the **Advanced Settings** of the container when a service is created in the TKE console. Here, the user is going to add two environment variables for the container: `Foo` with a value of `foo` and `Bar` with a value of bar.

### 3. Commands and Args

Sometimes we want to specify a command and parameter for `docker run`, for example:

```
docker run --name=kubedns gcr.io/google_containers/kubedns-amd64:1.7 /kube-dns --domain=cluster.local. --dns-port=10053 -v 2

```

Here, we specified the container process name: `/kube-dns`, and specified three parameters: `-domain=cluster.local.`, `--dns-port=10053`, and `-v 2`.
In the console, we can specify as follows:

![](https://mc.qcloudimg.com/static/img/cf991cd098b96c19b70b1da4e11507c5/image.png)