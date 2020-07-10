## Overview
To use Windows services, you need to create a custom image from the official Windows Server image. This document introduces how to create a Windows custom image.

##  Prerequisites
You have registered a Tencent Cloud account. If you haven’t, go to the [Sign up](https://intl.cloud.tencent.com/register) page.

## Directions


### Installing required software on a CVM
Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to check details of the CVM you have created. Log in to the CVM remotely, install all the necessary software on the CVM, and simply test the connectivity.



### Creating a custom image
1. Locate the CVM on which you want to create a custom image, click **More** -> **Create Image** under its **Operation** column, as shown below:
![](https://main.qcloudimg.com/raw/975b28eff24b9196137d220c4e830adb.png)
2. In the pop-up window, enter the image name and description, and click **Create Image**.
3. After the image is created, click **Images** in the left sidebar to query custom images, as shown below:
>!You can obtain the custom image ID on the **image** page.
>
![](https://main.qcloudimg.com/raw/2633a0a09a9d792d16baf99fba0be98b.png)



### Submitting the test job using a custom image
You can acquire and modify the official example to create a Batch computing environment under a personal account. Learn each configuration item in the computing environment by referring to the following information.
```
tccli batch SubmitJob --version 2017-03-12 --Job '{
    "JobName": "TestJob",       // Job name
    "JobDescription": "for test ",    // Job description
    "Priority": "1",            // Job priority
    "Tasks": [                  // Task list (this example only contains one task)
        {
            "TaskName": "Task1",   // Task 1 name
            "Application": {        // Task execution command
                "DeliveryForm": "LOCAL",    // Runs the local command.
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // Command content (Fibonacci summation)
            },
            "ComputeEnv": {         // Computing environment configuration
                "EnvType": "MANAGED",   // Computing environment types: MANAGED and UNMANAGED
                "EnvData": {        // Specific configuration (The current type is MANAGED. Refer to the CVM instance creation description)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "",      // CVM image ID (Replace it with your custom image ID)
                }
            },
            "RedirectInfo": {       // Configuration of standard output redirection           
                "StdoutRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/",    // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"     // Standard error (to be replaced)
            }
        }
    ]
}'
--Placement'{
    "Zone": "ap-guangzhou-2"    // Availability zone (to be replaced)
}'
```
You can use the following sample codes. Refer to the “Job Configuration” section in [Using CLI - Submit a Job](https://intl.cloud.tencent.com/document/product/599/10523), and replace the fields marked with **To be replaced** in the example with your actual information. For example, replace `ImageId` with your custom image ID.
```
tccli batch SubmitJob --version 2017-03-12  --Job '{"JobName": "TestJob",  "JobDescription": "for test", "Priority": "1", "Tasks": [{"TaskName": "Task1",  "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command":  "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "},  "ComputeEnv": {"EnvType":  "MANAGED", "EnvData": {"InstanceType": "S1.SMALL1",  "ImageId": "To be replaced" }  }, "RedirectInfo": {"StdoutRedirectPath": "To be replaced", "StderrRedirectPath":   "To be replaced"}, "MaxRetryCount":  1 } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'
```





