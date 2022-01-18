
## Overview
This document describes how to obtain an access credential for a TCR Enterprise Edition instance in Tencent Container Registry (TCR). To push and pull container images, you must first run the `docker login` command on the access client and enter your username and password (the credential) to log in to the instance.

TCR Enterprise Edition instances support both a long-term access credential and a temporary login command, in which:
- **Long-term access credential**: is permanently valid after being generated. It can be disabled and deleted. Long-term access credentials can be applied in scenarios such as early-stage testing, CICD assembly lines, and container cluster image pull.
>!Please keep the access credential properly after it is generated. If it is lost, disable or delete it promptly.
>
- **Temporary login token**: is valid for 1 hour and cannot be disabled or terminated after being generated. It can be applied in scenarios such as temporary use and one-time external authorization. Production clusters with high security requirements can also use this method through regular refreshing.



## Prerequisite

Before obtaining an access credential for a TCR Enterprise Edition instance, you must complete the following preparations.
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- To obtain the access credential through an API, you need to obtain the [API key](https://console.cloud.tencent.com/cam/capi) for calling API 3.0.

## Directions

### Obtaining a long-term access credential
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and click **Access Credential** in the left sidebar.
2. On the "Access Credential" page, choose a region and an instance. Click **Create**.
3. In the "Create Access Credential" window that pops up, complete the following steps to obtain an access credential:
   1. In the "Create Access Credential" step, enter the usage of the credential in **Usage Description**, and click **Next**.
   2. In the "Save Access Credential" step, click **Save Access Credential** to download the credential. **Please save the access credential properly. You will not be able to get it again.**
3. After the creation, you can view, disable, or delete the credential on the **Access Credential** page.

### Obtaining a temporary login token
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and click **Access Credential** in the left sidebar.
2. On the "Access Credential" page, choose a region and an instance. Click **Generate Temp Login Token**.
3. In the "Temp login token" window that pops up, click **Copy login token** to obtain the temporary access credential.


### Creating via API

You can also create an instance access credential via CreateInstanceToken API.



## Subsequent Operations
Refer to [Logging in to the TCR instance](https://intl.cloud.tencent.com/document/product/1051/35484) to log in to the TCR Enterprise Edition instance.


## Notes
#### A long-term access credential will be created automatically in some scenarios:
1. When you install the TCR plugin in a TKE cluster, a long-term access credential will be created automatically for the selected instance. This credential will not be terminated automatically when the plugin is deleted. If you do not want to use it any more, you need to delete it manually.
2. When you use an image to build or deliver the pipeline feature, a dedicated access credential will be auto-created and provided to CODING DevOps service to push the auto-built images. Do not delete the access credential directly, otherwise, it will cause the failure of existing image building configuration.
