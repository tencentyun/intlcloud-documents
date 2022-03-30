This document describes the trigger configuration of a deployment pipeline in CODING Continuous Deployment (CODING-CD).

## Prerequisites

You must activate the CODING DevOps service for your Tencent Cloud account before you can use CODING Project Management (CODING-PM). 

## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING page.
2. On the Workspace homepage, click <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" style ="margin:0" data-nonescope="true"> on the left to go to the CODING-CD Console.

## Function Overview

CODING-CD Console supports various auto trigger conditions to match the pipelines in CODING, including Docker Repository Trigger, TCR Personal Repository Trigger, TCR Enterprise Repository Trigger, and Git Repository Trigger.

![](https://help-assets.codehub.cn/enterprise/20220308101701.png)

## Docker Repository Trigger

Docker Repository Trigger can be configured to listen on the updates of artifact repositories. Any image updates will trigger the CD pipeline automatically.

![](https://qcloudimg.tencent-cloud.cn/raw/b127696c9ac39ae0b2735159d0fb4f93.png)

## Git Repository Trigger

Three types of Git repositories are supported: CODING-CR, GitHub, and GitLab.

| Field           | Description                                                  |
| -------------- | ----------------------------------------------------- |
| Repository Type       | Three types of Git repositories are supported: CODING-CR, GitHub, and GitLab. |
| Project           | Lists all the projects that the logged-in account joins                            |
| Repository           | Lists all the code repositories in the project                              |
| Branch or Tag Rule | Regular expressions are supported. Null or `.*` indicates no restrictions on branches or tags.    |

### CODING Code Repositories

Configure the "cd-demo" code repository in the "cd-demo" project as a trigger. The branch or tag rule "release.*" means that the deployment pipeline is triggered only for branches or tags prefixed with "release" in their name.

![](https://help-assets.codehub.cn/enterprise/20220308102012.png)

[](id:Github)
### GitHub

To support a GitHub code repository, follow the steps below to associate the repository in the project settings:
1. Go to the project overview page，Click **Repository**.
![](https://help-assets.codehub.cn/enterprise/20220308102156.png)
2. Click the Associated Code Warehouse button in the upper right corner.
![](https://help-assets.codehub.cn/enterprise/20220308102156.png)
3. Use OAuth to jump to the GitHub associated account and select the code repository under the name.![](https://help-assets.codehub.cn/enterprise/20220308102254.png)
4. After the connection completed, Return to **Basic configuration** > **Execution Options**，Choose **GitHub** Repository Type。
![](https://help-assets.codehub.cn/enterprise/20220308103353.png)

### GitLab

After you associate your GitLab account (see [GitHub](#Github) for specific steps), click **Basic Configurations** > **Execution Options** to select the **GitLab** repository type.

![](https://help-assets.codehub.cn/enterprise/20220308103502.png)

### Webhook trigger

If you select the webhook trigger, a globally unique trigger URL will be generated. `Payload Constraints` defines the parameters that the `payload` request must provide. Regular expressions are supported. Null or `.*` indicates no restrictions on the key value.

Payload Constraints: If you need to use a specific payload to trigger a webhook, you can add a `key/value` pair in the `Payload Constraints` section. When a pipeline receives a webhook request, the `payload` content will be validated. The `value` supports regular expressions.

![](https://help-assets.codehub.cn/enterprise/20220308103712.png)

**Sample scenario**: A pipeline's webhook URL is accessible from the public network, but the pipeline can be triggered only if correct authentication credentials are provided.

The pipeline will be triggered for the following `payload` request:

```shell
curl --location --request POST 'http://codingcorp.coding.com/api/cd/webhooks/webhook/ba2e9f00-6445-11ea-88b5-a9bc004f5e0f' \
--header 'Content-Type: application/json' \
--data-raw '{"secret": "faiM4&KqJTTuEy8J"}'
```

## Scheduled Trigger

For example, to trigger a pipeline at 8:00 pm every day:

![](https://help-assets.codehub.cn/enterprise/20220308104032.png)
