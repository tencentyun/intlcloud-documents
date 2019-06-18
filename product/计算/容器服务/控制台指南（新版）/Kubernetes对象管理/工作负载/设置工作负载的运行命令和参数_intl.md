## Overview

When you create a workload, you can typically specify the processes run by the container in the Pod through an image. By default, the image will run the default command. If you want to run a specific command or override the default value of the image, you need to use the following three settings:
- Working directory (workingDir): This specifies the current working directory.
- Run command (command): This controls the actual command run by the image.
- Command argument ( args ): This is the parameter passed to the running command.

## Working Directory Description

WorkingDir specifies the current working directory. If no directory exists, the system will create one automatically. If this is not specified, the default value of the container runtime will be used. If no workdir is specified in the image and the console, the workdir will default to "/".

## Command and Parameter Usage

Click [here](https://cloud.tencent.com/document/product/457/9883) to learn how to adapt the docker run command to TKE.
 
A Docker image has relevant metadata that stores the image information. If no run commands and parameters are provided, the container will run the default commands and parameters provided during image creation. The fields natively defined by Docker are "Entrypoint" and "CMD". For more information, see Docker's [Entrypoint description](https://docs.docker.com/engine/reference/builder/#/entrypoint) and [CMD description](https://docs.docker.com/engine/reference/builder/#/cmd).
If you enter the run commands and parameters for the container when creating a service, TKE will override the default commands (i.e., "Entrypoint" and "CMD") when the image is built. The rules are as follows:

| Image Entrypoint | Image CMD | Container's run command | Container's run parameter | Final run |
| :-------- | :--------| :------ | :-------- | :------ |
| [ls]   | [/home]|  Not set  | Not set    |[ls / home]  |
| [ls]   | [/home]|  [cd]  | Not set    |	[cd]        |
| [ls]   | [/home]|  Set  |[/data] |[ls / data]  |
| [ls]   | [/home]|  [cd]  |[/data] |[cd / data]  |

 Docker's Entrypoint corresponds to the run command in the TKE console; while the CMD parameter of Docker run corresponds to the run parameter in the TKE console. If there are multiple run parameters, you need to enter them in TKE, one parameter per line.
