The call of a Tencent Cloud API is done by sending a request to the server address of the Tencent Cloud API and adding the corresponding request parameters to the request based on the API description. The request structure of Tencent Cloud API consists of service address, communications protocol, request method, request parameter and character encoding. The specific description is as follows:

## Service Address
The service access address of a Tencent Cloud API depends on the specific module. For details, see the description of each API.

## Communications Protocol
Most of Tencent Cloud APIs communicate via HTTPS, providing highly secure communications tunnels.

## Request Method
Tencent Cloud APIs support both POST and GET requests.

>**Note:**
1. POST and GET requests cannot be mixed. If GET is used, the parameters are taken from the Querystring. If POST is used, the parameters are taken from the Request Body, and the parameters in the Querystring are ignored. The parameter format rules of the two request methods are identical. Generally, GET requests are used. When the parameter string is too long, POST is recommended.
2. If your request method is GET, then all the request parameter values need to be URL encoded. If POST, no encoding is needed.
3. The maximum length of a GET request varies for different browser and server settings. For example, the maximum length for IE is 2 KB, while that for Firefox is 8 KB. For some lengthy API requests with long parameters, it is recommended that you use the POST method to prevent the request from failing because the string exceeds the maximum length during the request.
4. For POST requests, you need to pass in the parameters in the form of `x-www-form-urlencoded` because the Cloud API takes the request parameters from $_POST.

## Request Parameters
Each Tencent Cloud API request requires specifying two types of parameters: common request parameters and API request parameters. Common request parameters are the ones used by all APIs; for details, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). API request parameters are specific to each API; for details, see the description of the "request parameters" for each API.

## Character Encoding
The request and response of the Tencent Cloud API are encoded using the UTF-8 character set.
