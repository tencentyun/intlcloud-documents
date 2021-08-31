## Scenario

When creating a CVM, you can configure an instance by specifying **custom data**. During the **first launch** of the CVM, the custom data will be passed into the CVM in text format and be executed. If you purchase multiple CVMs at a time, all CVMs will execute the custom data upon their first launch.
This article describes how to pass a Shell script when launching a Linux CVM for the first time.

## Notes
- Linux operating systems that support custom data include:
	- 64-bit operating system: CentOS 6.8 64-bit or later versions, Ubuntu Server 14.04.1 LTS 64-bit or later versions, and suse42.3x86_64
	- 32-bit operating system: CentOS 6.8 32-bit or later versions
- A command can be executed by passing text only when a CVM is launched for the first time.
- Custom data must be Base64 encoded and then passed. **For a compatible format, encode the custom data in Linux environment.**
- Execute the custom data as `root`. Therefore, the `sudo` command is not required in the script. The `root` user can access all the files you created. If you need to grant other users with the access permission, modify the permission in the script.
- During launch, executing custom data tasks will increase the startup time of the CVM. Please wait a few minutes until the tasks are completed, and then test whether the tasks are executed successfully
* In this example, Shell script must start with `#!` and the path to the interpreter reading the script (usually `/bin/bash`).

## Directions

### Writing a Shell script
1. Run the following command to create a Shell script named “script_text.sh”.
```
vi script_text.sh
```
2. Press **i** to switch to the editing mode, enter the following and save the “script_text.sh” script.
```
#!/bin/bash
echo "Hello Tencent Cloud."
```
> Shell script must start with `#!` and the path to the interpreter reading the script (usually `/bin/bash`). For more information on Shell script, see BASH Programming of the Linux Documentation Project (tldp.org) (http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html).

<span id="Base64Script"></span>
### Encoding the script with Base64

1. Run the following command to encode the “script_text.sh” script with Base64.
```
# Base64 encoded script
base64 script_text.sh
```
You will see the following information:
```
# Encoded result
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. Run the following command to verify the Base64 encoded result of the script.
```
# Decode the returned result with Base64 and verify whether it is the command to be executed.
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### Passing the text

You can launch an instance through multiple methods, and here we introduce two of them. Choose a method according to your requirements:
- [Using the official website or the console](#Consoletrans)
- [Using API](#APItrans)

<span id="Consoletrans"></span>
#### Using the official website or the console

1. Refer to [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855) to purchase an instance, and click **Advanced Settings** in “4. Security Group and CVM”, as shown below:
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. In **Advanced Settings**, enter the returned result of [Base64 encoded script](#Base64Script) in the Custom Data text box, as shown below:
For example, the Base64 encoded result of the `script_text` script is `IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==`.
![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. Create an CVM instance as prompted by the page.
>Tencent Cloud CVM executes the script using the open-source software cloud-init. For more information about cloud-init, see [cloud-init's official website](https://cloud-init.io/).

<span id="APItrans"></span>
#### Using API

When creating a CVM by using API, you can pass the text by assigning the value of the encoded result returned in [Base64 encoded script](#Base64Script) to the UserData parameter of the RunInstances API.
The following is a sample CVM creation request with UserData:
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<Common request parameters>
```
