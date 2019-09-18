
You can call a TencentCloud API by sending a request to the API server address that contains the request parameters specified in the API description. The structure of a TencentCloud API request consists of service address, communication protocol, request method, request parameters, and character encoding, as detailed below:

## Service Address
The service access address of TencentCloud API depends on the specific module. For more information, see the descriptions of each API.

## Communication Protocol
Most of TencentCloud APIs communicate via HTTPS, providing highly secure communication tunnels.

## Request Method
TencentCloud API supports both POST and GET requests.

>1. POST and GET requests cannot be used together. If GET is used, the parameters are taken from the query string. If POST is used, the parameters are taken from the request body, and the parameters in the query string are ignored. The parameter format rules of the two request methods are identical. GET requests are generally used. If the parameter string is too long, POST is recommended.
>2. If the GET method is used, all request parameters need to be URL-encoded. This is not required if the POST method is used.
>3. The maximum length of GET requests varies by browser and server settings. For example, the limit is 2 KB in IE and 8 KB in Firefox. For long API requests with a lot of parameters, we recommend using the POST method so as to avoid request failure due to overlong string.
>4. For POST requests, the input parameters should be in the form of `x-www-form-urlencoded`, because TencentCloud API acquires the request parameters from $_POST.

## Request Parameters
Two types of parameters are required for each Tencent Cloud API request: common request parameters and API request parameters. Common request parameters are required for every API (see [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/公共请求参数), while API request parameters are specific to each API (see "Request Parameters" in each API document).

## Character Encoding
Both the request and returned result of TencentCloud API are encoded using the UTF-8 character set.
