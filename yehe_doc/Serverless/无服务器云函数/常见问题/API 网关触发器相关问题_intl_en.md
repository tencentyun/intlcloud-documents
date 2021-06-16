### What should I do if SCF returns a 504 error?

1. Check the timeout period configured for the function and gateway and try to increase the gateway timeout period.
2. [View log analysis](https://intl.cloud.tencent.com/document/product/628/34636) to identify specific causes.

### What should I do if SCF returns the "error":403,"error":"Invalid scf response format. please check your scf response format." error message?

API Gateway parses the function response and constructs an HTTP response based on the parsed content. This integration response allows you to control the status code, headers, and body content of the response by using codes, and customize the response in the XML, HTML, JSON, and even JS format. This feature requires that [data structures of integration response for API Gateway trigger](https://intl.cloud.tencent.com/document/product/583/12513) should be returned to API Gateway for parsing; otherwise, the error message `{"error":403,"error":"requestId xxx , Invalid scf response. expected scf response valid JSON."}` will appear.

### How do I use a custom domain name?

You can bind your independent domain name to the SCF service, so that the service can be accessed at it. For more information, see [Configuring a Custom Domain Name](https://intl.cloud.tencent.com/document/product/628/11791). Then you can select **Use Existing API Service** to create an API Gateway trigger for a function that requires a custom domain name.

