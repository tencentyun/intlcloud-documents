Session persistence can forward requests from the same IP to the same real server. By default, a CLB instance will route requests to different real servers for load balancing; however, you can use session persistence to route requests from a specified user to the same real server, so that some applications that need to hold their session (such as shopping cart) can run properly.

## Layer-4 Session Persistence
Layer-4 protocols (TCP/UDP) support source IP-based session persistence. The session persistence duration can be set to any integer between 30 and 3600 seconds. If the time threshold is exceeded and the session has no new request, the session persistence will end. Session persistence is subject to the load balancing mode:
- In the mode of "weighted round-robin" where requests are distributed based on the weight of real servers, session persistence based on source IP is supported.
- In the mode of "weighted least-connection" where overall scheduling depends on server load and weight, session persistence is not supported.

## Layer-7 Session Persistence
Layer-7 protocols (HTTP/HTTPS) supports session persistence based on cookie insertion (CLB inserts the cookie into the client). The session persistence duration can be set to any value between 30 and 3600 seconds. Session persistence is subject to the load balancing mode:
- In the mode of "weighted round-robin" where requests are distributed based on the weight of real servers, session persistence based on cookie insertion is supported.
- In the mode of "weighted least-connection" where overall scheduling depends on server load and weight, session persistence is not supported.
- The mode of "IP Hash" supports session persistence based on source IP but not on cookie insertion.

## Connection Timeout Period
Currently, HTTP connection timeout period (`keepalive_timeout`) is 75s by default. If you want to adjust it, please enable [custom configuration](https://intl.cloud.tencent.com/document/product/214/32427). If the threshold is exceeded and the session has no data transmission, the connection will be disconnected.
Currently, TCP connection timeout period is 900s by default and cannot be customized. If the threshold is exceeded and the session has no data transmission, the connection will be disconnected.

## Configuring Session Persistence
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the ID of the CLB instance to be configured with session persistence to enter its details page.
2. Select the **Listener Management** tab.
3. Click **Modify** after the CLB listener to be configured with session persistence.
4. Choose whether to enable the session persistence feature. Click the button to enable it, enter the persistence duration, and click **OK**.

## Relationship Between Persistent Connection and Session Persistence

### Scenario 1. HTTP layer-7 business

**Assume a client accesses HTTP/1.1 protocol and `Connection:keep-alive` is configured in the header information. The client accesses CVM via a CLB instance without session persistence enabled. Can the client access the same CVM next time?**

**A:** no.

First, HTTP keep-alive indicates TCP connection remains connected after a request is sent, so the browser can send requests via the same connection. Persistent connection reduces the time required for establishing a new connection for each request and lowers bandwidth consumption. The default timeout period of a CLB cluster is 75s (if there is no new request within 75s, TCP will be disconnected by default).

HTTP keep-alive is established between the client and a CLB instance. If cookie session persistence is disabled, the CLB instance will randomly select a CVM instance according to the polling policy. The previous persistent connection is no longer valid.

Therefore, we recommend you enable session persistence.

If the cookie session persistence period is configured as 1000s, the client will initiate a request again. Because the period between the two requests exceeds 75s, TCP connection needs to be established again. The application layer identifies the cookie and finds the CVM instance the client accessed last time so it will be assessed again this time.

### Scenario 2. TCP layer-4 business
**Assume a client initiates access, TCP is the transport-layer protocol, persistent connection is enabled, but session persistence based on source IP is disabled. Can the same client access the same server in the next access request?**

**A:** not necessarily.

First, according to layer-4 implementation mechanism, when persistent connection is enabled for TCP and not closed, and the same connection is accessed in two requests, then the same client can access the same server. If the connection is closed for some reasons (such as network restart or connection timeout) during the second access request, the request may be scheduled to another real server. The default global timeout period for a persistent connection is 900s, that is, the persistent connection will be released if there is no new request in 900s.
