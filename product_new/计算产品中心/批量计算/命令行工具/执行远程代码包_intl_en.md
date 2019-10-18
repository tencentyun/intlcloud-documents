## Scenario
Batch allows you to acquire a code package from a .tgz file via HTTP. You can compress the code and upload it to COS. This helps you organize the code more conveniently than using LOCAL mode.

## Prerequisites
Complete preparations based on the instructions in [Preparation](http://intl.cloud.tencent.com/document/product/599/10548), and learn how to configure the general part of the custom information.

## Steps
### Viewing the Demo
>Modify the general part of the custom information in `2_RemoteCodePkg.py` based on the instructions in [Preparation](http://intl.cloud.tencent.com/document/product/599/10548).
>
Open the `2_RemoteCodePkg.py` file in an editor.
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/fib.py",
    "PackagePath": "http://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```
All information except `Application` in the general part is described in Preparation. Set the parameters of `Application` based on the following table.

<table>
	<tr>
	<th>Configuration Item</th>
	<th>Description</th>
	</tr>
	<tr>
	<td>DeliveryForm</td>
	<td>Three delivery methods of applications are available: software packaging, container image, and direct running within the CVM. In this case, PACKAGE indicates software packaging.</td>
	</tr>
	<tr>
	<td>PackagePath</td>
	<td>Address of the .tgz software package in HTTP. Batch downloads the software package to a directory of the scheduled CVM and runs `Command` in the directory.</td>
	</tr>
	<tr>
	<td>Command</td>
	<td>Task startup command. In this case, a Python script file in the software package is directly called. You can download the package, and view the file structure and content in it.</td>
	</tr>
</table>

`fib.py` is composed as below:
```
fib = lambda n:1 if n<=2 else fib(n-1)+fib(n-2)
print("Remote Code Package : %d"%(fib(20)))
```


### Submitting a Job
Run the following command to run the Python script.
The demo encapsulates the job submission process by using Python scripts and the Batch command line tool.
```
python 2_RemoteCodePkg.py
```
The returned result is as follows, indicating that the job is successfully submitted:
```
{
    "RequestId": "c09e9291-2661-xxxx-8783-72d36f91ec8a", 
    "JobId": "job-7xxxx26l"
}
```
If the submit operation fails, check the returned value or [Contact Us](http://intl.cloud.tencent.com/document/product/599/10806).


### Viewing State
See [Viewing State](http://intl.cloud.tencent.com/document/product/599/10551) in Quick Start.

### Viewing the Result
1. See [Viewing the Result](http://intl.cloud.tencent.com/document/product/599/10551) in Quick Start.
2. The execution result of `2_RemoteCodePkg.py` is as follows:
```
Remote Code Package : 6765
```
