Remote mapping is Batch's auxiliary function for storage and can map remote storage such as COS and CFS to a local folder.

## 1. Preparations
Please follow the instructions in [Preparation]() to complete the preparations and learn how to configure the general part of the custom information.

## 2. Uploading Input Data File
The content of number.txt is as follows:
```
1
2
3
4
5
6
7
8
9
```

Upload the file to the input folder created during preparation

![](https://mc.qcloudimg.com/static/img/02738c821f14ed132fef76c466c79d08/COS_5.png)

## 3. Viewing and Modifying Demo
Open the 3_StoreMapping.py file with the editor
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/countnum.py",
    "PackagePath": "http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
InputMapping = {
    "SourcePath": "your input remote path",
    "DestinationPath": "/data/input/"
}
OutputMapping = {
    "SourcePath": "/data/output/",
    "DestinationPath": "your output remote path"
}
```
Compared with 2_RemoteCodePkg.py, the customization part has the following changes:
* Application's Command is changed to executing countnum.py 
* InputMapping (the input mapping): SourcePath remote storage address (changed to the address of the input folder created during preparation), DestinationPath local directory (not modified at this time)
* OutputMapping (the output mapping): SourcePath local directory (not modified at the moment), DestinationPath remote storage address (changed to the address of the output folder created during preparation)

The content of countnum.py is as follows:
```
import os

inputfile = "/data/input/number.txt"
outputfile = "/data/output/result.txt"

def readFile(filename):
    total = 0
    fopen = open(filename, 'r')
    for eachLine in fopen:
        total += int(eachLine)
    fopen.close()
    print "total = ",total
    fwrite = open(outputfile, 'w')
    fwrite.write(str(total))
    fwrite.close()

print("Local input file is ",inputfile)
readFile(inputfile)
```
Open the input/number.txt file, sum the numbers in each line and write the result to output/Result.txt.

## 4. Submitting a Job
The job submission process has already been encapsulated in the form of Python script + Batch CLI (internal trial version) in the demo, so you can just follow the example below to execute the Python script:
```
$ python 3_StoreMapping.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

If the JobId field is returned, the submission succeeds. If not, please check the return value for errors. You can also consult the administrator via [User Feedback]().

## 5. Viewing State
See the section with the same name in [Quick Start]().

## 6. Viewing the Result
Batch will copy the output data from the local directory to the remote storage directory. The execution result of 3_StoreMapping.py is saved in result.txt which will be automatically synced to COS.
![pic](https://mc.qcloudimg.com/static/img/aee7138e589378eea48851dd1649b711/COS_6.png)
```
45
```
