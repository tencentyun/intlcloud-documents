## Overview

Many DevOps requirements need to be implemented with Jenkins. This document describes how to deploy Jenkins in TKE.  

## Prerequisites

You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637).  

## Directions

### Installing Jenkins

1. Log in to the TKE console and click **[Marketplace](https://console.cloud.tencent.com/tke2/market)** on the left sidebar.  
2. On the **Marketplace** page, search for `Jenkins` and enter the Jenkins application page.  
3. Click **Create Application** and configure `values.yaml` in **Parameters** as needed.  
![](https://qcloudimg.tencent-cloud.cn/raw/03ec3394fc4813137d4034dc4402e8f7.png)
4. Click **Create**.  

### Exposing Jenkins UI

By default, you can't access the Jenkins UI outside the cluster. To access it, you can use an Ingress. TKE provides [CLB type Ingress](https://intl.cloud.tencent.com/document/product/457/37013) and [Nginx type Ingress](https://intl.cloud.tencent.com/document/product/457/38980) for your choice.  


### Logging in to Jenkins

On the Jenkins UI, enter the initial username and password to log in to the Jenkins backend. The username is `admin`, and the password can be obtained by running the following command.  

```bash
kubectl -n devops get secret jenkins -o jsonpath='{.data.jenkins-admin-password}' | base64 -d
```

>!When running the above command, replace the text with the actual namespace.  

### Creating user



We recommend you manage Jenkins as a general user. Before creating a general user, you need to configure an authentication and authorization policy.  

1. Log in to the Jenkins backend and click **Dashboard** > **Manage Jenkins** > **Security** > **Configure Global Security** to enter the authentication and authorization policy page as shown below:
![](https://main.qcloudimg.com/raw/98801d650feb5e2a9623dff3057a1c1a.png)
 - **Security Realm**: Select **Jenkins' own user database**.  
 - **Authorization**: Select **Logged-in users can do anything**.  
2. Click **Dashboard** > **Manage Jenkins** > **Security** > **Manage Users** > **Create User** and create a user as prompted as shown below:
	![](https://main.qcloudimg.com/raw/b0e04f93312ee575d42d074979f4797f.png)
	- **Username**: Enter the username.  
	- **Password**: Enter the password.  
	- **Confirm password**: Confirm the password.  
	- **Full name**: Enter the full username.  
3. Click **Create User**.  




### Installing plugin

Log in to the Jenkins backend and click **Dashboard** > **Manage Jenkins** > **System Configuration** > **Manage Plugins** to enter the plugin management page.  
![](https://main.qcloudimg.com/raw/3f0c59f227e66ff388a41c2bfbb07fe3.png)
You can install the following commonly used plugins:
- kubernetes
- pipeline
- git
- gitlab
- github
