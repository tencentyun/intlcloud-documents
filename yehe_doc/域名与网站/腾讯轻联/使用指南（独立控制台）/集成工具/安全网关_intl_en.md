## Overview

A security gateway is a proxy system designed to integrate and interconnect iPaaS and your private network service. You can use it when you want to integrate your private network service through iPaaS (deployed in the public cloud) but your private network service is inaccessible over the public network.

A security gateway consists of the Server and the Agent:
- The Server is deployed in the private network of iPaaS, and you don't need to care about it.
- The Agent is deployed in your private network. You can deploy multiple Agents in different regions or for different services and use the security gateway for forwarding data to implement data interaction between iPaaS and your private network service.




## Configuring the Agent
[](id:agent)
### Step 1. Download the Agent

1. Log in to the [iPaaS console](https://ipaas.cloud.tencent.com/gateway) and select **Security gateway**.
2. Click **Create** and upload a public key as instructed in [Generating Public and Private Keys](#certificate).
3. Configure the Agent IP allowlist and private network service, confirm the information, and click **Save**.
4. Click **Download Agent** in the security gateway list.
- The directory structure of the decompressed Agent package is as detailed below:
  - The `bin` directory contains the executable programs of the Agent, which are in sub-directories `Linux`, `Windows`, and `Mac` for use on different operating systems.
  - The `configs` directory contains the configurations required for Agent execution. In `configs`:
    - The `client` directory stores the configurations such as key required for Agent TLS communication. Such configurations correspond to those of the Server. Files in this directory **cannot be deleted or modified**.
    - The `secret` directory stores the private key for the Agent to connect to the Server. For more information on how to generate a private key, see [Generating Public and Private Keys](#certificate).
    - The `config.yaml` file contains configurations that must be depended on for Agent execution.
    - The `logger_config.yaml` file contains the log configuration for Agent execution. **You can modify the log level and log backup policy**.
  - The `log` directory stores logs generated during Agent execution.
  - The `scripts` directory stores the Agent startup/stop scripts (`start.sh/stop.sh`).

### Step 2. Configure Agent logs

You can modify the `logger_config.yaml` file in the `ipaas-private-cloud-agent/configs` directory of the Agent to modify the gateway log level and log backup policy as needed. The meaning of each parameter has been detailed in the file.

### Step 3. Start the Agent

Run the startup script for your operating system to start the Agent:

<dx-tabs>
::: macOS
Run the following command to start the Agent:
<dx-codeblock>
:::  plaintext
./ipaas-private-cloud-agent/scripts/mac/start.sh
:::
</dx-codeblock>
:::
::: Linux
Run the following command to start the Agent:
<dx-codeblock>
:::  plaintext
./ipaas-private-cloud-agent/scripts/linux/start.sh
:::
</dx-codeblock>
:::
::: Windows
Run the following command to start the Agent:
<dx-codeblock>
:::  plaintext
./ipaas-private-cloud-agent/scripts/windows/start.bat
:::
</dx-codeblock>
:::
</dx-tabs>



### Relevant commands

Below are the commands for stopping the Agent on different operating systems:

<dx-tabs>
::: macOS
Run the following command to stop the Agent:
<dx-codeblock>
:::  plaintext
./ipaas-private-cloud-agent/scripts/stop.sh
:::
</dx-codeblock>
:::
::: Linux
Run the following command to stop the Agent:
<dx-codeblock>
:::  plaintext
./ipaas-private-cloud-agent/scripts/linux/stop.sh
:::
</dx-codeblock>
:::
::: Windows
Run the following command to stop the Agent:
<dx-codeblock>
:::  plaintext
./ipaas-private-cloud-agent/scripts/windows/stop.bat
:::
</dx-codeblock>
:::
</dx-tabs>



[](id:certificate)
## Generating Public and Private Keys

### Step 1. Check the OpenSSL version

Run the following command to check whether OpenSSL has been installed:
```plaintext
openssl version
```

If the OpenSSL version information can be output normally after the command is executed, OpenSSL has been installed and you can skip step 2; otherwise, install OpenSSL as instructed below.



### Step 2. Install OpenSSL

The OpenSSL installation method varies by operating system as follows:


<dx-tabs>
::: macOS
Run the following command to install OpenSSL:
<dx-codeblock>
:::  plaintext
brew install openssl
:::
</dx-codeblock>
:::
::: Linux
Run the following command to install OpenSSL:
**Centos**
<dx-codeblock>
:::  plaintext
  yum install openssl
:::
</dx-codeblock>**Ubuntu**
<dx-codeblock>
:::  plaintext
  sudo apt-get install openssl 
  sudo apt-get install libssl-dev
:::
</dx-codeblock>
:::
::: Windows
1. Download the installation package of [OpenSSL](http://slproweb.com/products/Win32OpenSSL.html) based on your operating system version. For example, for a 64-bit system, select the version as shown below (the EXE file on Light Edition):
    ![](https://main.qcloudimg.com/raw/fd2eb3eb9bc733c1e7a814394e6fd7d5.jpg)
2. Double-click the installation package to install OpenSSL. Remember the OpenSSL installation directory such as `C:\Program Files\OpenSSL-Win64`, **which will be used in OpenSSL environment variable configuration**.
3. Configure environment variables. Here, Windows 10 is taken as an example:
 1. Press **Win + R**. In the **Run** pop-up window, enter `sysdm.cpl` and press **Enter** to open the **System Properties** window.
 2. Select **Advanced** > **Environment Variables**.
 3. Double-click **Path**.
 4. Click **New** and enter the path of the `bin` directory in the OpenSSL installation directory to add it to the variables on the left (the `bin` directory path is the installation directory path plus `bin`; for example, if the installation directory path is `C:\Program Files\OpenSSL-Win64`, the `bin` directory path will be `C:\Program Files\OpenSSL-Win64\bin`).
 5. Click **Confirm**.
4. Verify the installation.
 1. Press **Win + R**. In the **Run** pop-up window, enter `cmd` and press **Enter** to open the **System Properties** window.
 2. Run the `openssl version` command. If the OpenSSL version information is displayed, OpenSSL is installed successfully; otherwise, carefully check the installation steps.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xQ7X770_6924f2f52a9e8c393806ada4731c8c41.jpg)
:::
</dx-tabs>





### Step 3. Generate and update public and private keys

1. Run the following command to generate a private key:
```plaintext
openssl genrsa -out private.pem 1024
```
>!Place the generated private key in the `ipaas-private-cloud-agent/configs/secret` directory.
2. Run the following command to generate a public key for the private key. The `public.pem` file generated in the current directory is the public key.
```plaintext
openssl rsa -in private.pem -RSAPublicKey_out -out public.pem
```
3. To generate a new private key, replace the `private.pem` file in the `ipaas-private-cloud-agent/configs/secret` directory.
