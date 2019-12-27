## Overview
When you create a service, an image is used to specify the process of the container in the pod. By default, the image runs a default command. To run a specific command or to rewrite the default value of the image, the following three settings need to be used:

- Working directory (workingDir): This specifies the current working directory.
- Run command (command): This controls the actual command run by the image.
- Command argument (args): This is the parameter passed to the running command.

## Working Directory
Specify the current working directory. Create one if it does not exist. If no directory is specified, you can use the default value during the running of container. If workdir is not specified in the image or through the console, the `workdir` is `/` by default.

## How Does the Container Execute the Command and Parameter?
For more information on how to adapt `docker run` command to Tencent Cloud TKE, please see [Details](https://intl.cloud.tencent.com/document/product/457/9883).
 
Docker image has the metadata for storing the image information. If you do not specify any command or parameter for the container, the container may run the default command and parameter used in the creation of the image. By default, they are `Entrypoint` and `CMD` in Docker. For more information, please see [Entrypoint](https://docs.docker.com/engine/reference/builder/#/entrypoint) and [CMD](https://docs.docker.com/engine/reference/builder/#/cmd) from Docker.
If you specify a command and a parameter for the container when creating the service, the default commands `Entrypoint` and `CMD` generated in the creation of the image will be overwritten according to the following rules:

| Image Entrypoint | Image CMD | Container's run command | Container's run parameter | Final run |
| :-------- | :--------| :------ | :-------- | :------ |
| [ls] | [/home]| Not set | Not set |[ls / home] |
| [ls] | [/home]| [cd] | Not set |                            [cd] |
| [ls] | [/home]| Not set |[/data] |[ls / data] |
| [ls] | [/home]| [cd] |[/data] |[cd / data] |

>
>- Docker entrypoint corresponds to the command on TKE console, and the parameter CMD of Docker run corresponds to the parameter on TKE console. If multiple parameters exist, enter them in the parameter field of TKE with each parameter per line.
>- To learn more about configuring container run command and parameter examples in TKE console, please see [Command and Args](https://intl.cloud.tencent.com/document/product/457/9883).
