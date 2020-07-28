
## Scenario
This document describes how to obtain an access credential for a TCR Enterprise Edition instance in Tencent Container Registry (TCR). To push and pull container images, you must first run the `docker login` command on the access client and enter your username and password (the credential) to log in to the instance.

TCR Enterprise Edition instances support both a long-term access credential and a temporary login command, in which:
- **Long-term access credential**: is permanently valid after being generated. It can be disabled and deleted. Long-term access credentials can be applied in scenarios such as early-stage testing, CICD assembly lines, and container cluster image pull.
>! Please keep the access credential properly after it is generated. If it is lost, disable or delete it promptly.

- **Temporary login command**: is valid for 1 hour and cannot be disabled or terminated after being generated. It can be applied in scenarios such as temporary use and one-time external authorization. Production clusters with high security requirements can also use this method through regular refreshing.



## Prerequisites

Before obtaining an access credential for a TCR Enterprise Edition instance, you must complete the following preparations.
- You have [created a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- To obtain the access credential through an API, you need to obtain the [API key](https://console.cloud.tencent.com/cam/capi) for calling API 3.0.

## Directions

### Obtaining a long-term access credential
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and click **Instance List** in the left sidebar.
2. On the "Instance List" page, choose an instance name to go to the instance details page.
3. Click the **Access Credential** tab and click **Create** above the instance list, as shown in the following figure:
![](https://main.qcloudimg.com/raw/db1354036ef81af4a3d6bc0c76c0c7be.png)
4. In the "Create an Access Credential" window that appears, complete the following steps to obtain an access credential:
   1. In the "Create an access credential" step, enter the purpose of the credential in "Purpose", and click **Next**.
   2. In the "Save the access credential" step, click **Save the access credential** to download the credential. **Store the access credential properly, as it can be saved only once.**
After the creation, you can view the credential on the **Access Credential** tab page. You can also disable or delete the credential now.

### Obtaining a temporary login command
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and click **Instance List** in the left sidebar.
2. On the "Instance List" page, choose an instance name to go to the instance details page.
3. Click the **Access Credential** tab and click **Generate a temporary login command**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/baf31c5b06f33ec14aac5b7a66fb67d6.png)
4. In the "Temporary Login Command" window that appears, click **Copy login command** to obtain the temporary access credential.


## Next Steps
Refer to [Logging in to a Registry Instance](https://intl.cloud.tencent.com/document/product/1051/35484) to log in to the TCR Enterprise Edition instance.
