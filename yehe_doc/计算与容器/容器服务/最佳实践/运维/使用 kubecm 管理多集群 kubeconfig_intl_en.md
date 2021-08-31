## Overview

Kubectl is a command line tool provided by Kubernetes for performing operations on clusters. It uses Kubeconfig as a configuration file (the default path is `~/.kube/config`) to configure the information of multiple clusters, and manage and operate multiple clusters.


To manage and operate the TKE or EKS cluster through Kubectl, you need to enable the APIServer's public or private network access on the cluster basic information page to obtain Kubeconfig (cluster access credentials). If you need to use Kubectl to manage multiple clusters, generally you need to extract the contents of each field in Kubeconfig and merge them into the Kubeconfig file of the device where Kubectl locates. This method is complicated and may easily cause an error.

Through kubecm tool, you can merge multiple cluster access credentials into kubeconfig more simply and efficiently. This document describes how to use kubecm to efficiently manage the Kubeconfig of multiple clusters.



## Prerequisites


- You have created a [TKE](https://intl.cloud.tencent.com/document/product/457/30637) or [EKS](https://intl.cloud.tencent.com/document/product/457/34048) cluster.
- You have installed [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) command line tool on the device used for managing multiple clusters.


## Directions

### Installing kubecm

Install [Kubecm](https://kubecm.cloud/#/en-us/install) on the device used for managing multiple clusters.


### Obtaining cluster access credential

After creating a TKE or EKS cluster, you need to follow the instructions below to obtain access credentials for [TKE](#tke) or [EKS](#eks) cluster.


<span id="tke"></span>

#### Obtaining access credential for TKE cluster

1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID/name of the cluster that needs to obtain the access credential to go to the management page.
3. Click **Basic Information** on the left side.
4. On the **Basic Information** page, enable **Internet Access** and **Private Network Access** in **Cluster APIServer Information** section.
![](https://main.qcloudimg.com/raw/e03c7edb546614e72c0de61dec459098.png)
5. Click **Download** on the right side of **Kubeconfig** to download Kubeconfig.


<span id="eks"></span>

#### Obtaining access credential for EKS cluster

1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar.
2. Click the ID/name of the cluster that needs to obtain the access credential to go to the management page.
3. Click **Basic Information** on the left side.
4. On the **Basic Information** page, enable **Internet Access** and **Private Network Access** in **Cluster APIServer Information** section.
![](https://main.qcloudimg.com/raw/e3e4c60083734403e783b819d747d38c.png)
5. Click **Download** on the right side of **Kubeconfig** to download Kubeconfig.




### Using Kubecm to add access credential to Kubeconfig

This document takes the cluster access credential `cls-l6whmzi3-config` as an example. Run the following command, use Kubecm to add the access credential to Kubeconfig (`-n` means you can specify the context name). Examples are as follows:
```plaintext
kubecm add -f cls-l6whmzi3-config -n cd -c
```

### Viewing cluster list

Run the command `kubecm ls` to view the cluster list in kubeconfig (The asterisk identifies the cluster is under operation), as shown below:

```plaintext
$ kubecm ls
+------------+------------+-----------------------+--------------------+-----------------------------------+-------------------+
|   CURRENT  |    NAME    |        CLUSTER        |        USER        |               SERVER              |     Namespace     |
+============+============+=======================+====================+===================================+===================+
|      *     |     cd     |   cluster-chh6kgf9d9  |   user-chh6kgf9d9  |   https://cls-l6whmzi3.ccs.tence  |      default      |
|            |            |                       |                    |            nt-cloud.com           |                   |
+------------+------------+-----------------------+--------------------+-----------------------------------+-------------------+
|            |     bj     |   cluster-6qaua96n    |   user-6qaua96n    |   https://cls-6qaua96n.ccs.tence  |    kube-system    |
|            |            |                       |                    |            nt-cloud.com           |                   |
+------------+------------+-----------------------+--------------------+-----------------------------------+-------------------+
```

### Switching the cluster


Run the command `kubecm switch` to interactively switch to another cluster, as shown below:

![](https://main.qcloudimg.com/raw/3eea3d35d3a19f93906eabf60a423a0b.png)

### Removing the cluster

Run the command `kubecm delete` to remove a cluster, as shown below:

```plaintext
$ kubecm delete bj
Context Delete:「bj」
「/Users/roc/.kube/config」 write successful!
+------------+---------+-----------------------+--------------------+-----------------------------------+--------------+
|   CURRENT  |   NAME  |        CLUSTER        |        USER        |               SERVER              |   Namespace  |
+============+=========+=======================+====================+===================================+==============+
|            |    cd   |   cluster-chh6kgf9d9  |   user-chh6kgf9d9  |   https://cls-l6whmzi3.ccs.tence  |    default   |
|            |         |                       |                    |            nt-cloud.com           |              |
+------------+---------+-----------------------+--------------------+-----------------------------------+--------------+
```

## References

- [Open-source kubecm](https://github.com/sunny0826/kubecm)
- [kubecm Official Documents](https://kubecm.cloud)
