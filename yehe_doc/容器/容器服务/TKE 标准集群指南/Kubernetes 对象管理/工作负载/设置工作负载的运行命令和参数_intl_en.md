## Overview

When you create a workload, an image is used to specify the process of the container in the pod. By default, the image runs a default command. To run a specific command or to rewrite the default values of the image, you need to use the following three settings:
- Working directory (workingDir): this specifies the current working directory.
- Run command (command): this controls the actual command run by the image.
- Command argument (args): this is the parameter passed to the running command.

## Working Directory

WorkingDir specifies the current working directory. If it does not exist, a working directory will be automatically created. If this parameter is not specified, the default value of the container runtime will be used. If WORKDIR is not specified in the image or console, the default value of workingDir will be “/”.

## Command and Parameter Usage

For information on how to adapt the docker run command to Tencent Cloud TKE, see [docker run Parameter Adaptation](https://intl.cloud.tencent.com/document/product/457/9883).
 
Docker images contain metadata related to image information storage. If you do not specify any command or parameter for the container, the container may run the default command and parameter used when the image is created. By default, they are `Entrypoint` and `CMD` in Docker. For more information, see [Entrypoint](https://docs.docker.com/engine/reference/builder/#/entrypoint) and [CMD](https://docs.docker.com/engine/reference/builder/#/cmd) from Docker.
If you enter the run commands and parameters for the container when creating a service, TKE will override the default commands (i.e., "Entrypoint" and "CMD") when the image is created. The rules are as follows:

| Image Entrypoint | Image CMD | Container's run command | Container's run parameter | Final run |
| :-------- | :--------| :------ | :-------- | :------ |
| [ls] | [/home]| Not set | Not set |[ls / home] |
| [ls] | [/home]| [cd] | Not set | [cd] |
| [ls] | [/home]| Not set |[/data] |[ls / data] |
| [ls] | [/home]| [cd] |[/data] |[cd / data] |

> !
>- Docker entrypoint corresponds to the run command on the TKE console, and the parameter CMD of Docker run corresponds to the run parameter on the TKE console. If multiple parameters exist, enter them in the parameter field of TKE with each parameter on its own row.
>- For examples on how to use the [TKE console](https://console.cloud.tencent.com/tke2) to set the running command and parameter for a container, see [Commands and Args](https://intl.cloud.tencent.com/document/product/457/9883#command-.E5.92.8C-args). 
