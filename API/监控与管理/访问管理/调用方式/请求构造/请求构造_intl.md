The process of calling a Tencent Cloud API is achieved by sending a request to the server IP address of the API and adding relevant request parameters in the request as described in the API description. A request for calling a Tencent Cloud API is made up of the following elements:

### Service address

The service access address of a Tencent Cloud API depends on the module. For more information, see the description of each API.

### Communication protocol

Most Tencent Cloud APIs communicate over HTTPS to provide high-security connections.

### Request method

Tencent Cloud APIs support both POST and GET requests. 

> **Notes:**
> 1. POST and GET requests cannot be used together. If the GET method is used, the parameters are obtained from Querystring. If the POST method is used, the parameters are obtained from Request Body, and the parameters in the Querystring are ignored. 
> The request parameters are organized in the same way in both types of requests. Generally, GET method is used. If the parameter strings are too long, POST method is used.
> 2. If the GET method is used, all request parameters need to be URL encoded. This is not required if the POST method is used.

### Request parameters

Two types of parameters are required for each Tencent Cloud API request: common request parameters and API request parameters. Common request parameters are required for every API (see [Common Request Parameters](https://cloud.tencent.com/document/api/213/11650), while API request parameters are specific to each API (see "Request Parameters" in each API document).

### Character encoding

All requests for Tencent Cloud APIs and their responses are encoded using the UTF-8 character set.
