This document describes the permission control in CODING Continuous Deployment (CODING-CD).

## Prerequisites

You must activate the CODING DevOps service for your Tencent Cloud account before you can use CODING Project Management (CODING-PM). 

## Open Admin Settings

1. Log in to the CODING Console and click the team domain name to go to CODING.
2. Hover over your profile photo in the upper-right corner to open the Team Management page through the dropdown list. Then, click "Permission Configuration" to open the Admin page.

## Permission Control

By default, the roles and permissions in CODING-CD are as follows:

- Team owner: Has permission to manage deployment.
- Team admin: Has permission to manage deployment.
- Ordinary team member: Has no permission to manage deployment.

We recommend that you create an independent **Ops** role in your team, grant it permission to **manage deployment**, and specify a team member to take on the role to implement the principle of least privilege. Set an **Ops** role as shown below. You can click **Add User Group** to set more roles.
![](https://qcloudimg.tencent-cloud.cn/raw/61e2adbcddb2b06cdb39b5e09a0e58be.png)

We recommend that you divide all the operations during continuous deployment into two categories and assign them to two roles respectively:

- Ops: Configures the continuous deployment process (including the application, release process, and approval process)
- Developer: Releases an application by submitting a release order (Specifically, submits a release order, waits for approval, and views the release process)

