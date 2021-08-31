A CLB instance can periodically send `Ping` commands to real servers, attempt to connect with or send requests to them to check their running status. These are called "health check". It uses health checks to determine the availability of real servers and prevent exceptional real servers from affecting frontend services, thereby improving overall service availability.
- If a real server is confirmed as exceptional, the CLB instance will automatically distribute new requests to other normal servers instead of forwarding them to the exceptional server; after the exceptional server returns to the normal state, the CLB instance will automatically restore its service and distribute new requests to it again.
- After health check is enabled, regardless of the weights of real servers (including 0), the CLB instance will always perform health check.
- An auto scaling group will periodically use a similar method to check the running status of each instance in the group. For more information, please see [Auto Scaling](https://intl.cloud.tencent.com/document/product/377).

## Health Check Configuration for Layer-4 Forwarding
The health check mechanism for layer-4 forwarding is as follows: CLB initiates an access request to the server port specified in the configuration. If access to the port is normal, the real server is considered healthy. Otherwise, it is considered unhealthy.
For TCP business, SYN packets are used for health check. For UDP business, the ping command is used.

| Health Check Configuration    | Description                    | Default Value                               |
| ------- | ------------------------ | ---------------------------------------- |
| Response timeout period | <li>Maximum response timeout period for health check.</li><li>If a real server fails to respond properly within the timeout period, it is considered as having an exception.</li><li>Value range: 2–60s.</li> | 2s |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5–300s. </li> | 5s |
| Unhealthy threshold | <li>If the health check results received are failures for n times (n is the entered number) in a row, the real server will be considered as unhealthy, and the status displayed in the console will be **unhealthy**.</li><li>Value range: 2–10.</li> | 3 times |
| Healthy threshold | <li>If the health check results received are successes for n times (n is the entered number) in a row, the real server will be considered as healthy, and the status displayed in the console will be **healthy**.</li><li>Value range: 2–10.</li> | 3 times |

## Health check configuration for Layer-7 forwarding

The health check mechanism for layer-7 forwarding is as follows: CLB sends an HTTP request to the real server for health check. CLB determines whether the server is healthy based on the HTTP return value. For example, assume HTTP return values include `http_1xx`, `http_2xx`, `http_3xx`, `http_4xx` and `http_5xx`, users can define `http_1xx` and `http_2xx` as normal status based on their business needs, and configure `http_3xx` to `http_5xx` as unhealthy status.

| Health Check Configuration    | Description                    | Default Value                                |
| ------- | ------------------------ | ---------------------------------------- |
| Check domain name | Health check domain name: <ul style="margin-bottom:0px;"><li>It can contain 1–80 characters. </li><li>It is the forwarded domain name by default. </li><li>Regex is not supported. If your forwarded domain name is a wildcard domain name, you should specify a fixed one (non-regex) as the health check domain name. </li><li>Supported characters: `a–z`, `0–9`, `.`, `-`. </li></ul> | Forwarded domain name |
| Check path | Health check path: <ul style="margin-bottom:0px;"><li>It can contain 1–200 characters. </li><li>It is `/` by default and must begin with `/`. </li><li>Regex is not supported. You are recommended to specify a fixed URL path (static page) for health checks. </li><li>Supported characters: `a–z`, `A–Z`, `0–9`, `.`, `-`, `_`, `/`, `=`, `?`. </li></ul>  | `/` |
| Check interval | <li>Interval between two health checks.</li><li>Value range: 5–300s. </li> | 5s |
| Unhealthy threshold | <li>If the health check results received are failures for n times (n is the entered number) in a row, the real server will be considered as unhealthy, and the status displayed in the console will be **unhealthy**.</li><li>Value range: 2–10.</li> | 3 times |
| Healthy threshold | <li>If the health check results received are successes for n times (n is the entered number) in a row, the real server will be considered as healthy, and the status displayed in the console will be **healthy**.</li><li>Value range: 2–10.</li> | 3 times |
| HTTP request method | HTTP request method for health checks. Valid values: GET, HEAD. <ul style="margin-bottom:0px;"><li>If HEAD is used, the server will only return the HTTP header, which can reduce backend overheads and improve request efficiency. The corresponding real server must support HEAD.</li><li>If GET is used, the real server must support GET.</li></ul> | GET |
| HTTP status code check | If the status code is the selected one, the real server is considered alive (healthy). Valid values: http_1xx, http_2xx, http_3xx, http_4xx, http_5xx. | http_1xx, http_2xx, http_3xx, http_4xx |

## Health Check Status
According to the health check detection conditions, the health check status of a real server may be one of the following four options:

| Status | Description | Whether to Forward Traffic |
| ------- | ----------- | ---------------- |
| Detecting | This is the state of the newly bound real server during the period of check interval * healthy threshold; for example, if the check interval is 2 seconds and the health threshold is 3 times, this will be state within 6 seconds. | CLB does not forward traffic to the real server in "detecting" status. |
| Healthy | The real server is normal. | CLB forwards traffic to the "healthy" real server. |
| Exceptional | The real server is exceptional. | <li>CLB does not forward traffic to "exceptional" real servers. </li><li>Under a layer-4 listener or layer-7 URL rule, if CLB detects that all real servers are unhealthy, it will activate the all-dead-all-alive logic, that is, requests will be forwarded to all real servers. </li>|
| Disabled | Health check has been disabled. | CLB forwards traffic to the real server. |
>!If you disable health check, CLB will forward traffic to all real servers (including exceptional ones). Therefore, we strongly recommend you enable health check to allow CLB to automatically check for and remove exceptional real servers for you.

## How to Troubleshoot Health Check Issues
If an exception is detected during health check, it can be checked from various aspects such as real server bandwidth, layer-4 listener, and layer-7 protocol. For specific troubleshooting directions, please see [Troubleshooting Health Check Issues](https://intl.cloud.tencent.com/document/product/214/3394)
