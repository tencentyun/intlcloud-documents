Before installing CLI, make sure your system has the Python environment installed. Specifically, Python 2.7 and python-pip should be installed.

## 1. Install Tencent Cloud Command Line Interface (CLI)	
### a. Confirm that **your application for internal trial has been approved**
Otherwise, you will be prompted for denied access when trying to use Batch-related commands of CLI.

### b. Install CLI:
* If CLI has not been installed, it can be quickly installed via pip.
```
$ sudo pip install qcloudcli
```

* If CLI has already been installed, it can be quickly upgrade via pip. The command is as follows:
```
$ sudo pip install --upgrade qcloudcli
```

### c. Verify that CLI is installed successfully and includes Batch-related capabilities:
```
$ qcloudcli batch help
You should use the qcloudcli in the following format:
qcloudcli <module> <action> [options and parameters]
The action name you entered is invalid! The module [batch] supports the following valid actions:

DescribeAvailableCvmInstanceTypes       	|DescribeTask
DescribeJob                             	|SubmitJob
DescribeJobs                            	|TerminateTaskInstance
```

## 2. Get SecretID and SecretKey
### a. Log in to Tencent Cloud [API Key Console](https://console.cloud.tencent.com/capi).

### b. Create a new key or use an existing Cloud API key. Click the Cloud API key ID to go to the details page and get the SecretID and SecretKey.
![Alt text](https://mc.qcloudimg.com/static/img/ab7aea426d53f31f6bb1fc84bd2ce177/1.png)

## 3. Prepare the COS directory
### a. Create buckets and subfolders
![](https://mc.qcloudimg.com/static/img/ecb3282f6cf12b371925743d9efa3874/COS_1.png)
Create a bucket with an arbitrary name and create three folders in the bucket with the names as shown above for subsequent use.

### b. Note down the COS access address
![](https://mc.qcloudimg.com/static/img/0a0a2a781ed55febaecc2531fbe4f592/COS_2.png)

View the access domain name of the COS bucket as shown in the figure above, and then create the access domain names of the three folders by piecing together the domain name and folder name. For example, the access addresses of the three folders created by the official account just now are as follows:

* cos://batchdemo-1251783334.cosgz.myqcloud.com/logs/
* cos://batchdemo-1251783334.cosgz.myqcloud.com/input/
* cos://batchdemo-1251783334.cosgz.myqcloud.com/output/

``` Be sure to create the folder access address based on your own bucket access domain name```

## 4. Download the Batch Demo File

[Download address](http://batchdemo-1251783334.cosgz.myqcloud.com/demo/BatchDemo.zip). The directory structure after decompression is as follows. Subsequently, please try Batch for various capabilities in the following order:

* [1_SimpleStart](https://cloud.tencent.com/document/product/599/10551)
* [2_RemoteCodePkg](https://cloud.tencent.com/document/product/599/10552)
* [3_StoreMapping](https://cloud.tencent.com/document/product/599/10983)

``` The demo is provided in form of Python + Batch CLI. Batch has many capabilities and configurable items, and it's easier to navigate using Python scripts. ```

## 5. Description of the General Part of the Custom Information in the Demo
Take the custom information part of "1_SimpleStart" as an example.

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

* imageId: The image containing the Cloud-init service is required during the internal trial period. Tencent Cloud provides a CentOS 7.2 image (image ID: **img-31tjrtph**) in Cloud Market that can be directly used. A custom image should be created based on this image
* StdoutRedirectPath, StderrRedirectPath: Please enter the full access address of the logs folder in the COS directory prepared in step 3. The address cos://batchdemo-1251783334.cosgz.myqcloud.com/logs/ in the example should be replaced with you own access address
* Application: This is used to start the command line and doesn't need to be modified for the time being
