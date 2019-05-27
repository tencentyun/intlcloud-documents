An SCF function is the basic unit of management and operation, which usually consists of a series of configuration items and executable code/packages.

## Function Configuration Configurations
When creating a function, you need to provide the following information:
- Function name (FunctionName): Required, which is the unique identifier of the function and cannot be modified after creation. 
- Runtime environment (Runtime): Required, which specifies the runtime environment of the function and cannot be modified after creation.
- Function code (Code): Required, which is the code that the function executes and can be modified after creation.
- Execution method (Handler): Required, which is the name of the function execution method and usually in the form of "file name. method name". This varies by runtime environment. For more information, see the descriptions of each programming language.
- Memory size (MemorySize): Optional, which specifies the amount of memory available for the function during execution. The minimum value is 128 MB (default) and increments by 128 MB.
- Execution timeout (Timeout): Optional, which specifies the maximum execution duration of the function between 1 and 300 seconds (3 seconds by default).
- Function description (Description): Optional, which can be used to record information such as the purpose of the function.

In addition to the items above, you can configure more function configurations during execution:
- Environment variable (Environment): Optional, which can be defined in the configuration and obtained from the environment when the function is executed.
- VPC (VPCConfig): Optional. After configuring a VPC, you can place the function in the configured VPC for execution.

## Executable Operations for a Function
- [Creating a function](/document/product/583/19806): Create a function;
- [Updating a function](/document/product/583/19808):
 - Updating function configuration: Update the configuration items of the function;
 - Updating function code: Update the execution code of the function;
- [Getting details](/document/product/583/19809): Get function configuration, trigger and code details;
- [Testing a function](/document/product/583/14572): Trigger the function in a synchronous or asynchronous manner as needed;
- [Getting a log](/document/product/583/19810): Get the log of function execution and output.
- [Deleting a function](/document/product/583/19807): Delete the function that is no longer needed.

Function trigger-related operations include:
- Creating a trigger: Create a trigger;
- Deleting a trigger: Delete an existing trigger.
