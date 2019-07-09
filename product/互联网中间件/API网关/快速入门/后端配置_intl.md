
## Integrating HTTP 
If your business is deployed in another Cloud or in your local server and is open with HTTP, select the HTTP integration for the backend.
Configuration instructions:
1. To integrate HTTP, you must select HTTP or HTTPS for Backend Type.

2. Enter the backend address, which starts with `http://` or `https://` and does not include the path behind, such as `http://api.myservice.com` or `http://108.160.162.30`.

3. Enter the backend path starting with /, such as `/path` or `/path/{petid}`.

4. Select the request method. The request methods for the frontend and the backend can be different.

5. Set the backend timeout.

6. Set the backend parameters that map the frontend.

7. Click **Finish**.
![Backend configuration](https://main.qcloudimg.com/raw/ab658b5ed1e42447c3d8eb52b9a95f86.png)

#### API Gateway backend integrates CLB resources in a VPC

When you want to integrate the backend with CLB in a VPC, the frontend configuration is the same as other API configuration methods, and the backend configuration method is as follows:

1. In the backend configuration, select the VPC to be integrated.
![](https://main.qcloudimg.com/raw/31a7b4036afabf65bb446d199a0df95e.png)

2. Select CLB in the VPC. API Gateway only supports integrating CLB in a VPC. Other cloud resources in the VPC will be supported soon.
![](https://main.qcloudimg.com/raw/739ff951ad6c76214725ce1854140ce3.png)

3. Enter `http://vip+port` or `https://vip+port` at the backend address. The requests we send to CLB will be HTTP requests or HTTPS requests depending on the content you entered. The VIP is that of CLB, which can be found in the basic information of application-based private network CLB.
![](https://main.qcloudimg.com/raw/a5ab1b742c4a9573bbfa00deda2a5dbf.png)

4. Select a listening type.

	**If you select the CLB listening type of HTTP/HTTPS**, you must configure the backend path as the path configured in the CLB listener.

	The following figure shows the domain name and path configured in the CLB listener:
![](https://main.qcloudimg.com/raw/3f55e4c00aa59225782f9fd286e443d9.png)

	The following shows the backend path in API Gateway, which must be consistent with that in CLB.
![](https://main.qcloudimg.com/raw/348e7ec22615ce020fd6aef927ac796d.png)

	You also need to configure the parameter host as the constant parameter and place it in the header. The parameter value is the domain name configured in the CLB listener.
![](https://main.qcloudimg.com/raw/264e17dda3311224b2e3fafdb52edbd3.png)

	**If you select the CLB listening type of TCP/UDP**, you must configure the backend path as the path required by the business in the CVM mounted on the CLB.

	If you configure the host verification in the CVM, you need to configure the parameter host as the constant parameter, and select the address to place parameter according to your own business, just like using a layer-7 listener.

	The subsequent configurations are the same as other API configurations.
>**Note:**
>When the backend integrates CLB, security groups on the CVM mounted to the backend should be open to the IP address ranges of 100.64.0.0/10 and 9.0.0.0/8.

## Integrating Mock 
Mock will return a response with fixed configurations for an API request. Mock is generally used for development test. It can complete the API configuration in advance and return responses when the backend service is not completely developed. When integrating MOCK, you only need to configure the returned data, and click **Finish**.
![mock](https://main.qcloudimg.com/raw/e40591c77c9c085afd09b0ffaf602f4b.png)

