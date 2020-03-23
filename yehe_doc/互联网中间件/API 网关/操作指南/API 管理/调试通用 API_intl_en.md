## Operation Scenarios
The API debugging page allows you to verify the correctness of an API immediately after completing its configuration by initiating a simulated API call and viewing the specific call log and request response. If the API fails to work as expected, you can modify the configuration according to the log and response to make it meet your design expectations.

## Directions
1. Log in to the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** on the left sidebar to enter the service list page.
2. Click a service name to enter the service details page and click **Manage API** at the top to manage the API.
3. Select the API to be debugged and click **Debug** in the "Operation" column to enter the debugging page.
On the debugging page, you can see the frontend configuration information of the API, including the path, request method, and request parameters. In the request parameters section:
	- If you configure a parameter to have a default value, the default value will be populated in the input box by default;
	- If you configure a parameter to be required, a check will be performed to verify whether any value has been entered for it before testing;
	- If your request method is POST, PUT, or DELETE, you will be required to enter a value for the `Body` parameter.
![Debugging](https://main.qcloudimg.com/raw/27992e84649800c7692945bec2345eea.png)
> If a parameter is optional and no value is entered for it, API Gateway will send a `null` to the backend by default.
4. After clicking **Send request**, you will see the output in two parts:
   - Request log: the log can output your request record in detail, including the request path and method composed of frontend parameters, header parameters, the configuration actually called by the backend, the process of initiating the request to the backend, and the response code and data content of the response from the backend. 
   - Response: the response code and data content actually returned to the frontend after an API call.
![Debugging result](https://main.qcloudimg.com/raw/3b9c79de835f326ddb90064b8361d42e.png)
