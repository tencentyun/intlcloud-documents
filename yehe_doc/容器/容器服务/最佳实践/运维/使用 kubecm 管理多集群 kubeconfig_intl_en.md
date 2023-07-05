## Overview

Kubectl is a command line tool provided by Kubernetes for performing operations on clusters. It uses kubeconfig as a configuration file (the default path is `~/.kube/config`) to configure the information of multiple clusters, and manage and operate multiple clusters.  


To manage and operate the TKE or TKE Serverless cluster through Kubectl, you need to enable the APIServer's public or private network access on the cluster basic information page to obtain kubeconfig (cluster access credentials). If you need to use kubectl to manage multiple clusters, generally you need to extract the contents of each field in kubeconfig and merge them into the kubeconfig file of the device where kubectl locates. This method is complicated and may easily cause an error.  

Through the kubecm tool, you can merge multiple cluster access credentials into kubeconfig more simply and efficiently. This document describes how to use kubecm to efficiently manage the kubeconfig of multiple clusters.  



## Prerequisites


- You have created a [TKE general cluster](https://intl.cloud.tencent.com/document/product/457/30637) or [TKE Serverless cluster](https://intl.cloud.tencent.com/document/product/457/34048).  
- You have installed the [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) command line tool on the device used for managing multiple clusters.  


## Directions

### Installing kubecm

Install [kubecm](https://kubecm.cloud/#/en-us/install) on the device used for managing multiple clusters.  


### Obtaining cluster access credential

After creating a cluster, you need to follow the steps below to obtain access credential for the cluster:


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar. 
2. Click the ID/name of the cluster for which the access credential needs to be obtained to go to the basic information page of the cluster.  
3. On the **Basic Information** page, enable **Internet access** and **Private network access** in the **Cluster APIServer Information** section.
4. Click **Download** on the right of **KubeConfig**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Uh6S688_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206170914.png)



### Using kubecm to add access credential to kubeconfig

This document takes the cluster access credential `cls-l6whmzi3-config` as an example. Run the following command to use kubecm to add the access credential to kubeconfig (`-n` means you can specify the context name):
```plaintext
kubecm add -f cls-l6whmzi3-config -n cd -c
```

### Viewing the cluster list

Run the following `kubecm ls` command to view the cluster list in kubeconfig (the asterisk identifies the cluster under operation):

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


Run the following `kubecm switch` command to interactively switch to another cluster:

![](https://main.qcloudimg.com/raw/3eea3d35d3a19f93906eabf60a423a0b.png)

### Removing the cluster

Run the following `kubecm delete` command to remove a cluster:

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

## Learn More

- [Open-source kubecm](https://github.com/sunny0826/kubecm)
- [kubecm official documents](https://kubecm.cloud)
