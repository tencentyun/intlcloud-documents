Session persistence can forward requests from the same IP to a single real server. By default, a CLB instance will route requests to different real server instances for load balancing. However, you can use session persistence to route requests from a specified user to the same real server instance. This enables applications that require session persistence (such as shopping cart) to run properly.
For more information on session persistence, please see [How Session Persistence Works](https://intl.cloud.tencent.com/document/product/214/2736).

## Layer-4 session persistence
The Layer-4 protocol (TCP/UDP) supports session persistence based on a source IP. The duration of session persistence can be set to any integer between 30 and 3,600 seconds. Beyond this time threshold, a session will be disconnected in case of no new request. This feature varies for different load balancing modes:
- In the mode of "weighted polling" where requests are distributed based on the weight of real servers, session persistence based on source IPs is supported.
- In the mode of "weighted minimum number of connections" where overall scheduling depends on server load and weight, session persistence is not supported.

## Layer-7 session persistence
The Layer-7 protocol (HTTP/HTTPS) supports session persistence based on cookie insertion (CLB inserts the cookie into the client). The session persistence duration can be set to any value between 30 and 3,600s. This feature varies for different load balancing modes:
- In the mode of "weighted polling" where requests are distributed based on the weight of real servers, session persistence based on cookie insertion is supported.
- In the mode of "weighted minimum number of connections" where overall scheduling depends on server load and weight, session persistence is not supported.
- The mode of "IP Hash" supports session persistence based on source IPs, but not on cookie insertion.

## Connection timeout
The period of HTTP connection timeout (`keepalive_timeout`) is 75s by default. If you want to adjust it, please enable [Custom Configuration](https://intl.cloud.tencent.com/document/product/214/32427). When this threshold is exceeded and no data transmitted during a session, it will be disconnected.
The period of TCP connection timeout is 900s by default and cannot be customized for the time being. If this threshold is exceeded and no data transmitted during a session, it will be disconnected.

## Configuring session persistence
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the ID of the CLB instance to be configured with session persistence to enter its details page.
2. Select the **Listener Management** tab.
3. Click **Modify** after the CLB listener to be configured with session persistence.
4. Choose whether to enable the session persistence feature. Click the button to enable it, enter the persistence duration, and click **OK**.

## Relationship between persistent connection and session persistence

### Scenario 1: HTTP Layer-7 business

**Assume a client accesses HTTP/1.1 protocol with `Connection:keep-alive` configured in the header, and the client accesses a backend CVM via CLB without session persistence enabled. Can the client access the same CVM next time?**

**A:** no.

First, HTTP keep-alive indicates TCP connection remains connected after a request is sent, so the browser can send requests via the same connection. Persistent connection reduces the time required for establishing a new connection for each request and lowers bandwidth consumption. The default timeout period of a CLB cluster is 75s (if there is no new request within 75s, TCP will be disconnected by default).

HTTP keep-alive is established between the client and CLB. If cookie session persistence is disabled, the CLB will randomly select a backend CVM according to the polling policy for your access next time. The previous persistent connection is no longer valid.

Therefore, we recommend you enable session persistence.

If the cookie session persistence duration is configured as 1,000s, the client will initiate a request again. Because the interval between the two requests exceeds 75s, TCP connection needs to be established again. The application layer identifies the cookie and finds the CVM the client accessed last time so it will be assessed again.

### Scenario 2: Layer-4 TCP business
**Assume a client initiates access, TCP is the transport-layer protocol, persistent connection is enabled, but session persistence based on source IP is disabled. Can the same client access the same server in the next access request?**

**A:** not necessarily.

First, according to Layer-4 implementation mechanism, when persistent connection is enabled for TCP and not closed, and the same connection is accessed in two requests, then the same client can access the same server. If the connection is closed for some reasons (such as network restart or connection timeout) during the second access request, the request may be scheduled to another real server. The default global timeout period for a persistent connection is 900s, that is, the persistent connection will be released if there is no new request in 900s.
