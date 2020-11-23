For instance of **public network CLB or public network CLB with fixed IP**, Gzip compression is enabled for **HTTP and HTTPS** protocols by default. Gzip feature compresses websites, which effectively reduces data volume in network transmission and speeds up access of client browser. Pay attention to the following:

### Notes

- **You must enable Gzip compression on CVM instances in sync**
For common Nginx service containers, you must enable Gzip in their configuration files (nginx.conf by default) and restart the service
```
gzip on;
```
- **Currently, CLB supports the following file types. You can specify the file type for compression in the gzip_types configuration item**
```
application/atom+xml application/javascript application/json application/rss+xml application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/svg+xml image/x-icon text/css text/plain text/x-component;
```
>You must enable Gzip in sync for the above file types in the business software of CVM instances of CLB.
- **The client requests must carry the compression request identifier**
To enable Gzip compression, the client requests must carry the following identifier:
```
Accept-Encoding: gzip,deflate,sdch
```

### Example of enabling Gzip on CVM Instances

Example of CVM runtime environment: Debian 6

1. Use Vim to open the Nginx configuration file based on the user path:
```
vim /etc/nginx/nginx.conf
```
2. Find the following code:
```
gzip on;
gzip_min_length 1k;
gzip_buffers 4 16k;
gzip_http_version 1.1;
gzip_comp_level 2;
gzip_types text/html application/json;
```
Description of the above code syntax:
	- gzip: whether to enable or disable Gzip module.
Syntax: `gzip on/off`
Scopes: http, server, location
	
	- gzip_min_length: specifies the minimum number of bytes that a page can be compressed to. The number of bytes can be obtained from Content-Length in the HTTP header. Default value is 1k.
Syntax: `gzip_min_length length`
Scopes: http, server, location
	
	- gzip_buffers: specifies the unit of buffer for storing the data stream of the Gzip compression result. 16k means 16k is used as the unit, and memory 4 times the original data size (in 16k) will be applied for.
Syntax: `gzip_buffers number size`
Scopes: http, server, location
	
	- gzip_http_version: specifies the lowest HTTP version that can use Gzip. Configure HTTP/1.0 means the lowest HTTP version that needs Gzip is 1.0, so Gzip can be compatible with HTTP/1.1 or higher. You do not need to change this since Tencent Cloud supports HTTP/1.1 across the entire network.
Syntax: `gzip_http_version 1.0 | 1.1;`
Scopes: http, server, location

	- gzip_comp_level: specifies the Gzip compression ratio with value range: 1–9. 1 is the smallest compression ratio with the fastest processing speed, while 9 is the greatest compression ratio with the slowest processing speed (fast transmission with high CPU consumption).
Syntax: `gzip_comp_level 1..9`
Scopes: http, server, location

	- gzip_types: indicates the Multipurpose Internet Mail Extensions (MIME) types for compression, and "text/html" type will be compressed by default. In addition, Gzip for Nginx does not compress static resource files such as JavaScript and images by default. You can configure gzip_types to specify MIME types to be compressed. Types that are not specified will not be compressed. **For example, to compress data in JSON format, you need to add application/json to this sentence**
The supported types are below:
```
text/html text/plain text/css application/x-javascript text/javascript application/xml
```
Syntax: `gzip_types mime-type [mime-type ...]`
Scopes: http, server, location

3. To modify the configuration, save and exit the file, enter the Nginx bin file directory, and run the following command to reload Nginx:
```
./nginx -s reload
```
4. Use curl command to test whether Gzip has been successfully enabled:
```
curl -I -H "Accept-Encoding: gzip, deflate" "http://cloud.tencent.com/example/"
```
