An HTTP status code is a 3-digit code representing the HTTP response status of the webpage server. Such codes are defined by the RFC 2616 standard and further expanded by standards such as RFC 2518, RFC 2817, RFC 2295, RFC 2774, and RFC 4918.

The first digit of a status code represents one of the following five response classes:

1xx: information response, indicating that the request has been received and needs to be further processed
2xx: success response, indicating that the action was successfully received, understood, and accepted
3xx: redirection response, indicating that further action must be taken in order to complete the request
4xx: client error, indicating that the request contains syntax errors or cannot be executed correctly
5xx: server error, indicating that the server cannot properly run a correct request

Below are descriptions of common response return values:

100 - The client must continue to send the request
101 - The client asks the server to switch HTTP protocol versions as requested

200 - The transaction succeeded
201 - The URL of the new file has been known
202 - The request has been accepted for processing, but the processing has not been completed
203 - The returned message is indefinite or incomplete
204 - The request has been received, but the returned message is empty
205 - The server has completed the request, but the user proxy must reset the browsed files
206 - The server has partially completed the user's GET request

300 - The requested resource can be obtained in multiple locations
301 - The request data was deleted
302 - The requested data was found at another address
303 - The client is recommended to visit another URL or use another access method
304 - The client has executed GET, but the file remains unchanged
305 - The requested resource must be obtained from the address specified by the server
306 - This code was used in the previous version of HTTP and has been disused
307 - The requested resource was temporarily deleted

400 - Bad request such as syntax error
401 - The request authorization failed
402 - The valid `ChargeTo` header response is retained
403 - The request is forbidden
404 - No file, query, or URL was found
405 - The method defined by the user in the `Request-Line` field is not allowed
406 - Not acceptable. The requested resource is inaccessible
407 - Similar to 401. The user must be authorized first on the proxy server
408 - The client failed to complete the request within the time specified by the user
409 - The request cannot be completed in the current resource status
410 - This resource is no longer available on the server and there is no reference address
411 - The server rejected the user-defined `Content-Length` attribute request
412 - One or more request header fields are incorrect in the current request
413 - The requested resource is larger than the size allowed by the server
414 - The requested resource URL is longer than the length allowed by the server
415 - The format of the request project is not supported by the requested resource
416 - The request contains the `Range` request header field, but there is no range indication value within the current requested resource, and the request does not contain the `If-Range` request header field
417 - The server does not satisfy the expected value specified in the `Expect` header field of the request. If it is a proxy server, it is possible that the server at the next level cannot fulfill the request

500 - An internal server error occurred
501 - The requested function is not supported by the server
502 - The server is temporarily unavailable, sometimes to prevent system overload
503 - The server is overloaded or down for maintenance
504 - The gateway is overloaded, and the server uses another gateway or service to respond to the user, but the set waiting time is too long
505 - The server does not support or refuses to support the HTTP version specified in the request header
