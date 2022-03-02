This document describes how to store Docker artifacts in CODING-AR for centralized artifact management and version control. The following sections introduce how to create an image, configure authentication, and pull and push artifacts.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -   Install Docker.
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select Docker as the repository type.

## Create an Image (Optional) [](id:image)
This section describes how to quickly create a demo Docker image. You can skip this section if you are familiar with Docker images.

### Method 1: create an image locally
1.  In a local directory, create a Dockerfile with the following content:
```dockerfile
FROM coding-public-docker.pkg.coding.net/public/docker/nodejs:12
```
2.  Run the following command in the directory to build an image.
```bash
docker build -t hello-world .
```
The image is created with a default tag `hello-world:latest`. Refer to the [Docker documentation](https://docs.docker.com/engine/reference/commandline/tag/) for customized tags in the format of `<Image Name>:<Version>`.
![](https://main.qcloudimg.com/raw/db15803b6b67d56201f579ad8ef7c6cc.png)

### Method 2: pull an image from Docker Hub
1.  Run the following command in the terminal to pull an image.
```bash
docker pull hello-world
```
2.  Run the following command to view the images pulled.
```bash
docker images
```

## Configure Authentication Information

After creating a local artifact, you can push it to the remote repository. Before the push, you need to locally configure the authentication information of the remote repository.

### Access token

We recommend you use an **access token** to generate the authentication configuration.

1.  Click **Operation Guide** on the repository page.

2.  Enter the login password/two-step verification code and then copy the command generated.
![](https://qcloudimg.tencent-cloud.cn/raw/8ee278d3d4cffb7cda87b95cd9185dfe.png)
3.  Paste and run the command in the local Docker environment to complete the authentication.
![](https://main.qcloudimg.com/raw/d9c972a2b716b8074f49a6c68d599ec2.png)

## Push an Image

The following commands are for reference only. Use the commands generated in your project.

1.  Tag the `hello-world` image pulled in the [above section](#image).
<dx-codeblock>
:::  bash
docker tag hello-world straybirds-docker.pkg.coding.net/coding-demo/coding-demo/hello-world
:::
</dx-codeblock>
2.  Push your docker image to CODING-AR.
<dx-codeblock>
:::  bash
docker push straybirds-docker.pkg.coding.net/coding-demo/coding-demo/hello-world
:::
</dx-codeblock>

The following information will be displayed after the image is pushed successfully.
![](https://main.qcloudimg.com/raw/6ad8f7d415a764b22331063f9e74806d.png)
All the commands described above are displayed in the operation guide. Replace the variables and then run the commands.
![](https://qcloudimg.tencent-cloud.cn/raw/45e2f35e1d9a43718a52ea234acf17f1.png)


## View an Image

After the image is pushed, the activity will be shown in **Project Overview**.

You can see the **hello-world** image in the artifact list.
![](https://qcloudimg.tencent-cloud.cn/raw/3418f0b6af90f489049902cfa6eefdc8.png)
Click the image name to view its information, including overview, guide, properties, and version list.
![](https://qcloudimg.tencent-cloud.cn/raw/49af34e9f4db688512ab399fa2f2d165.png)

## Pull an Image

Run `docker pull` to pull a Docker image from CODING-AR. You can use the command generated in the **Guide**.
![](https://qcloudimg.tencent-cloud.cn/raw/1bca64fbc230f04a28ec25840cbfbcd9.png)
The following information will be displayed after the image is pulled successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/1bca64fbc230f04a28ec25840cbfbcd9.png)