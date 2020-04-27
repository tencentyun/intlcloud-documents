### What should I do if the following exception is thrown when I perform computing tasks: com.qcloud.cos.exception: CosServiceException: Reduce your request rate. (Status Code: 503; Error Code: SlowDown; Request ID: NWXXXXXXXXXX)?

As big data computing tasks usually read COS bucket data in parallel, they are likely to trigger a limit action on access frequency. By default, COS puts a 1,200 QPS limit on each account. To ensure your tasks run properly, we recommend you configure a greater value for `fs.cosn.maxRetries` to increase the maximum number COS can retry.

### What should I do if the following exception is thrown when I perform computing tasks: java.net.ConnectException: Cannot assign requested address (connect failed) (state=42000,code=40000)?

Generally, when this exception occurs, you have established too many short TCP connections in a short period of time. After the connections are closed, local ports will enter a 60-second timeout period by default instead of being immediately repossessed. As a result, there is no available port during this period for your Client to establish a socket connection with the Server.

To fix this problem, you can modify the `/etc/sysctl.conf` file with changes to the following kernel parameters:
```conf
net.ipv4.tcp_timestamps = 1     #Enables support for TCP timestamp
net.ipv4.tcp_tw_reuse = 1       #Supports the use of a socket in the status of TIME_WAIT to new TCP connection
net.ipv4.tcp_tw_recycle = 1     #Enables quick repossession of a socket in the status of TIME-WAIT
net.ipv4.tcp_syncookies=1       #Enables SYN Cookies. The default value is 0. When SYN waiting queue overflows, cookies are enabled to prevent a small number of SYN attacks.
net.ipv4.tcp_fin_timeout = 10              #Waiting time after the port is released.
net.ipv4.tcp_keepalive_time = 1200           #The interval for TCP to send KeepAlive messages. The default value is 2 hours. Change it to 20 minutes.
net.ipv4.ip_local_port_range = 1024 65000    #The range of ports for external connections. The default value is 32768 to 61000. Change it to 1024 to 65000.
net.ipv4.tcp_max_tw_buckets = 10240          #The maximum number (default: 180000) of sockets in TIME_WAIT status. Exceeding this number will directly release all the new TIME_WAIT sockets. You may consider reducing this parameter for a smaller number of sockets in TIME_WAIT status.
```

