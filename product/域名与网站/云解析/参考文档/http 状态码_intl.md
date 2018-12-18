## 1xx: Informational

This type of status codes represent temporary responses. The client should be prepared to receive one or more 1xx responses before receiving a regular response.

| HTTP status code | Description |
| ----------- | ---------- |
| 100 | Continue.     |
| 101 | Switching protocols. |

## 2xx: Successful

This type of status codes indicate that the server has successfully accepted the client's request.

| HTTP status code | Description |
| ----------- | ------------------------------------------------------------ |
| 200 | OK. The client request has succeeded.                                     |
| 201 | Created.                                                     |
| 202 | Accepted.                                                     |
| 203 | Non-authoritative information |
| 204 | No content.                                                     |
| 205 | Reset content.                                                   |
| 206 | Partial content. This indicates that a file has been partially downloaded. The interrupted download can be resumed or split into multiple concurrent streams. |
| 207 | Multi-status (WebDAV). There should be an XML message before this message, which may contain several separate response codes, subject to the number of sub-requests sent. |

## 3xx: Redirection

The client browser must take additional actions to complete the request. For example, the browser may have to request a different page on the server or repeat the request through a proxy server.

| HTTP status code | Description |
| ----------- | ------------------------------------------------------------ |
| 301 | Moved permanently. This request and all subsequent requests should be redirected to the specified URI.     |
| 302 | Object already moved. For form-based authentication, this message is usually expressed as "object moved." The requested resource temporarily resides in a different URI. Since the redirection may change sometimes, the client should continue to use the RequestURI when it makes requests in the future. This response can only be cached if indicated in the CacheControl or Expires header fields. |
| 304 | Not modified. The document requested by the client is already in its cache and the document has not been modified since it was cached. The client uses a cached copy of the document instead of downloading the document from the server. |
| 307 | Temporary redirect.                                                 |

## 4xx: Client Errors

An error occurred and the client seems to have problems. For example, the client requested a page that does not exist or the client didn't provide valid authentication information.

