## 1. Preparations
Please follow the instructions in [Preparation]() to complete the preparations and learn how to configure the general part of the custom information.

## 2. Viewing and Modifying Demo
Open the 1_SimpleStart.py file with an editor.
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "LOCAL",
    "Command": " python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```
Items in the customization part (custom) have been explained in the Preparations document, except Application which will be detailed below:
* DeliveryForm: The delivery method of the application, including software package, container image and direct execution in CVM. Here, LOCAL represents direct execution in CVM
* Command: Task start command. Here, a Python script is executed which sums the first 20 number of the Fibonacci sequence starting from 1 and outputs it into StdOutput

1_SimpleStart.py is quite simple. You only need to modify the general part according to the Preparations document and then execute it directly, so there is no need to modify it again here.

## 3. Submitting a Job
The job submission process has already been encapsulated in the form of Python script + Batch CLI in the demo, so you can just follow the example below to execute the Python script:
```
$ python 1_SimpleStart.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

If the JobId field is returned, the submission succeeds. If not, please check the return value for errors. You can also consult the administrator via [User Feedback]().

## 4. Viewing State

```
$ qcloudcli batch DescribeJob  --Version 2017-03-12 --JobId job-xxx
```
View the execution state through DescribeJob by replacing the JobId with your actual JobId. Common states include:
* STARTING  Stating
* RUNNING   Running
* SUCCEED   Successfully executed
* FAILED    Execution failed

The complete return information is as follows:

```
{
    "Response": {
        "JobState": "STARTING",
        "Zone": "ap-guangzhou-2",
        "JobName": "SimpleStart",
        "Priority": 1,
        "RequestId": "8e5ef77c-fa41-4b9f-8c80-107f2546e8ed",
        "TaskSet": [
            {
                "TaskName": "Task1",
                "TaskState": "STARTING"
            }
        ],
        "JobId": "job-n4ohivif",
        "DependenceSet": []
    }
}
```

## 5. Viewing the Result

The result is saved in the StdoutRedirectPath and StderrRedirectPath directories configured during preparation as shown below:

![](https://mc.qcloudimg.com/static/img/1038bd36c2c897f7241643995757dd7f/COS_4.png)

In care of success, please view the standard output stdout.job-xxx.xxxx.0.log as follows:
```
6765
```

In case of failure, please view the standard error stderr.job-xxx.xxxx.0.log with possible content as follows:
```
/bin/sh: -c: line 0: syntax error near unexpected token `('
/bin/sh: -c: line 0: ` python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" '
```



