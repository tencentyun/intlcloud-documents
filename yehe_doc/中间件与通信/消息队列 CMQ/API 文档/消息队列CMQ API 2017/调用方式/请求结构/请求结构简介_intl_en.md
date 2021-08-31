The call to a TencentCloud API is done by sending a request to the server address of the API and adding the corresponding request parameters to the request based on the API description. The structure of a TencentCloud API request consists of service address, communication protocol, request method, request parameters, and character encoding as detailed below:

## Service Address
The service access address of TencentCloud API depends on the specific module. For more information, please see the description of each API.

## Communication Protocol
Most TencentCloud APIs communicate over HTTPS, providing highly secure communication tunnels.

## Request Method
TencentCloud API supports both POST and GET requests.

>!
1. POST and GET requests cannot be mixed. If GET is used, parameters will be taken from the query string. If POST is used, parameters will be taken from the request body, and parameters in the query string will be ignored. The parameter format rules of the two request methods are identical. GET requests are generally used. If the parameter string is too long, POST is recommended.
2. Parameters sent in GET requests have to be URL-encoded. This is not needed for POST requests.
3. The maximum length of a GET request varies by browser and server settings. For example, the limit is 2 KB in Internet Explorer and 8 KB in Firefox. For long API requests with a lot of parameters, we recommend you use the POST method so as to avoid request failure due to overlong string.
4. For POST requests, the input parameters should be in the format of `x-www-form-urlencoded`, because TencentCloud API gets request parameters from `$_POST`.

## Request Parameters
Two types of request parameters are required for each TencentCloud API request: common ones and API ones. Common request parameters are required for every API (please see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/406/5883)), while API request parameters are specific to each API (please see "Request Parameters" in each API document).

## Character Encoding
Both the request and returned result of TencentCloud API are encoded with the UTF-8 character set.
