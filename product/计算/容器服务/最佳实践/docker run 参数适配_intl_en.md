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
![](https://main.qcloudimg.com/raw/86b13d42143d526aa7494b9069fba1ee.png)

`--restart`: Specifies whether to restart the container when the container exits. All containers created by TKE will be restarted when they exit, so this parameter does not need to be specified in the TKE console.

`-v`: Specifies the container volume. The previous command specifies three volumes, and, correspondingly, in TKE console, we need to add three **Volumes**, then mount the three volumes into the container through**Advanced Settings**.

First, create three volumes:
![](https://main.qcloudimg.com/raw/180afd444ace31c1ad0d93352e81f83e.png)

Then, mount the three volumes into the container through **Advanced Settings**:
![](https://main.qcloudimg.com/raw/d3dee9fe11dbbbf263e987d1b186ee2c.png)

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

![](https://main.qcloudimg.com/raw/a35fca2870f6ef4a16bc753b6be2dddc.png)
