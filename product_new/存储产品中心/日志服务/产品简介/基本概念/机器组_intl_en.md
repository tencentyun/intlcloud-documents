A server group is a list of servers for which logs need to be collected. In server groups, Cloud Log Service manages all servers for which logs are collected using [LogListener](https://intl.cloud.tencent.com/document/product/614/31578).

A server group can contain multiple servers. Generally, service applications of the same type are deployed on multiple servers, and the log collection configuration of these servers are similar. Therefore, you can assign these servers to the same server group, and then associate the server group with the corresponding log topic. You can associate a log topic with multiple server groups, and a server group can be associated with multiple log topics.

To define a server group, add the IP address of a server to the server group. Then, the server group will be able to identify the server using the IP address.