| HTTP status code | Description |
| ----------- | ------------------------------------------------------------ |
| 400 | Bad request.                                                 |
| 401 | Unauthorized. IIS defines several different 401 errors to indicate a more specific cause of the error. These specific error codes are displayed in the browser but not in the IIS log. For details, see [Status Code 401](#401). |
| 403 | Forbidden. If the website doesn't have a default document set and is not set to allow directory browsing, you will receive this generic 403 status code. IIS defines several different 403 errors to indicate a more specific cause of the error. For details, see [Status Code 403](#403). |
| 404 | Not found. This error occurs because the file you are trying to access has been removed or deleted. This error can also occur if you try to access a file with a limited extension after installing the URLScan tool. If you have the URIScan tool installed, you will see "Rejected by URLScan" in the w3svc log file. In this case, "Rejected by URLScan" will appear in the log file entry of the request. IIS defines several different 404 errors to indicate a more specific cause of the error. For details, see [Status Code 404](#404). |
| 405 | The HTTP verb used to access this page is not allowed (method is not allowed). This error occurs when the client sends an HTTP request to the server running IIS and the request contains an HTTP verb that the server cannot recognize. To fix this error, make sure that the client's request uses an HTTP RFC-compatible HTTP verb. |
| 406 | The client browser doesn't accept the MIME type of the requested page.                   |
| 407 | Proxy authentication required.                                       |
| 412 | Precondition failed.                                               |
| 413 | Request entity too large.                                               |
| 414 | Request URI too long.                                              |
| 415 | Unsupported media type.                                           |
| 416 | Request range not satisfiable.                                         |
| 417 | Execution failed.                                                   |
| 423 | Locked.                                                 |

<a id="401"></a>

### Status Code 401

| HTTP status code | Description |
| ----------- | ------------------------------------------------------------ |
| 401.1 | Logon failed due to invalid username or password.                               |
| 401.2 | Logon failed due to server configuration.                                     |
| 401.3 | Unauthorized due to ACL on resource. This indicates that there is a problem with NTFS permissions. This error may occur even if you have the appropriate permissions to the file you are trying to access. For example, if the IUSR account doesn't have access to the C:WinntSystem32Inetsrv directory, you will see this error. |
| 401.4 | Authorization failed by filter.                                             |
| 401.5 | Authorization failed by ISAPI/CGI application.                                 |
| 401.7 | Access denied by URL authorization policy on the Web server. This error code is specific to IIS 6.0. |

<a id="403"></a>

### Status Code 403

| HTTP status code | Description |
| ----------- | ------------------------------------------------------------ |
| 403.1 | Execute access forbidden. Possible causes: <br><li>You do not have enough Execute permissions. For example, you may receive this error message if you try to access an ASP page in a directory where permissions are set to None, or you try to execute a CGI script in a directory with Scripts Only permissions. To modify the Execute permission, right-click the directory in the Microsoft Management Console (MMC), click "Properties" and the "Directory" tab, and make sure that you have set the appropriate Execute permission for the content you are trying to access. <li>The script mapping for the file type that you are trying to execute is not set up to recognize the verb that you are using (for example, GET or POST). To verify this, right-click the directory in MMC, click "Properties", the "Directory" tab and "Configuration", and verify that the script mapping for the appropriate file type is set to allow the verb used. |
| 403.2 | Read access denied. Verify that the IIS is granted Read access to the directory. Also, if you are using a default document, verify that the document exists. |
| 403.3 | Write access denied. Verify that the IIS and NTFS are granted Read access to the directory. |
| 403.4 | SSL required. Disable the option that requires a secure channel, or use HTTPS instead of HTTP to access the page. |
| 403.5 | SSL 128 required. Disable the option that requires 128-bit encryption, or use a browser that supports 128-bit encryption to view the page. |
| 403.6 | IP address rejected. You have configured the server to deny access to your current IP address. |
| 403.7 | Client certificate required. You have configured the server to require a certificate for client authentication, but you do not have a valid client certificate installed. |
| 403.8 | Site access denied. You have set a domain name restriction for the domain used to access the server.   |
| 403.9 | Too many users. The number of users who are connected to the server exceeds the connection limit. Note: Microsoft Windows 2000 Professional and Windows XP Professional automatically set a limit of up to 10 connections on IIS. You cannot change this limit. |
| 403.10 | Invalid configuration.                                                   |
| 403.11 | Password change.                                                   |
| 403.12 | Mapping table denied access. The page you are trying to access requires a client certificate. However, the user ID mapped to the client certificate has denied access to the file. |
| 403.13 | Client certificate revoked.                                           |
| 403.14 | Directory listing rejected.                                               |
| 403.15 | Client access license exceeded.                                         |
| 403.16 | Client certificate is untrusted or invalid.                                   |
| 403.17 | Client certificate has expired or is not yet valid.                                 |
| 403.18 | Cannot execute requested URL in the current application pool. This error code is specific to IIS 6.0. |
| 403.19 | Cannot execute CGIs for the client in this application pool. This error code is specific to IIS 6.0. |
| 403.20 | Passport logon failed. This error code is specific to IIS 6.0.           |

<a id="404"></a>

### Status Code 404

| HTTP status code | Description |
| ----------- | ------------------------------------------------------------ |
| 404.0 | File or directory not found.                                         |
| 404.1 | Website not accessible on the requested port. This error message indicates that the IP address of the website you are trying to access does not accept requests from the port used for this request. |
| 404.2 | Web service extension lockdown policy prevents this request. In IIS 6.0, this indicates that the request is prevented in the list of Web service extensions. |
| 404.3 | MIME map policy prevents this request. This issue occurs if the following conditions exist: <li>The handler mapping for the requested file extension is not configured. <li>The corresponding MIME type is not configured for the website or application. |

## 5xx: Server Errors

The server cannot complete the request due to an error.

| HTTP status code | Description |
| ----------- | ------------------------------------------------------------ |
| 500 | Internal server error. A wide variety of server-side errors may cause this error message. The event viewer log contains a more detailed error cause. In addition, you can disable friendly HTTP error message in order to receive detailed error description. IIS defines several different 500 errors to indicate a more specific cause of the error. For details, see [Status Code 500](#500). |
| 501 | Header values specify a configuration that is not implemented.                                   |
| 502 | Web server received an invalid response while acting as a gateway or proxy. This error message occurs if the CGI script that you are trying to run does not return a valid set of HTTP headers. To fix this error, you must debug the CGI application to determine why it passes invalid HTTP information to IIS. IIS defines several different 502 errors to indicate a more specific cause of the error. For details, see [Status Code 502](#502). |
| 503 | Service unavailable. This error code is specific to IIS 6.0. Starting from IIS 6.0, the kernel-mode Http.sys component generates an HTTP 503 state. |
| 504 | Gateway timeout.                                                   |
| 505 | HTTP version not supported.                                          |

<a id="500"></a>

### Status Code 500

| HTTP status code | Description |
| ----------- | ------------------------------------------------------------ |
| 500.12 | Application is busy restarting on the Web server. This indicates that you tried to load an ASP page while IIS was restarting the application. This message will disappear when the page is refreshed. If the message appears again after the page is refreshed, it may be caused by antivirus software that is scanning your configuration file. |
| 500.13 | Web server is too busy.                                             |
| 500.15 | Direct requests for Global.asa are not allowed.                                  |
| 500.16 | UNC authorization credentials incorrect. This error code is specific to IIS 6.0.          |
| 500.18 | URL authorization store cannot be opened. This error code is specific to IIS 6.0.     |
| 500.19 | The data for this file is not configured correctly in the metabase. You will receive this error if the XML metabase contains invalid configuration information in the content type you are trying to access. To fix this error, remove or correct the invalid configuration. This error usually indicates a problem in the ScriptMap metabase key. |
| 500.100 | Internal ASP error. This error message occurs if the ASP page you are trying to load has errors in the code. To get a more accurate error message, disable friendly HTTP error message. By default, this error message is only enabled on the default website. |

<a id="502"></a>

### 502 Status Code

| HTTP status code | Description |
| ----------- | ------------------ |
| 502.1 | CGI application timeout. |
| 502.2 | Error in CGI application. |

 
