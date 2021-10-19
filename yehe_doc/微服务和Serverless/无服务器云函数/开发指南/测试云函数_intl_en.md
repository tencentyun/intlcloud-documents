After creating a function, you can directly test it in the following ways to understand the function execution conditions and check the code execution process.

- SCF console: [Creating Event-Triggered Function in Console](https://intl.cloud.tencent.com/document/product/583/32742)

## Test Events and Templates

Functions are executed in an event-triggered method. Different triggers pass different event data structures when they trigger functions. The function testing method is to trigger the function by sending a simulated test event.

The SCF console provides the following event templates to simulate corresponding events:

* **Hello World event template**: it contains simple data structure and content that can be used to trigger functions created by the hello world template.
* **COS file event template**: it simulates file upload/deletion events in COS.
* **CMQ topic event template**: it simulates message receiving events in a CMQ topic.
* **API Gateway event template**: it simulates API request receiving events in API Gateway.
* **CKafka event template**: it simulates message receiving events in a CKafka topic.

By clicking **Change** on the template management page in the console, you can change the currently used test template to another system-defined or custom template. For more information on message structures in event templates, please see [Trigger Event Message Structure Summary](https://intl.cloud.tencent.com/document/product/583/31439).

## Custom Template Configuration and Usage

In addition to the system-provided event templates, you can create more custom templates. By clicking **Configure** on the template management page in the console, you can modify an existing template and save it as a custom template, or directly enter a test event designed by yourself and save it as a custom template.

## Notes
When using the test event template feature, you need to pay attention to the following:
- The test event template name can contain letters, digits, hyphens, and underscores and must begin with a letter.
- On the same page, the created custom test templates can be deleted if they are no longer needed.
- Up to five custom test templates can be configured for one single function. After the limit is reached, to configure a new one, please first delete an old one that is no longer in use.


