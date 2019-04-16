[//]: # (chinagitpath:XXXXX)

You can call a Tencent Cloud API by sending a request that include specified request parameters to an API endpoint. A Tencent Cloud API request involves service address, communication protocol, request method, request parameters and character encoding. See below for details.

## Endpoint
The endpoint of a Tencent Cloud API depends on the module. For more information, see the description of each API.

## Communication Protocol
Most Tencent Cloud APIs can be connected through HTTPS, which provides high-security communication tunnels over the network.

## Request Method
Tencent Cloud APIs support both POST and GET requests.

>!
>1. POST and GET requests cannot be used together. A GET request arries request parameter appended in **Querystring**, while a POST request carries request parameter in **Request Body** and ignores the parameters in **Querystring**. The request parameters in both types of requests are formatted in the same way. GET requests are more common than POST requests. However, if the request parameters are too long, we recommend POST requests.
>2. When you send a GET request, all request parameters need to be URL encoded. This is not required for POST requests.
>3. The maximum URL length of GET requests varies by browser and server setting. For example, maximum URL length is 2 KB in traditional IE browsers, while it is 8 KB in Firefox browsers. For API requests with long URL and many parameters, we recommend that you use POST method to prevent request failures from exceeding the maximum length.
>4. The query parameters of POST requests need to be `x-www-form-urlencoded` because the APIs extract query parameters from *$_POST*.

## Request Parameters
Two types of parameters are required for each Tencent Cloud API request: common request parameters and API request parameters. Common request parameters are required for each API (see [Common Request Parameters](https://cloud.tencent.com/document/product/1014/31224)), while API request parameters are unique to each API (see "Request Parameters" in each API document)

## Character Encoding
All requests sent to Tencent Cloud APIs and their responses are UTF-8 encoded.

