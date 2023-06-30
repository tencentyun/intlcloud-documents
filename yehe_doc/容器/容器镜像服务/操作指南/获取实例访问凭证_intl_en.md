
## Overview
This document describes how to obtain an access credential for a TCR Enterprise Edition instance in Tencent Container Registry (TCR). To push and pull container images, you must first run the `docker login` command on the access client and enter your username and password (the credential) to log in to the instance.

TCR Enterprise Edition instances support both a long-term access credential and a temporary login command, in which:
- **Long-term access credential**: is permanently valid after being generated. It can be disabled and deleted. Long-term access credentials can be applied in scenarios such as early-stage testing, CICD assembly lines, and container cluster image pull.
>!Please keep the access credential properly after it is generated. If it is lost, disable or delete it promptly.
>
- **Temporary login token**: is valid for 1 hour and cannot be disabled or terminated after being generated. It can be applied in scenarios such as temporary use and one-time external authorization. Production clusters with high security requirements can also use this method through regular refreshing.



## Prerequisites

Before obtaining an access credential for a TCR Enterprise Edition instance, you must complete the following preparations.
- You have [purchased a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088).
- To obtain the access credential through an API, you need to obtain the [API key](https://console.cloud.tencent.com/cam/capi) for calling API 3.0.

## Directions

### Obtaining a long-term access credential
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and click **Instance** in the left sidebar.
2. On the "Instance List" page, choose an instance name to go to the instance details page.
3. Click the **Access Credential** tab, click **Create**, and complete the following steps to obtain an access credential:
   1. In the **Create Access Credential**, enter the usage of the credential in **Usage Description**, and click **Next**.
   2. In the **Save Access Credential**, click **Save Access Credential** to download the credential. **Please save the access credential properly. You will not be able to get it again.**
3. After the creation, you can view, disable, or delete the credential on the **Access Credential** page.

### Obtaining a temporary login token
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and click **Instance** in the left sidebar.
2. On the "Instance List" page, choose an instance name to go to the instance details page.
3. Click the **Access Credential** tab and click **Generate Temp Login Token**. In the pop-up window, click **Copy login token** to obtain the temporary credential.


## Reference

You can also use the `CreateInstanceToken` API to create the instance access credential. For more information, see CreateInstanceToken API Documentation.



## Subsequent Operations
Refer to [Logging in to the TCR instance](https://intl.cloud.tencent.com/document/product/1051/35484) to log in to the TCR Enterprise Edition instance.


