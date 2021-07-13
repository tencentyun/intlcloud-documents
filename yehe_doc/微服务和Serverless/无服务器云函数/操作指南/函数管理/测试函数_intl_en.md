## Directions
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** page, click the target function to enter its details page.
3. Select **Function Code** on the **Function Management** page.
4. Select the desired test template in the "Editor" as shown below:
![](https://main.qcloudimg.com/raw/8893e985cb3965a424544847996e1fdd.png)
5. Click **Test** to test the function.


## Testing Event Template
During product iteration, new content will be added to the default testing event templates.
A testing event template is used to simulate the event and content passed to a function when the corresponding trigger triggers the function, which is represented as the `event` input parameter in the function. The template must be a data structure in JSON format. The default testing event templates and their descriptions are as follows:
* Hello World event template: this is a simple custom event template that allows you to enter custom event content when you trigger a function through TencentCloud API.
* COS file upload and deletion event template: this simulates an event that is generated and passed upon function triggering when a file is uploaded or deleted in a bucket after a COS trigger is bound.
* CMQ topic event template: this simulates an event that is generated and passed upon function triggering when a message is received in CMQ after a CMQ topic subscription is bound.
* API Gateway event template: this simulates an event that is generated and passed upon function triggering when an API request arrives API Gateway after API Gateway is bound.

## Custom Testing Event Template
Before testing, you can directly select a default test template or modify the test template based on your own event conditions and save it as a custom test template. The modified test template passes the event content that is used as function trigger to the function and must be in JSON format.

### Use limits
The following usage restrictions apply to custom testing event templates.
- Custom testing event templates are used at the account level. Different functions under the same account share the same testing event template.
- Up to five custom testing templates can be configured for one account.
- A custom testing template can be up to 64 KB in size.

### Creating and saving custom testing event template
When testing, if you do not want to modify the testing template every time, you can save the modified template as a custom template. After selecting the template to be modified, you can click **Create Template** to modify the template, enter an easy-to-remember name, and save it. When using the saved template for testing subsequently, the template on the testing page will be the same as that used last time.

### Deleting custom testing event template
You can delete a custom template that is no longer used by selecting it and clicking **Delete**.



