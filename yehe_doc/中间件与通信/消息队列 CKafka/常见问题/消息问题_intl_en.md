## How do I calculate the number of unconsumed messages?

Number of unconsumed messages = maximum offset - submitted offset, as shown below:

![img](https://main.qcloudimg.com/raw/539e54d9e429f2b0d07f51549a026b62.png)

## Can the message retention period be automatically adjusted?

CKafka allows you to add dynamic message retention policies. After such a policy is set, if the disk utilization reaches the specified percentage, a certain proportion of existing data will automatically expire in case of message surges, helping avoid situations where normal production and consumption stop after the disk space is used up. For detailed directions, please see [Adding Dynamic Message Retention Policy](https://intl.cloud.tencent.com/document/product/597/40211).
