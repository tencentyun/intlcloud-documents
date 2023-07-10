## Installation and Use Process

### 1. Create a namespace

```shell
$ kubectl create ns fluid-system
```


### 2. Download Fluid

You can go to the Fluid official website [Fluid Releases](https://github.com/fluid-cloudnative/fluid/releases) to download Fluid 0.6.0 or later. By default, the latest version is recommended.


### 3. Install Fluid with Helm

```shell
$ helm install --set runtime.goosefs.enabled=true fluid fluid-0.8.0.tgz
```

### 4. Check the running status of Fluid

```shell
$ kubectl get pod -n fluid-system
NAME                                         READY   STATUS    RESTARTS   AGE
csi-nodeplugin-fluid-2mfcr                   2/2     Running   0          108s
csi-nodeplugin-fluid-l7lv6                   2/2     Running   0          108s
dataset-controller-5465c4bbf9-5ds5p          1/1     Running   0          108s
goosefsruntime-controller-654fb74447-cldsv     1/1     Running   0          108s
```

The number of `csi-nodeplugin-fluid-xx` must be the same as the number of nodes in the Kubernetes cluster.

Now, Fluid is successfully installed. If you want to customize an image and upgrade the system CRD, see the following instructions (optional).

### 5. Customize an image

Decompress `fluid-0.8.0.tgz` and modify the default `values.yaml` file:
```yaml
runtime:
  mountRoot: /runtime-mnt
  goosefs:
    runtimeWorkers: 3
    portRange: 26000-32000
    enabled: false
    init:
      image: fluidcloudnative/init-users:v0.8.0-116a5be
    controller:
      image: fluidcloudnative/goosefsruntime-controller:v0.8.0-116a5be
    runtime:
      image: ccr.ccs.tencentyun.com/qcloud/goosefs:v1.2.0
    fuse:
      image: ccr.ccs.tencentyun.com/qcloud/goosefs:v1.2.0
```

You can modify the default `image` content related to GooseFS. For example, you can change the location of the image to your own repository. After modification, run `helm package fluid` again for packaging and run the following command to update the Fluid version:
```shell
helm upgrade --install fluid fluid-0.8.0.tgz
```

### 6. Update the CRD

```shell
$ kubectl get crd      
NAME                                             CREATED AT
databackups.data.fluid.io                        2021-03-02T13:12:31Z
dataloads.data.fluid.io                          2021-04-14T11:14:58Z
datasets.data.fluid.io                           2021-03-02T13:12:31Z
goosefsruntimes.data.fluid.io                    2021-04-13T13:31:38Z
```

The following shows how to update the existing GooseFSRuntime CRD in the system.

First, delete the existing CRD:

```shell
kubectl delete crd goosefsruntimes.data.fluid.io
```

Then, decompress `fluid-0.8.0.tgz`:

```shell
$ ls -l fluid/
total 32
total 32
-rw-r--r--  1 xieydd  staff   489  5 15 16:14 CHANGELOG.md
-rw-r--r--  1 xieydd  staff  1061  7 22 00:08 Chart.yaml
-rw-r--r--  1 xieydd  staff  2560  5 15 16:14 VERSION
drwxr-xr-x  8 xieydd  staff   256  7 20 15:06 crds
drwxr-xr-x  7 xieydd  staff   224  5 24 14:18 templates
-rw-r--r--  1 xieydd  staff  1665  7 22 00:08 values.yaml
```

Finally, create a new CRD:

```shell
kubectl apply -f crds/data.fluid.io_goosefsruntimes.yaml
```
