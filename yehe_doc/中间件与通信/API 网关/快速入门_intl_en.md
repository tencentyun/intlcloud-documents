Before using Tencent Cloud API Gateway, you are recommended to read its [Product Overview](https://intl.cloud.tencent.com/document/product/628/11755), [Use Limits](https://intl.cloud.tencent.com/document/product/628/31716), and [Purchase Guide](https://intl.cloud.tencent.com/document/product/628/11771).

In the API Gateway Console, you can quickly perform operations such as creating services, creating/debugging APIs, making releases, and implementing access by following the steps below:


## Step 1. Sign up for a Tencent Cloud account
If you already have a Tencent Cloud account, you can ignore this step.
<div style="background-color:#00A4FF; width: 190px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;">Click here to sign up for a Tencent Cloud account</a></div>

## Step 2. Verify your identity
If you have already done so, you can ignore this step.
For more information on how to verify your identity, please see <a href="https://intl.cloud.tencent.com/document/product/378/3629">Identify Verification Overview</a>.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>



## Step 3. Log in to API Gateway
<div style="background-color:#00A4FF; width: 220px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/apigateway" target="_blank"  style="color: white; font-size:16px;">Click here to log in to the API Gateway Console</a></div>



## Step 4. Create a service
1. In the [API Gateway Console](https://console.cloud.tencent.com/apigateway), click **Service** on the left sidebar to enter the service list page.
2. Click **Create** and enter the service details.
 - Service Name: this is required and can contain up to 50 characters out of `a-z`, `A-Z`, `0-9`, and `_`. `exampleservice` is entered here as an example.
 - Frontend Type: protocol type supported by the service. `HTTP` is selected here as an example.
 - Remarks: remarks of the service. `Testing` is entered here as an example.
![](https://main.qcloudimg.com/raw/d979368f1746512a2e9e0064a9a92561.png)
3. Click **Submit** to create the service.


## Step 5. Create an API with Mock as the backend type
1. In the service list, click a service name to enter the service details page.
2. On the service details page, click **Manage API** to enter the API list page.
3. Click **General API** > **Create** and enter the frontend configuration information of the API.
	- API Name: name of an API. `exampleapi` is entered here as an example.
	- Frontend Type: HTTP and WebSocket are supported. `HTTP` is selected here as an example.
	- Path: access path of the API. `/` is entered here as an example.
	- Request Method: request method of the API. `GET` is selected here as an example.
	- Authentication Type: three types of authentication are currently supported: no authentication, OAuth 2.0, and key pair. `No authentication` is selected here as an example.
	- CORS Support: whether the API supports cross-origin resource sharing. `Yes` is selected here as an example.
	- Remarks: remarks of the API. `Testing` is entered here as an example.
	- Parameter Configuration: frontend parameters of the API. Nothing is entered here.
![](https://main.qcloudimg.com/raw/d979368f1746512a2e9e0064a9a92561.png)
4. Click **Next** and enter the backend configuration information of the API.
	- Backend Type: type of the backend service of the API. `mock` is selected here as an example.
	- Returned Data: data to be returned by Mock. `hello world, hello apigateway` is entered here as an example.
![](https://main.qcloudimg.com/raw/0d163eff7c5ba8e8e5377a547c7032d8.png)
5. Click **Complete** to create the API with Mock as the backend type.



## Step 6. Debug the API
1. Find the API just created in step 5 on the API list page and click **Debug** in the "Operation" column to enter the API debugging page.
2. Select `application/x-www-form-urlencoded` as the `Content-Type`.
3. Click **Send Request** and view the result returned after debugging.
![](https://main.qcloudimg.com/raw/2a4b35df5799f3da48b2b713c78b4768.png)


## Step 7. Publish the service
A created service is in unpublished state by default and can be normally accessed only after it is published.
1. Find the service just created on the service list page, click **Publish** in the "Operation" column, and enter the service release information.
	- Environment: environment in which the service is published. The release environment is selected here.
	- Remarks: remarks of the service release. `Release for testing` is entered here as an example.
![](https://main.qcloudimg.com/raw/1dd18d606de4841c490f3ccdab489c10.png)
2. Click **Submit** to publish the service.
3. After the service is published, you can access the API at the sub-domain name provided by the service.



## Troubleshooting
If you have any questions, please follow the steps below for solutions:
1. View [FAQs](https://intl.cloud.tencent.com/document/product/628/34887) to find a solution.
2. If you can't find a satisfactory answer, please contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).



## Related Documents
For more information on how to use the API Gateway Console, such as viewing logs, viewing monitoring data, or setting a traffic control policy, please see [Operation Guide](https://intl.cloud.tencent.com/document/product/628/34064).


