In the console or through TCCLI, function testing is used to directly initiate a function call, simulate a triggering event sent by the trigger, and display the function execution conditions, return content, and log.

## Testing a Function in the Console
On the function details page in the console, you can test run a function by going to the function code tab and clicking **Execute**.

### Testing Event Template
During product iteration, new content will be added to the default testing event templates.
A testing event template is used to simulate the event and content passed to a function when the corresponding trigger triggers the function, which is represented in the function as event input parameter. The template must be a data structure in JSON format. The default testing event templates and their descriptions are as follows:
* Hello World event template: This is a simple, custom event template that allows you to enter custom event content when you trigger a function through TencentCloud API.
* COS file upload and deletion event template: This simulates an event that is generated and passed upon function triggering when a file is uploaded or deleted in a bucket after a COS trigger is bound.
* CMQ topic event template: This simulates an event that is generated and passed upon function triggering when a message is received in a topic queue after a CMQ topic subscription is bound.
* API Gateway event template: This simulates an event that is generated and passed upon function triggering when an API request arrives API Gateway after API Gateway is bound.

### Custom Testing Event Template
Before testing, you can directly select a default test template, or modify the test template based on your own event conditions and save it as a custom test template. The modified test template passes the event content that is used as function trigger to the function, and must be in JSON format.

#### Custom Testing Event Template Usage Restrictions
The following usage restrictions apply to custom testing event templates.
- Custom testing event templates are used at the account level. Different functions under the same account share the same testing event template.
- Up to 5 custom testing templates can be configured for a single account.
- A custom testing template can be up to 64 KB in size.

#### Creating and Saving a Custom Testing Event Template
When testing, if you do not want to modify the testing template every time, you can save the modified template as a custom template. After selecting the template to be modified, you can click **Create a template** to modify the template, enter a memorable name, and save it. When using the saved template to test subsequently, the template in the testing interface will be the same as that used last time.

#### Deleting a Custom Testing Event Template
You can delete a custom template that is no longer used by selecting it and clicking **Delete**.

## Testing a Function Through TCCLI
Before starting, you need to install and configure TCCLI by following the instructions in [TCCLI Installation and Configuration](https://intl.cloud.tencent.com/document/product/1013/33463).

The function can be executed using the `tccli scf Invoke` command. `FunctionName` is a required parameter, indicating the name of the function to be executed; the `InvocationType` parameter can be used to specify sync or async execution method; the `LogType` parameter specifies whether to obtain the execution log; and the `ClientContext` parameter is used to enter the testing event content.
When entering the testing event content, you should pay attention to the conversion of data content. You need to first perform JSON format escaping and then complete URL-encoding. For example, if you want to enter the event content `{"test":"value"}`, you need to first escape it into `{\"test\":\"value\"}` and then URL-encode it into `%7B%5C%22test%5C%22:%5C%22value%5C%22%7D`.
```
$ tccli scf Invoke --FunctionName testclifunc --ClientContext '%7B%5C%22test%5C%22:%5C%22value%5C%22%7D' --LogType Tail
{
    "Result": {
        "MemUsage": 126976, 
        "Log": "hello world\n{'test': 'value'}\n", 
        "RetMsg": "{\"test\": \"value\"}", 
        "BillDuration": 100, 
        "FunctionRequestId": "ba54a7cc-b569-11e8-b955-525400c7c826", 
        "Duration": 1.049, 
        "ErrMsg": "", 
        "InvokeResult": 0
    }, 
    "RequestId": "8fe876cc-e5b2-42ae-b461-3c45a944d425"
}
```
