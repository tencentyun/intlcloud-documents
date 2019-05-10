You can call a Tencent Cloud API by sending a request to the server IP address of the API and adding parameters according to the API interface specification. A Tencent Cloud API request has the following elements:

### API endpoint address

Tencent Cloud API endpoints vary according to module. For more information, see each API specification.

### Communication protocol

Most Tencent Cloud APIs communicate over HTTPS to provide high-security connections.

### HTTP Request method

Tencent Cloud APIs support both POST and GET HTTP request methods

> **Notes:**
> 1. POST and GET cannot be used together. If you use GET, you are using the parameters obtained from Querystring. Otherwise, you are using the parameters obtained from Request Body, and ignore the parameters in the Querystring.
> Same parameter rule is applied to both GET and POST requests, and GET is more comonly used than POST. However, we do recommend you to use POST when the parameter is too long.
> 2. Parameters sent in GET requests have to be URL-encoded. This is not needed for POST requests.







### Request parameters

Two types of parameters are required for each Tencent Cloud API request: common request parameters and API request parameters. Common request parameters are required for every API (see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/11650), while API request parameters are specific to each API (see "Request Parameters" in each API document).

### Character encoding

All of the Tencent Cloud API requests and responds are UTF-8 encoded.
