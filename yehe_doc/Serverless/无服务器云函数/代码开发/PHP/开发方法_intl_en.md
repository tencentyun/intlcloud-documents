## Function Form

The PHP function form is generally as follows:

```php
<?php
function main_handler($event, $context) {
    print_r ($event);
    print_r ($context);
    return "hello world";
}
?> 
```

## Execution Method

You need to specify the execution method when creating a SCF function. If the PHP programming language is used, the execution method is similar to `index.main_handler`, where `index` indicates that the executed entry file is `index.php`, and `main_handler` indicates that the executed entry function is `main_handler`.

When submitting the ZIP code package by uploading the ZIP file locally or through COS, please make sure that the root directory of the ZIP package contains the specified entry file, which contains the entry function specified by the definition, file name, function name, and execution method; otherwise, execution will fail as the entry file or entry function cannot be found.

## Input Parameters

The input parameters in the PHP environment include $event and $context.

- **$event**: this parameter is used to pass the trigger event data.
- **$context**: this parameter is used to pass runtime information to your handler.

The event parameter varies with trigger or event source. For more information on its data structure, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).

## Response

Your handler can use `return` to return a value. The return value will be handled differently depending on the function invocation type.

In the Python environment, a serializable object such as `dict` object can be directly returned:

- **Sync invocation**: the return value of a sync invocation will be serialized in JSON and returned to the caller for subsequent processing. The function testing in the console is sync invocation, which can capture the function’s return value and display it after the invocation is completed.
- **Async invocation**: the return value of an async invocation will be discarded, since the invocation method responds right after the function is triggered, without waiting for function execution to complete.

> ? 
> - The return value of both sync and async invocations will be recorded in the function logs. The return value will be written to the function invocation log `SCF_Message` in the format of `Response RequestId:xxx RetMsg:xxx`.
> - The value of `SCF_Message` is limited to 8 KB in length, and excessive parts will be truncated.

## Exception Handling

You can exit the function by calling `die()`. At this point, the function will be marked as execution failed, and the output from the exit using `die()` will also be recorded in the log.
