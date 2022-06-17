>! If there are problems with backend adaptation you cannot fix, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.


## Step 1: Create a TCP Listener and Enable Proxy Protocol

Only layer-4 TCP allows Proxy Protocol to obtain the client real IP. Please enable Proxy Protocol in the acceleration connection as follows:

Log in to the [GAAP console](https://console.cloud.tencent.com/gaap). Select **Access Management** > **TCP/UDP Listener Management**. Click **Create** to add a TCP listener and select TOA, and then complete configurations required to create the listener and connection.
![]()

## Step 2: Adapt Proxy Protocol on the Backend Server

Both Nginx and HaProxy support Proxy Protocol.
For example, to configure Proxy Protocol in Nginx, you only need to add the parameter `proxy_protocol` to listen directive in a server block as follows:

```
http {
    #...
    server {
        listen 80   proxy_protocol;
        listen 443  ssl proxy_protocol;
        #...
    }
}
```

For programs that do not support Proxy Protocol, after the TCP connection is set up, you need to parse the Proxy Protocol text string as follows to obtain the client IP:

```
PROXY TCP4 1.1.1.2 2.2.2.2 12345 80\r\n
```


## Step 3: View the Client IP

You can directly check the client IP in nginx logs. The log path is "/var/log/nginx/access.log".

You can also get the client IP with the command `nc -l port`.

![](https://qcloudimg.tencent-cloud.cn/raw/9a5326eb6c60fca084f625199098edbf.png)
