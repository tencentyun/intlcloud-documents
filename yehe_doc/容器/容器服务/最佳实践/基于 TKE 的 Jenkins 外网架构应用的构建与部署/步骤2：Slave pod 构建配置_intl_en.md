This step describes how to build a slave pod in Jenkins by creating a task and configuring task parameters.

### Creating a Task
1. Log in to the Jenkins backend and click **New Task** or **Create a Task**.
2. On the "Create a Task" page, configure the basic information of the task.
 - **Enter a task name**: enter a custom name. This document uses `test` as an example.
 - **Type**: select **Build a freestyle software project**.
3. Click **OK** to go to the task parameter configuration page.
4. Configure the basic information on the task parameter configuration page.
 - **Description**: enter custom task information. This document uses `slave pod test` as an example.
 - **Parameterize the building process**: check this option and choose **Add Parameter** > **Git Parameter**.


### Configuring Task Parameters
1. On the "Git Parameter" panel, configure the following parameters.
The following describes the main parameters. For other parameters, simply keep them as their defaults:
 - **Name**: enter `mbranch`, which can be used to match and obtain a branch.
 - **Parameter Type**: select **Branch or Tag**.
2. Choose **Add Parameters** > **Extended Choice Parameters**. On the "Extended Choice Parameters" panel that appears, configure the following parameters, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8287b6baae8da7bb181b96c6ab5bedf5.png)
The following describes the main parameters. For other parameters, simply keep them as their defaults:
  - **Name**: enter `name`, which can be used to obtain the image name.
  - **Basic Parameter Types**: select this option.
  - **Parameter Type**: select **Check Boxes**.
  - **Value**: select this option and enter a custom image name. This value will be passed to the `name` variable. This document uses `nginx,php` as an example.
3. Choose **Add Parameters** > **Extended Choice Parameters**. On the "Extended Choice Parameters" panel, configure the following parameters, as shown in the following figure:
![](https://main.qcloudimg.com/raw/c9a5bb698e624bb98d0a2b00ff93d749.png)
The following describes the main parameters. For other parameters, simply keep them as their defaults:
 - **Name**: enter `version`, which can be used to obtain the image tag variable.
 - **Basic Parameter Types**: select this option.
 - **Parameter Type**: select **Text Box** to obtain the image value in text format and pass it to the `version` variable.
4. Check **Restrict the running node of the project**. For the tag expression, enter the pod tag `jnlp-agent` set in the [Configuring the slave pod template](https://intl.cloud.tencent.com/document/product/457/34867#PodTemplates) step.

### Configuring Source Code Management
In the "Source Code Management" area, select **Git** and configure the following information.
- **Repositories**:
  - **Repository URL**: enter your GitLab address, such as `https://gitlab.com/user-name/demo.git`.
  - **Credentials**: select the authentication credential created in the [Adding GitLab authentication](https://intl.cloud.tencent.com/document/product/457/34867#addGitlab) step.
- **Branches to build**:
  - **Specified branch (any if it is empty)**: enter `$mbranch`, which is used to dynamically obtain the branch, and its value corresponds to the value of `mbranch` defined in "Git Parameter".


### Configuring the Shell Packaging Script
1. In the "Building" area, choose **Add Building Step** > **Run Shell**.
2. Copy and paste the following script content into the "Command" entry box. Then, click **Save**.
> 
>- In this script, information such as the GitLab address, TKE image address, and username and password of the image repository are for example only. In actual cases, replace them based on your needs.
>- Be sure to build the package based on the source code of Docker build. In addition, the working directory `/home/Jenkins/agent` must be consistent with the working directory of the [container template](https://intl.cloud.tencent.com/document/product/457/34867#ContainerTemplate) in "Container List".
>
```
	echo "GitLab address: https://gitlab.com/[user]/[project-name]].git" 
	echo "Selected branch (image): "$mbranch", set branch (image) version: "$version"
	echo "TKE image address: hkccr.ccs.tencentyun.com/[namespace]/[ImageName]"

	echo "1. Log in to the TKE image repository"
	docker login --username=[username] -p [password] hkccr.ccs.tencentyun.com

	echo "2. Build the package based on the source code of Docker build:"
	cd /home/Jenkins/agent/workspace/[project-name] && docker build -t $name:$version

	echo "3. Upload the Docker image to the TKE repository:"
	docker tag $name:$version hkccr.ccs.tencentyun.com/[namespace]/[ImageName]:$name-$version
	docker push hkccr.ccs.tencentyun.com/[namespace]/[ImageName]:$name-$version
```
The script provides the following features:
    - Obtain the selected branch, image name, and image tag.
    - Publish the docker image combined and built with the code in the TKE image repository.

### Subsequent Operations
You have now successfully built the slave pod. Next, go to [Building Tests](https://intl.cloud.tencent.com/document/product/457/34869) to publish and verify images.
