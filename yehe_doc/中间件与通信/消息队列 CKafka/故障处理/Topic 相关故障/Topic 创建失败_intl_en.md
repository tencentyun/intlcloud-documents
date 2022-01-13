## Issue Description

A topic fails to be created.


## Possible Causes

- The limit of an instance on the total number of topic partitions has been reached.
- The topic is created while one with the same name is being deleted.
- The topic already exists in the cluster.



## Solutions

- **The limit of an instance on the total number of topic partitions has been reached**
Try expanding the Kafka instance or delete unnecessary topics.
![](https://qcloudimg.tencent-cloud.cn/raw/02420c74f53287536ba470820ca40f35.jpg)

- **The topic is created while one with the same name is being deleted**
Topic deletion is an async operation. After the deletion instruction is delivered, the system will delete the topic metadata asynchronously. During this period, if you try to create a topic with the same name as the deleted one, the system will prompt that the topic already exists. In this case, wait about 1 minute and try again later.

- **The topic already exists in the cluster**
If a topic with the same name as the topic you want to create already exists in the cluster, the system will prompt that the topic already exists. In this case, you are recommended to rename the topic.
