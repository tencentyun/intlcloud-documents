A function is the basic unit of management and operation, which usually consists of a series of configuration items and executable code/packages.

## Function Configuration Attributes
When creating a function, you need to provide the following information:
- Function name (FunctionName): unique identifier of the function, which is required and cannot be modified after creation. 
- Runtime environment (Runtime): runtime environment of the function, which is required and cannot be modified after creation.
- Function code (Code): code that the function executes, which is required and can be modified after creation.
- Execution method (Handler): name of the function execution method, which is required and usually in the format of "filename.method name" and varies by runtime environment. For more information, please see [Programming Language Description](https://intl.cloud.tencent.com/document/product/583/11061).
- Function description (Description): used to record information such as the purpose of the function, which is optional.


In addition to the items above, you can also modify the following configuration items for function execution by [updating function configuration](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/583/19806):
- Memory size (MemorySize): amount of memory available for the function during execution, which is optional. It ranges from 64 to 3,072 MB in increments of 128 MB starting from 128 MB (default value). The CPU processing capacity of a function is directly proportional to the function's configured memory. You can increase or decrease the memory to control the configured memory and CPU processing capacity allocated to the function.
- Execution timeout (Timeout): maximum execution duration of the function between 1 and 900 seconds (3 seconds by default), which is optional.
- Environment variable (Environment): this is optional and can be defined in the configuration and obtained from the environment when the function is executed.
- VPC (VPCConfig): after configuring a VPC, you can place the function in the configured VPC for execution, which is optional.

## Executable Operations for Function
- [Creating function](https://intl.cloud.tencent.com/document/product/583/19806): creates a function.
- [Updating function](https://cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/583/19806):
 - Updating function configuration: updates the configuration items of the function.
 - Updating function code: updates the execution code of the function.
- [Getting details](https://intl.cloud.tencent.com/document/product/583/19809): gets function configuration, trigger, and code details.
- [Testing function](https://intl.cloud.tencent.com/document/product/583/14572): triggers the function in a sync or async manner as needed.
- [Getting log](https://intl.cloud.tencent.com/document/product/583/19810): gets the log of function execution and output.
- [Deleting function](https://intl.cloud.tencent.com/document/product/583/19807): deletes a function that is no longer needed.

Function trigger-related operations include:
- [Creating trigger](https://intl.cloud.tencent.com/document/product/583/31441): creates a trigger.
- [Deleting trigger](https://intl.cloud.tencent.com/document/product/583/31442): deletes an existing trigger.

## Execution Method
The execution method specifies the starting file and function while invoking the function. There are three ways as follows:
- For Go programming, use the **"[FileName]"** format, such as `main`.
- For Python, Node.js, or PHP programming, use the **"[FileName].[FunctionName]"** format, such as `index.main_handler`.
>?Please note that FileName does not include the file name extension, and FunctionName is the name of the entry function. Ensure that the file name extension matches the programming language. For example, for Python programming, the file name extension is `.py`, and for Node.js programming, the file name extension is `.js`. 
>
- For Java programming, use the **"[package].[class]::[method]"** format, such as `example.Hello::mainHandler`.

