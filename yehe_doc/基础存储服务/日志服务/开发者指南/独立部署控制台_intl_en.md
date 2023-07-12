This document describes how to open up CLS's log search and query, monitoring alarm, and dashboard capabilities to others in an independently deployed console. This is a quick and easy way to eliminate the development workload and costs for managing multiple CAM accounts.


## Independently Deployed Console

The independently deployed console doesn't require development or logging in to a Tencent Cloud account to use CLS. It has weak permission management and security capabilities and provides only simple password authentication though. We recommend you use it in the private network.

| Usage         | Supported Features        | Free from Tencent Cloud Account Login      | Development Workload      | Account Permission Management       | Login State Conflict |
| ----------------- | ----------------- | --------------------------- | ---------------------- | ------------------------- | -------------------------- |
| [Tencent Cloud console](https://console.cloud.tencent.com/cls/overview) | All CLS features                           | No                                                   | None                                       | Tencent Cloud CAM         | None                          |
| Iframe-embedded console - general embedding | All CLS features                           | Yes, with iframe embedded into the enterprise Ops system for login through the authentication system | Light, where frontend iframe embedding is required                   | Enterprise authentication system              | Yes                     |
| Iframe-embedded console - SDK embedding | CLS features of log search and analysis and dashboard view     | Yes, with iframe embedded into the enterprise Ops system for login through the authentication system | Heavy, where frontend iframe embedding and backend access layer forwarding are required | Enterprise authentication system              | No                   |
| [Independently deployed console](https://www.tencentcloud.com/document/product/614/50280)                                           | All CLS features                           | Yes, with independent deployment and password-based or password-free login                   | None                                       | None or password authentication               | Yes                     |
| [Grafana plugin](https://intl.cloud.tencent.com/document/product/614/39592) | Grafana's dashboard features excluding alarming | Yes, with Grafana for data access                                | None                                       | Grafana's permission management system | No                   |


## Using the Independently Deployed Console

CLS provides the image of the independently deployed console in TKE's public image repository, which can be pulled from the [TKE](https://console.cloud.tencent.com/tke2) console for use.

### Prerequisites

The following takes image deployment in a TKE general cluster as an example, which requires an available cluster. If there are no clusters, create one as instructed in [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637) or create a container instance as instructed in [Creating a Container Instance](https://intl.cloud.tencent.com/document/product/457/47857) for direct deployment.

### Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click the name/ID of an available cluster in the cluster list to enter the cluster management page.

2. On the left sidebar, select **Workload** > **Deployment** and click **Create**.

3. On the deployment creation page, configure the following items and use the default values for others.

 - Image: Click **Select Image** > **Public Image** and search for and select the "cls_iframe" image.
 - Image Tag: Select **Latest image tag**.
 - Environment variable:
 <table>
<thead>
<tr><th>Environment Variable</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td>SecretId</td><td>Get it from the <a href="https://console.cloud.tencent.com/cam/capi">CAM</a> console.</td></tr>
<tr><td>SecretKey</td><td>Get it from the <a href="https://console.cloud.tencent.com/cam/capi">CAM</a> console.</td></tr>
<tr><td>RoleArn</td><td><a href="https://intl.cloud.tencent.com/document/product/1150/49456">AssumeRole</a> API request parameter. To get the role resource description, go to the <a href="https://console.cloud.tencent.com/cam/role">CAM</a> console and click the role name. We recommend you use CLS's read-only role.</br>If there is no such role, create one with <b>CLS's read-only access permission</b> for the Tencent Cloud root account as instructed in <a href="https://intl.cloud.tencent.com/document/product/598/19381">Creating Role</a>.</td></tr>
<tr><td>password</td><td>Enter the password to access the console with the configured identity.</td></tr>
</tbody></table>
 - Port Mapping: Set **Target Port** and **Port** to **3000**.
>? In the example, **LoadBalancer (public network)** is selected. We recommend you select **LoadBalancer (private network)**, which is more secure in actual business operations.
>
5. Click **Create Workload** to complete the process.
6. Click **Services and Routes** to view the LB access address bound to the workload.

7. Copy the LB IP address, add port **3000**, and enter the password in the browser to access the deployed CLS console.


