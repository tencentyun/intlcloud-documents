After creating a function, you can directly test it in the console to understand the function execution conditions and check the code execution process. The function is executed in an event-triggered method, and the test is performed by sending a simulated event to trigger the function.

## Test Events and Templates

Functions are executed in an event-triggered method. Different triggers pass different event data structures when they trigger functions. The function testing method is to trigger the function by sending a simulated test event.

The SCF console provides the following event templates to simulate corresponding events:

* Hello World event template: It contains simple data structure and content that can be used to trigger functions created by the hello world template.
* COS file event template: It simulates file upload/deletion events in COS.
* CMQ topic event template: It simulates message receiving events in a CMQ topic.
* API Gateway event template: It simulates API request receiving events in API Gateway.
* CKafka event template: It simulates message receiving events in a CKafka topic.

By clicking the **Change** button on the template management page in the console, you can change the currently used test template to another system-defined or custom template.

### Custom Template Configuration and Usage

In addition to the system-provided event templates, you can create more custom templates. By clicking the **Configure** button on the template management page in the console, you can modify an existing template and save it as a custom template, or directly enter a test event designed by yourself and save it as a custom template.

The name of the test event template can contain letters, digits, - and _, and has to begin with a letter.

On the same page, the created custom test templates can be deleted if they are no longer needed.

Up to 5 custom test templates can be configured for one single function. After the limit is reached, to configure a new one, please first delete and old one that is no longer in use.

## Function Testing

You can click **Test** or **Save and test** on the function code page to trigger the function using the currently selected test template.

After the function is triggered, the "Test result", "Return result", "Summary", and "Log" will be added at the bottom of the page for display.

### Test Result

This identifies whether the result of the current test run is a success or failure.

### Return Result

This is the return content of the function, corresponding to the return data structure content in the function code.

### Summary

This records the statistics of the current execution, including the current request ID, function execution duration, billable duration, and memory occupied.

### Log

This is the function output log of the current runtime, i.e., the printout of the log in the function code. Currently, the log output can be up to 512 KB. If the function outputs too many log entries, they will be truncated when outputted to the console.
