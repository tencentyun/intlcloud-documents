>? **This is a legacy API and may be deprecated in the future. It is currently not displayed on the left sidebar. We recommend using <a href="https://intl.cloud.tencent.com/document/product/214/33789" target="_blank">CLB API 3.0</a>, which is more standardized and has a significantly reduced access latency.**
>

To call a TencentCloud API, you send a request containing parameters specified in the API description to the API server address. The structure of a TencentCloud API request consists of service address, communication protocol, request method, request parameters and character encoding, as detailed below:

## Service Address
The service access address of a TencentCloud API depends on the specific module. For more information, see the description of each API.

## Communication Protocol
Most TencentCloud APIs communicate over HTTPS, which provides highly secure communication channels.

## Request Method
Tencent Cloud APIs support both POST and GET request methods.

>!
>1. POST and GET requests cannot be used together. If GET is used, parameters are taken from the query string. If POST is used, parameters are taken from the request body, and parameters in the query string are ignored. The parameter format rules of the two request methods are identical. GET requests are generally used. If the parameter string is too long, we recommend using POST.
>2. If the GET method is used, all request parameters need to be URL encoded. This is not required for the POST method.
>3. The maximum length of GET requests varies by browser and server settings. For example, the limit is 2 KB in IE and 8 KB in Firefox. For long API requests with a lot of parameters, we recommend using the POST method to avoid request failure due to overlong string.
>4. For POST requests, pass in parameters in the format of `x-www-form-urlencoded`, because the TencentCloud API acquires the request parameters from $_POST.

## Request Parameters
Each TencentCloud API request consists of two types of parameters: common request parameters and API request parameters. Common request parameters are required for every API (see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/377/4153)), while API request parameters are specific to each API (see "Request Parameters" in each API document).

## Character Encoding
Both the request and response of TencentCloud APIs are encoded using the UTF-8 character set.
