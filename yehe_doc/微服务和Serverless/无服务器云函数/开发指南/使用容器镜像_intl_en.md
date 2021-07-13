## Overview


The SCF container image feature has been launched, so you can use images for development. This document describes how to install an image and use it for development.




## Prerequisites

[Docker](https://docs.docker.com/install/) has been installed in the development environment.


## Directions

### Getting image

The SCF image is based on CentOS 7.7.1908 and available as a [public image](https://console.cloud.tencent.com/tke2/registry/qcloud) in TKE. You can search for `scf-repo` on the public image page to [view the image information](https://console.cloud.tencent.com/tke2/registry/qcloud/default/detail/tag?rid=8&reponame=scf-repo%252Fscf-runtimes-image).

1. Run the following command to pull the image:
```bash
# Pull the SCF source image
docker pull ccr.ccs.tencentyun.com/scf-repo/scf-runtimes-image:latest
```
	>! If the command prompts a permission error and cannot be executed normally, add `sudo` before the command and try again.
2. You can view the runtime contained in the current image in the `/scf/lang/` directory.
As the SCF source image contains all runtimes, it is relatively large. Please refer to the following table and choose a runtime image according to your needs.
<table>
<thead>
<tr>
<th>Runtime</th>
<th>Address</th>
</tr>
</thead>
<tbody><tr>
<td>SCF</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/scf-runtimes-image:latest</code></td>
</tr>
<tr>
<td>Go 1.8</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-go1:latest</code></td>
</tr>
<tr>
<td>Python 2.7</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-python2:latest</code></td>
</tr>
<tr>
<td>Python 3.6</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-python3:latest</code></td>
</tr>
<tr>
<td>PHP 5.6</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-php5:latest</code></td>
</tr>
<tr>
<td>PHP 7.2</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-php7:latest</code></td>
</tr>
<tr>
<td>Java 8</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-java8:latest</code></td>
</tr>
<tr>
<td>Node.js 6.10</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-node6:latest</code></td>
</tr>
<tr>
<td>Node.js 8.9</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-node8:latest</code></td>
</tr>
<tr>
<td>Node.js 10.15</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-node10:latest</code></td>
</tr>
<tr>
<td>Node.js 12.16</td>
<td><code>ccr.ccs.tencentyun.com/scf-repo/runtime-node12:latest</code></td>
</tr>
</tbody></table>
3. This document uses the `scf:python3` tag as an example. Run the following command to retag the image:
```bash
docker pull ccr.ccs.tencentyun.com/scf-repo/runtime-python3:latest
# Run this command to find the IMAGE ID and copy it
docker images
# docker tag IMAGE_ID REPOSITORY:TAG
docker tag 0729ecc15d37 scf:python3
```
 The execution result is as shown below:
![image-20201204112659373](https://main.qcloudimg.com/raw/5f0fef9599a89115b589cbb0d620b836.png)
>?If you don't want to tag the image, you need to replace `scf:python3` in the sample with `ccr.ccs.tencentyun.com/scf-repo/runtime-python3:latest`.


### Using image for dependency installation

This document uses the NodeJieba dependency in the Node.js 12 environment as an example to describe how to install dependencies with an image.

#### Getting Node.js 12 image

Run the following command to pull the image:
```bash
docker pull ccr.ccs.tencentyun.com/scf-repo/runtime-node12:latest
# Run this command to find the IMAGE ID and copy it
docker images
docker tag d64a665357b6 scf:node12
```

#### Starting container and mounting directory

Run the following command to start the container and mount the local directory to a directory in the container (if the directory does not exist, it will be created automatically). This document uses mounting the `/path/to/your_project` directory to the `/tmp/your_project` directory in the container as an example.
```bash
docker run -it -v /path/to/your_project:/tmp/your_project scf:node12 /bin/bash
```

#### Installing dependencies in container

1. After starting the container, run the `cd` command to enter the directory in the container. Then, run the `npm` command to install NodeJieba in this directory as shown below:
```plaintext
cd /tmp/your_project
npm install nodejieba --save
```
2. The dependency will be installed in the local `/path/to/your_project` directory. Run the `exit` command to exit the container as shown below:
```bash
# Exit the container
exit
```

Following the above steps, you can install dependencies through the container image and then redeploy the code to SCF. For the Node.js language, [online dependency installation](https://intl.cloud.tencent.com/document/product/583/38105) is also supported, so that dependencies will be automatically installed upon upload.

### Using image for development

This document uses Python 3.6 as an example to describe how to use a container for development and testing.


#### Getting Python 3.6 image

Run the following command to pull the image:
```bash
docker pull ccr.ccs.tencentyun.com/scf-repo/runtime-python3:latest
# Run this command to find the IMAGE ID and copy it
docker images
docker tag d64a665357b6 scf:python3
```

#### Starting container and mounting directory

1. Run the following command to start the container and mount the local project directory to a directory in the container (if the directory does not exist, it will be created automatically):
```bash
docker run -it -v /path/to/your_project:/tmp/your_project scf:node12 /bin/bash
```
2. Run the `docker exec` command to enter the container for development as shown below:
```bash
docker ps
# Get the CONTAINER ID
docker exec -it CONTAINER_ID /bin/bash
```

#### Saving image

Run the following command to submit changes to the local image for subsequent use:

```bash
# Get the container ID
docker ps 
# Save the image locally
# docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
docker commit db47b8e66e64 scf:myimage
```
