### Does CKafka support public network access?
Currently, CKafka transfers data over the private network by default. To access over the public network, you need to activate a public network route separately. For detailed directions, please see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555). The maximum public network bandwidth of one broker is 1 MB/s. As public network access runs the risk of issues such as delay and network environment security, we do not recommend long-term use of public network transfer.

