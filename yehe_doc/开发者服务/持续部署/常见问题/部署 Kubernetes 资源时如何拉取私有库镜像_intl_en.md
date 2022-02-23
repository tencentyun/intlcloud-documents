This document describes how to pull images from a private repository when deploying Kubernetes resources.

## Prerequisites

You must activate the CODING DevOps service for your Tencent Cloud account before you can use Coding Continuous Deployment (CD). 

## Open Project

1. Log in to the [CODING console](https://console.cloud.tencent.com/coding) and click the team domain name to enter the CODING page.
2. On the Workspace homepage, click <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" style ="margin:0" data-nonescope="true"> on the left to go to the Continuous Deployment console.

### Feature Overview

When deploying Kubernetes resources, if the images referenced by manifest are stored in a private repository, you need to configure `imagePullSecrets` in manifest to pull the images.

The following describes how to configure `imagePullSecrets` for different types of cloud accounts:

#### Tencent Cloud TKE

![](https://qcloudimg.tencent-cloud.cn/raw/574f87f69b4cc268c7467f73b2fb5d0c.png)
As shown above, CODING-CD generates a Secret named `coding-registry-cred-$(user_id)` in the TKE cluster. You can view the Secret information in the TKE console:
![](https://qcloudimg.tencent-cloud.cn/raw/45354622b6be37c4de9c2b2aa0f1a8a2.png)
After a cloud account is added, you can view the sample usage：
![](https://qcloudimg.tencent-cloud.cn/raw/925fb602f377a95c5494509740b92466.png)

#### Kubernetes cloud accounts (non-TKE cluster)

For a Kubernetes cloud account added with Kubeconfig or Service Account credentials, you need to create a Secret in the Kubernetes cluster before manifest can reference images from a private repository (CODING artifact repository is taken as an example here):
![](https://qcloudimg.tencent-cloud.cn/raw/dd76ee6beb0ab28012db43acf882b885.png)
If you directly reference images from the private repository in mainfest without generating a Secret in the cluster, the operation will fail.

```shell
kubectl create secret docker-registry coding-regcred \
--docker-server=Your team domain --docker-username=Your email --docker-password=$(passwd)
```

After a Secret is generated, use `imagePullSecrets` in manifest to configure the Secret for pulling images (the last two lines).

```yaml
apiVersion: apps/v1
kind: Deployment
...
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
      imagePullSecrets:
      - name: coding-regcred
```

For more information, see [How to pull images from a private repository in Kubernetes](https://kubernetes.io/zh/docs/tasks/configure-pod-container/pull-image-private-registry)

#### Kubernetes cloud accounts (TKE cluster)

If you add a TKE cluster cloud account using a Kubeconfig or Service Account, you can directly create a Secret on the TKE console. Go to the cluster Information page, and select **Configuration Management** > **Secret** > **New**:
![](https://qcloudimg.tencent-cloud.cn/raw/56dd3e6fe6d4b27db63f1f022991f99e.png)
Fill in the form as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/45b27e63b845a62b5f02e78b918e061f.png)

Similarly, after a Secret is generated, use `imagePullSecrets` in manifest to configure the secret for pulling images (the last two lines).

```yaml
apiVersion: apps/v1
kind: Deployment
...
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
      imagePullSecrets:
      - name: coding-regcred
```

