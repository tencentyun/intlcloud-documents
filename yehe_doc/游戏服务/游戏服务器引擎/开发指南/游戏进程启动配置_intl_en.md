## Launching game process as a root user or user_00 in Linux environment
In Linux environment, the game process should be launched by a root user by default. If you want to launch the game process as a non-root user, please do the following:

1. Add the file `gse.yaml` to the root directory of the game’s asset package, which means the decompressed file path will be `/local/game/gse.yaml` on the game server fleet instance;  
2. The content of the file `gse.yaml` is shown below, indicating that user_00 is added to the `users` user group. You cannot configure other users and user groups currently;
```
User: user_00:users
```
When the file `gse.yaml` is added to the asset package, GSE will launch the game process with `user_00:users` and set the users and user groups of all files under `/local/game` as `user_00:users`.

	See below for the example:
![](https://main.qcloudimg.com/raw/c39326e6328dac93964f6d3e6da5efad.png)

## Executing `install.sh` before launching game process in Linux environment
Before a game process is launched, you may need to install some software or configure some environment variables on the CVM instance with the following steps:

1. Create the `install.sh` script and write the operations to be conducted before launching the game process in this script;  
2. Add the file `install.sh` under the root directory of the game’s asset package, which means the decompressed path will be `/local/game/install.sh` on the game server fleet instance.

## Launch configuration for Java game process
In Linux environment, a command like `java -jar XXXX.jar` can be used to launch Java programs. The following configurations are required to ensure the Java game process is successfully launched:

1. Write the `install.sh` script

		#!/bin/bash

		# Install the JDK 1.8 environment - y indicates answer yes for all questions
		yum install java-1.8.0-openjdk.x86_64 -y
		# Put the java command under `/local/game` with a soft link
		ln -s /usr/bin/java /local/game/java

2. Put `install.sh` script under the root directory of the game’s asset package, which means the decompressed path will be `/local/game/install.sh` on the game server fleet instance.
3. When creating the game server fleet, enter `/local/game/java` as the launch path, and enter `-jar jar package specified by user` as the launch parameter.
![](https://main.qcloudimg.com/raw/4bd297141914431440f69cb4d1393aee.png)

4. After the game process is successfully launched, the content of the path `/local/game` is shown below:
![](https://main.qcloudimg.com/raw/637aebe468e921d845baeb88fa21688c.png)




