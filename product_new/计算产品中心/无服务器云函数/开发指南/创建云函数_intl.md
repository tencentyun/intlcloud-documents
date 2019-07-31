By packaging the application service code and related dependencies and uploading the package to SCF, an SCF function is created. The function contains user-uploaded code, dependencies, and running-related configuration information. This document describes the specific function configuration items and their meanings to help you understand how to build functions suitable for your own business.

## Function Name
Tencent Cloud uses the function name to uniquely identify an SCF function in a single region, which cannot be modified after the function is created. The function name should follow the following rules:

- It can contain up to 60 characters
- It can contain only `a-z, A-Z, 0-9, -, _`
- It must begin with a letter

## Region

You specify in which region the function is executed. Currently, Beijing, Shanghai, Guangzhou, and Chengdu regions are supported. The function is automatically deployed across multiple availability zones within a region to provide high availability. The region attribute cannot be changed after the function is created.

## Computing Resources

Tencent Cloud allows you to define the *memory space* allocated to the function, which can be `128 - 1,536 MB` in increments of 128 MB. Tencent Cloud will automatically allocate proportional CPU processing power to the function based on the user-specified memory. For example, if you allocate 1,024 MB of memory to a function, the CPU obtained by the function will be *twice* that when 512 MB of memory is allocated. Therefore, in a conventional scenario, increasing the memory space for the function usually results in a relative reduction in the actual computation duration of the code.

You can change the memory space required by the function at any time. It is strongly recommended that you increase the value of this parameter if you find that the memory consumed by the function is approaching or reaches the set memory space during testing to avoid function errors due to OOM.

## Timeout Period
SCF is billed based on the execution duration and number of requests. In order to prevent a function from running indefinitely (such as when an infinite loop occurs in the code), each function has a user-definable timeout period, which is 3 seconds by default and can be up to 300 seconds. After the timeout period elapses, if the function is still running, the SCF platform will automatically terminate the function.

You can change the timeout period of the function at any time. It is strongly recommended that you increase the value of this parameter if you find that the function times out or its actual execution duration is close to the timeout period during testing to avoid function termination due to timeout.

## Description

You can set and change the function description at any time.

## Function Code Upload Method

At present, function code supports **online editing**, **local zip package upload**, and **zip package upload through COS**.

### Online Editing

The code of the entry file can be directly modified in the file editing window in the console. The entry file in a code package successfully uploaded via **local zip package upload** or **zip package upload through COS** can also be edited online without affecting other libraries or reference files.

### Local Zip Package Upload

You can directly select the function code package that has been zipped and upload it through the upload API in the console. For this upload method, the zip package cannot be greater than 5 MB in size. A larger zip package can be submitted via **zip package upload through COS**.

### Zip Package Upload Through COS

When uploading a zip package through COS, you first upload the zip package to a COS bucket in the same region, and then submit the package to the SCF platform by specifying the bucket and file location when creating or modifying a function. To upload a zip package using COS, you need to enter the COS bucket and zip file path.

* COS bucket: Only a COS bucket in the same region as the function can be selected. Choose the bucket where the zip package is located in the drop-down list.
* COS object file: This is the path and file name of the zip package in the COS bucket, beginning with the root directory `/`. For example, the test.zip file in the root directory should be written as `/test.zip`; if the functioncode folder is created in the root directory and the test.zip file is placed in the folder, it should be written as `/functioncode/test .zip`.

## Execution Method

The execution method indicates which function of which file should be called. It is usually written as `index.main_handler`, which points to the main\_handler function method in the index file. The execution method can be modified based on the actual file name and function name.

The first half of the execution method identifies the file name, for example, index refers to the index.py, index.js, or index.php file in the root directory of the code package in the Python, Node.js, or PHP environment, respectively. Please make sure that the file name suffix corresponds to the runtime environment.

The second half of the execution method identifies the function name, for example, main\_handler points to the main\_handler function in the file. When SCF is triggered, it will first call this function and pass the event and context parameters to the function. For more information about the specific function writing method and input parameters, see the notes on the corresponding programming language.
