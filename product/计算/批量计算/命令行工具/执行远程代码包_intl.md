Batch can extract code package from .tgz files in the form of HTTP. You can compress the code and upload it to COS. In this way, the code can be organized more easily than in LOCAL mode.

## 1. Preparations
Please follow the instructions in [Preparation](https://cloud.tencent.com/document/product/599/10548) to complete the preparations and learn how to configure the general part of the custom information.

## 2. Viewing and Modifying Demo
Open the 2_RemoteCodePkg.py file with the editor
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/fib.py",
    "PackagePath": "http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```
Items in the customization part (custom) have been explained in the Preparations document, except Application which will be detailed below:
* DeliveryForm: The delivery method of the application, including software package, container image and direct execution in CVM. Here, PACKAGE represents the software package method
* PackagePath: The address of the package provided in the form of HTTP. It must be in .tgz format. Batch will download the package to a directory of the scheduled CVM instance and then execute Command there
* Command: The task start command. A Python script file in the package is called directly here. You can download the package and view the file structure and content inside

The content of fib.py is as follows:
```
fib = lambda n:1 if n<=2 else fib(n-1)+fib(n-2)
print("Remote Code Package : %d"%(fib(20)))
```

2_RemoteCodePkg.py is quite simple. You only need to modify the general part according to the Preparations document and then execute it directly, so there is no need to modify it again here.

## 3. Submitting a Job
The job submission process has already been encapsulated in the form of Python script + Batch CLI (internal trial version) in the demo, so you can just follow the example below to execute the Python script:
```
$ python 2_RemoteCodePkg.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

If the JobId field is returned, the submission succeeds. If not, please check the return value for errors. You can also consult the administrator in the chat group for [User Feedback](https://cloud.tencent.com/document/product/599/10806).

## 4. Viewing State
See the section with the same name in [Quick Start](https://cloud.tencent.com/document/product/599/10551).

## 5. Viewing the Result
See the section with the same name in [Quick Start](https://cloud.tencent.com/document/product/599/10551).

The execution result of 2_RemoteCodePkg.py is as follows:
```
Remote Code Package : 6765
```
