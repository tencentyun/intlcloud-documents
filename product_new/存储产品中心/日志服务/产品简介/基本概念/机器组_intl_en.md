A machine group is a list of machines for which logs need to be collected. In machine groups, Cloud Log Service manages all machines for which logs are collected using [LogListener](https://intl.cloud.tencent.com/document/product/614/31578).

A machine group can contain multiple machines. Generally, service applications of the same type are deployed on multiple machines, and the log collection configuration of these machines are similar. Therefore, you can assign these machines to the same machine group, and then associate the machine group with the corresponding log topic. You can associate a log topic with multiple machine groups, and a machine group can be associated with multiple log topics.

To define a machine group, add the IP address of a machine to the machine group. Then, the machine group will be able to identify the machine using the IP address.
