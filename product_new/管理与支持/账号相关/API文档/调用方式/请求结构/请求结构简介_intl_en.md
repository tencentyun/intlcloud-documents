The call to TencentCloud API is done by sending a request to the server address of TencentCloud API and adding the corresponding request parameters to the request based on the API description.

## Service Address
The service access address of TencentCloud API depends on the specific module. For more information, please see the description of each API.

## Communication Protocol
Most TencentCloud APIs communicate over HTTPS, providing highly secure communications tunnels.

## Request Method
TencentCloud API supports both POST and GET requests.

>
- The two request methods cannot be used together. If GET is used, parameters will be taken from the query string. If POST is used, parameters will be taken from the request body, and parameters in the query string will be ignored. The parameter format rules of the two request methods are identical. GET requests are generally used. If the parameter string is too long, POST is recommended.
- Parameters sent in GET requests have to be URL-encoded. This is not needed for POST requests.

## Request Parameters
Two types of request parameters are required for each TencentCloud API request: common ones and API ones. Common request parameters are required for every API (please see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/378/4380)), while API request parameters are specific to each API (please see "Request Parameters" in each API document).

## Character Encoding
Both the request and returned result of TencentCloud API are encoded with the UTF-8 character set.
