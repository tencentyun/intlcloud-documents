## Summary

For Windows-based businesses, you need to create a custom image from the official Windows Server base image available at [link >>](https://market.cloud.tencent.com/products/5310) with image ID ``img-er9shcln``.

## Steps for Creating a Windows Custom Image

### 1. Create a CVM instance from the official base image

Go to the [CVM Purchase Page](https://buy.cloud.tencent.com/cvm).

![](https://mc.qcloudimg.com/static/img/f4c62ba416032b20e17ff9ec3ed15e39/s3.png)
[Cloud Market link >>](https://market.cloud.tencent.com/products/5310)

When selecting the image, select **Service Market**, search for **Batch** in the search bar, select the base image of Windows Server 2012 (image ID: img-er9shcln), follow on-screen prompts to configure storage, network and other settings and click **Buy now** to create the CVM instance.

### 2. Install the software required by the business on the CVM instance

View the created instance in the [CVM Console](https://buy.cloud.tencent.com/cvm), install all the software that your business depends on to the instance after logging in remotely and simply test related calls.

### 3. Make a custom image

![](https://mc.qcloudimg.com/static/img/270d48a5e64e7ec32e1d710f43123b47/s1.png)

Click ``Make an image`` in the console and wait for completion.

![](https://mc.qcloudimg.com/static/img/e939a39dcebe0c7449c7dacdb33e52ea/s2.png)

This ID is the ID of your custom image which can be viewed in the [Image Console](https://console.cloud.tencent.com/cvm/image) at any time.

### 4. Submit a test job using the custom image

```
qcloudcli batch SubmitJob --Version 2017-03-12 --Job '{
    "JobName": "TestJob",       // Job name
    "JobDescription": "for test ",    // Job description
    "Priority": "1",            // Job priority
    "Tasks": [                  // Task list (only one task in this example)
        {
            "TaskName": "Task1",   // Task 1 name
            "Application": {        // Task execution command
                "DeliveryForm": "LOCAL",    // Execute local command
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // Specific command content (summing the Fibonacci sequence)
            },
            "ComputeEnv": {         // Compute environment configuration
                "EnvType": "MANAGED",   // Compute environment type: managed or non-managed
                "EnvData": {        // Specific configuration (managed currently; see the instructions on CVM instance creation)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "",      // CVM image ID (to be replaced with your custom image ID)
                }
            },
            "RedirectInfo": {       // Standard output redirection configuration           
                "StdoutRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/",    // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"     // Standard error (to be replaced)
            }
        }
    ]
}'
--Placement'{
    "Zone": "ap-guangzhou-2"    // Availability zone (probably to be replaced)
}'
```

Replace the ImageId in the example in Getting Started with your custom image ID


```
qcloudcli batch SubmitJob --Version 2017-03-12  --Job '{"JobName": "TestJob",  "JobDescription": "for test", "Priority": "1", "Tasks": [{"TaskName": "Task1",  "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command":  "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "},  "ComputeEnv": {"EnvType":  "MANAGED", "EnvData": {"InstanceType": "S1.SMALL1",  "ImageId": "To be replaced" }  }, "RedirectInfo": {"StdoutRedirectPath": "To be replaced", "StderrRedirectPath":   "To be replaced"}, "MaxRetryCount":  1 } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'
```

When submitting am actual command line, copy the command above to a text file and modify the "To be replaced" parts (3 parts for image ID and log address).




