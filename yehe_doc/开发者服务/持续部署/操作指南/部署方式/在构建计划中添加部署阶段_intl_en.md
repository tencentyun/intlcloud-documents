Before you trigger deployment in Continuous Deployment, go to the **CODING-CD Console** to associate your application with the project.

![](https://qcloudimg.tencent-cloud.cn/raw/5f98a1ddeea6c8c9ee5cc842e1df8a1a.png)

You can add a deployment stage to a build plan in either of the following ways:

- Directly use a build plan template
- Add a deployment stage to an existing build plan

## Use Build Plan Template

>! Associate the cloud account for the relevant cluster in the CODING-CD Console. For more information, see [Cloud Accounts](https://intl.cloud.tencent.com/document/product/1137/45451).

Click **Continuous Deployment** in the product section on the left, and then click "Create Build Plan" in the upper-right corner. Under the **Deployment** category, select the **Push to Kubernetes** template.
![](https://qcloudimg.tencent-cloud.cn/raw/dcbf168e39468d56bf3237724ed19390.png)

Select the corresponding artifact repository, remote cluster address, and other information as instructed. When you are done, select "Trigger build after creation".

![](https://qcloudimg.tencent-cloud.cn/raw/604104bb68dd05d7da03094200da9651.png)

After the setup is complete, you can run the continuous build plan to automate the release process.

## Add Deployment Stage

Click **Build Plan** > **Process Configuration** to add a deployment stage by using an editor or entering a command.

### Graphical editor

Add a **deployment** stage in the existing build plan settings, and then fill in the image URL, cluster, namespace, etc.
![](https://qcloudimg.tencent-cloud.cn/raw/6294aaeb4bcc0046443ccbabcb377c71.png)

### Jenkinsfile
<dx-codeblock>
:::  groovy
stage('Push to CODING Docker artifact repository') {
      steps {
        script {
          docker.withRegistry(
            "${env.CCI_CURRENT_WEB_PROTOCOL}://${env.CODING_DOCKER_REG_HOST}",
            "${env.CODING_ARTIFACTS_CREDENTIALS_ID}"
          ) }
            docker.image("${CODING_DOCKER_IMAGE_NAME}:${env.DOCKER_IMAGE_VERSION}").push()
          
        }
     
      }
:::
</dx-codeblock>
