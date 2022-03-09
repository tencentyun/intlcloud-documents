CODING Continuous Deployment (CODING-CD) allows you to easily integrate upstream and downstream products as workflows. This article describes how to configure a basic automated pipeline for **pushing artifacts through CI task**, **updating artifact repository images**, and **triggering pipeline**.

## Step 1: Associate the application with the project

The **application** in the CODING-CD Console must be associated with the project. Go to the CODING-CD Console, click the **Associate Project** button in the application, and then select the project with the CI configuration.

![](https://qcloudimg.tencent-cloud.cn/raw/8d5cd27f3c6885e1a864bc6a2a0eaf71.png)

## Step 2: Configure CI process

This step pushes artifacts to the artifact repository through CI. You can create a CI process from the CI plan template, or add this stage by writing a Jenkinsfile.

![](https://qcloudimg.tencent-cloud.cn/raw/d35601050dfdc7e8af9160afee073a9b.png)

Add this stage to the CI process:

![](https://qcloudimg.tencent-cloud.cn/raw/79ca2c5bd857ae03b814c3846380909b.png)

**Jenkinsfile**
<dx-codeblock>
:::  groovy
stage('Deploys to the remote Kubernetes cluster') {
      steps {
        cdDeploy([
          deployType: 'PATCH_IMAGE',
          application: "${CCI_CURRENT_TEAM}",
          pipelineName:  "${PROJECT_NAME}-${CCI_JOB_NAME}-${CD_CREDENTIAL_INDEX}",
          image: "${CODING_DOCKER_REG_HOST}/${CODING_DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_VERSION}",
          cloudAccountName: "${CD_ACCOUNT_NAME}",
          namespace: "${CD_NAMESPACE_NAME}",
          manifestType: "${CD_MANIFEST_TYPE}",
          manifestName: "${CD_MANIFEST_NAME}",
          containerName: "${CD_CONTAINER_NAME}",
          credentialId: "${CD_CREDENTIAL_ID}",
          personalAccessToken: "${CD_PERSONAL_ACCESS_TOKEN}",
        ])
      }
    }
:::
</dx-codeblock>



## Step 3: Trigger According to Artifact Image Version

Go to the Application pipeline page in Continuous Deployment, and then click "Enable Trigger" in **Basic Configurations**. If you select "CODING Docker Repository Trigger", the artifact version number in the associated project will be listened on. When artifacts are pushed to the artifact repository through CI, the pipeline will be triggered automatically. If you select "Custom", the artifact repository updates of other projects can be listened on.

In addition to CODING Docker Repository Trigger, you can also select Git Repository Trigger or Scheduled Trigger.

![](https://qcloudimg.tencent-cloud.cn/raw/ac82903f9e8d15ab5a136666d209ff73.png)
