## Overview

When creating a CVM instance, you can configure an instance by specifying **custom data**. During the **first launch** of the CVM, the custom data will be passed into the CVM in text format and be executed. If you purchase multiple CVM instances at a time, the custom data text will be executed on all CVM instances during their first launch.

This document describes how to transfer a shell script when a CVM instance for Linux is started for the first time.

## Notes
- Linux operating systems that support custom data include:
	- 64-bit OSs: CentOS 6.8 and later, Ubuntu Server 14.04.1 LTS and later, and openSUSE 42.3 x86
	- 32-bit OSs: CentOS 6.8 and later
- A command can be executed by passing text only when a CVM instance is launched for the first time.
- The text to be transferred must be Base64-encoded. **Perform encoding in a Linux environment to avoid format incompatibility**.
- Execute the user input as `root`. Therefore, the `sudo` command is not required in the script. The `root` user can access all the files you created. If you need to grant other users with the access permission, modify the permission in the script.
- During launch, executing specified tasks in custom data will increase the amount of time it takes to launch the CVM. We recommend that you wait for a few minutes, and after the tasks are completed, test whether the tasks have been successfully executed.
- In this sample, the shell script must start with `#!` and the path directing to the interpreter of the script to be read (generally starting with `/bin/bash`).

## Directions

### Writing a shell script
1. Run the following command to create a shell script named "script_text.sh".
```shellsession
vi script_text.sh
```
2. Press **i** to switch to the editing mode, refer to the following content, write it into the file, and save the "script_text.sh" script.
```bash
#!/bin/bash
echo "Hello Tencent Cloud."
```
<dx-alert infotype="notice" title="">
The shell script must start with `#!` and the path directing to the interpreter of the script to be read (generally starting with `/bin/bash`). For more information on the shell script, see [BASH Programming - Introduction HOW-TO](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html).
</dx-alert>




### Base64-encoding the script file[](id:Base64Script)

1. Run the following command to Base64-encode the "script_text.sh" script.
```shellsession
# Base64-encode the script
base64 script_text.sh
```
The following information is returned:
```shellsession
# Result returned after the encoding
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. Run the following command to verify the result returned after the script is Base64-encoded.
```shellsession
# Base64-decode the returned result to verify the command
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### Passing text

We provide multiple methods to launch an instance, and here we introduce two of them. Choose a method according to your requirements:
<dx-tabs>
::: Using the official website or the console[](id:Consoletrans)
1. Purchase an instance as instructed in [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and click **Advanced Settings** in "2. Complete configuration".
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. In the text box in **Advanced Settings**, enter the encoded result returned in the [Base64-encoded script](#Base64Script).
For example, the encoded result of the `script_text` script with Base64 is `IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==`.
![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. Follow the prompts on the interface to complete CVM creation.
<dx-alert infotype="explain" title="">
CVM will run the script through the open-source software cloud-init. For more information on cloud-init, visit the [cloud-init website](https://cloud-init.io/).
</dx-alert>


:::
::: Using API[](id:APItrans)
When creating a CVM instance through APIs, you can pass the text by assigning the value of the encoded result returned in the [Base64-encoded script](#Base64Script) to the `UserData` parameter of the `RunInstances` API.
The following is an sample CVM creation request with UserData:
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<Common Request Parameters>
```

:::
</dx-tabs>

### Viewing execution logs
After the CVM instance is created successfully, you can run the following command to view the script execution log:
```shellsession
cat /var/log/cloud-init-output.log
```

