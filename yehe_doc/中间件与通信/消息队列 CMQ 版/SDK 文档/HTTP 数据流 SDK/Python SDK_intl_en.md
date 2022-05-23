## Directions

This document uses the SDK for Python as an example to describe how to connect the client to TDMQ for CMQ and send/receive messages.

## Prerequisites

- [You have installed Python.](https://www.python.org/downloads/)
- [You have installed pip.](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [You have downloaded the demo.](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-python-sdk-demo.zip)

## Queue Model
### Directions
1. Create a queue in the console as instructed in [Queue Management](https://intl.cloud.tencent.com/document/product/1111/42994).
<dx-alert infotype="explain" title="">
You can create a message queue in the console or via TencentCloud API. To use TencentCloud API, you need to install the SDK for Python.
</dx-alert>
<dx-codeblock>
:::  shell
 pip install --upgrade tencentcloud-sdk-python
:::
:::  python
# API authentication information
cred = credential.Credential(SecretId, SecretKey)
httpProfile = HttpProfile()
httpProfile.endpoint = NameServerAddress

clientProfile = ClientProfile()
clientProfile.httpProfile = httpProfile
# Create the TDMQ client
client = tdmq_client.TdmqClient(cred, "ap-guangzhou", clientProfile)

# Create CMQ queue request parameters
req = models.CreateCmqQueueRequest()
params = {
	 "QueueName": "queue_api",
	 # Below is the dead letter queue configuration
	 "DeadLetterQueueName": "dead_queue_api",  # Dead letter queue, which needs to be created first
	 "Policy": 0,  # 0: Message has been consumed multiple times but not deleted. 1: `Time-To-Live` has elapsed
	 "MaxReceiveCount": 3  # Maximum receipts. Value range: 1–1000
}
req.from_json_string(json.dumps(params))

# Create a CMQ message queue
resp = client.CreateCmqQueue(req)
:::
</dx-codeblock>
<table>
<thead>
<tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr><td >NameServerAddress</td><td >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/19d35ff376f2ce5e97424d1b0b24a520.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td >SecretId, SecretKey</td><td >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/48360df81a3ffdbe60fada488d370009.png" referrerpolicy="no-referrer" alt="img"></td></tr></tbody>
</table>
2. Import [CMQ files](https://github.com/tencentyun/cmq-python-sdk) into the project. You need to select a branch based on the used Python version. The default SDK is for Python 2, and you can switch to the Python 3 branch to view the SDK for Python 3.
3. Send messages.
<dx-codeblock>
:::  python
import os
import sys

sys.path.insert(0, os.path.dirname(os.path.abspath(__file__)) + "/..")

import logging
from cmq.account import Account
from cmq.queue import Message
from cmq.cmq_exception import CMQExceptionBase

# `secretId` and `secretKey` of your Tencent Cloud account, which should be kept confidential
# You can get them at https://console.intl.cloud.tencent.com/cam/capi
secretId = 'AKIDSiiRtxxxx'
secretKey = 'GGzSeaM5xxxx'
# CMQ service call address
nameServerAddress = 'https://cmq-gz.public.tencenttdmq.com'

# Initialize `my_account` and `my_queue`
# Account class objects are not thread-safe. If you need to use them in multiple threads, initialize them for each thread
my_account = Account(nameServerAddress, secretId, secretKey, debug=True)
my_account.set_log_level(logging.DEBUG)
# Message queue name
queue_name = sys.argv[1] if len(sys.argv) > 1 else "python_queue"
my_queue = my_account.get_queue(queue_name)

try:
	 # Message content
	 msg_body = "I am test message."
	 msg = Message(msg_body)
	 # Send messages
	 re_msg = my_queue.send_message(msg)
	 # Sending result
	 print("Send Message Succeed! MessageBody:%s MessageID:%s" % (msg_body, re_msg.msgId))
except CMQExceptionBase as e:
	 print("Send Message Fail! Exception:%s\n" % e)
:::
</dx-codeblock>
<table>
<thead>
<tr><th style='text-align:left;' >Parameter</th><th style='text-align:left;' >Description</th></tr></thead>
<tbody><tr><td style='text-align:left;' >NameServerAddress</td><td style='text-align:left;' >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/5a703690d73b627fdd399a334a55791b.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >SecretId, SecretKey</td><td style='text-align:left;' >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/923788b175aae92828c13577b2b213fe.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >queue_name</td><td style='text-align:left;' >Queue name, which can be obtained on the <strong>Queue Service</strong> page in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>.</td></tr></tbody>
</table>
4. Consume messages.
<dx-codeblock>
:::  python
import os
import sys

sys.path.insert(0, os.path.dirname(os.path.abspath(__file__)) + "/..")

import logging
from cmq.account import Account
from cmq.cmq_exception import CMQExceptionBase

# `secretId` and `secretKey` of your Tencent Cloud account, which should be kept confidential
# You can get them at https://console.intl.cloud.tencent.com/cam/capi
secretId = 'AKIDSiiRtxxxx'
secretKey = 'GGzSeaM5xxxx'
# CMQ service call address
nameServerAddress = 'https://cmq-gz.public.tencenttdmq.com'

# Initialize `my_account` and `my_queue`
# Account class objects are not thread-safe. If you need to use them in multiple threads, initialize them for each thread
my_account = Account(nameServerAddress, secretId, secretKey, debug=True)
my_account.set_log_level(logging.DEBUG)
queue_name = sys.argv[1] if len(sys.argv) > 1 else "python_queue"
my_queue = my_account.get_queue(queue_name)

try:
	 wait_seconds = 3
	 # Obtain messages
	 recv_msg = my_queue.receive_message(wait_seconds)
	 # Specific business
	 print("Receive Message Succeed! ReceiptHandle:%s MessageBody:%s MessageID:%s" % (
			 recv_msg.receiptHandle, recv_msg.msgBody, recv_msg.msgId))
	 # Successfully consumed messages are deleted
	 my_queue.delete_message(recv_msg.receiptHandle)
except CMQExceptionBase as e:
	 print("Receive Message Fail! Exception:%s\n" % e)
:::
</dx-codeblock>
<table>
<thead>
<tr><th style='text-align:left;' >Parameter</th><th style='text-align:left;' >Description</th></tr></thead>
<tbody><tr><td style='text-align:left;' >NameServerAddress</td><td style='text-align:left;' >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/bce053dd67c070032601f936813e8ec6.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >SecretId, SecretKey</td><td style='text-align:left;' >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/5546831d3386dd37352e0c54ac8da52b.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >queue</td><td style='text-align:left;' >Queue name, which can be obtained on the <strong>Queue Service</strong> page in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>.</td></tr></tbody>
</table>

## Topic Model
### Directions
1. Prepare the required resources and create a topic subscription and a subscriber.
   1. Create a topic subscription in the console or via TencentCloud API. To use TencentCloud API, you need to install the SDK for Python.
   <dx-codeblock>
   :::  python
# API authentication information
cred = credential.Credential(SecretId, SecretKey)
httpProfile = HttpProfile()
httpProfile.endpoint = NameServerAddress

clientProfile = ClientProfile()
clientProfile.httpProfile = httpProfile
client = tdmq_client.TdmqClient(cred, "ap-guangzhou", clientProfile)

req = models.CreateCmqTopicRequest()
params = {
		"TopicName": "topic_api",  # Topic name, which must be unique in the same region under the same account
		"FilterType": 1,  # Used to specify the message match policy for the topic. 1: Tag matching policy. 2: Routing matching policy
		"MsgRetentionSeconds": 86400  # Message retention period. Value range: 60–86400 seconds (i.e., 1 minute–1 day)
}
req.from_json_string(json.dumps(params))

# Create a topic
resp = client.CreateCmqTopic(req)
:::
</dx-codeblock>
<table>
<thead>
<tr><th style='text-align:left;' >Parameter</th><th style='text-align:left;' >Description</th></tr></thead>
<tbody><tr><td style='text-align:left;' >NameServerAddress</td><td style='text-align:left;' >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/d3d39cd56e77a4c10cb66915033164f2.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >SecretId, SecretKey</td><td style='text-align:left;' >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/beb94c56768d9e1189e4d7115015dfd6.png" referrerpolicy="no-referrer" alt="img"></td></tr></tbody>
</table>
   2. Create a subscriber in the console or via TencentCloud API. To use TencentCloud API, you need to install the SDK for Python.
<dx-codeblock>
:::  python
# API authentication information
cred = credential.Credential(SecretId, SecretKey)
httpProfile = HttpProfile()
httpProfile.endpoint = NameServerAddress

clientProfile = ClientProfile()
clientProfile.httpProfile = httpProfile
client = tdmq_client.TdmqClient(cred, "ap-guangzhou", clientProfile)

req = models.CreateCmqSubscribeRequest()
params = {
		"TopicName": "topic_api",  # Name of the topic for which to create a subscription
		"SubscriptionName": "sub",  # Subscription name
		"Protocol": "queue",  # Subscription protocol. Currently, two protocols are supported: HTTP and queue. To use the HTTP protocol, you need to build your own web server to receive messages. With the queue protocol, messages are automatically pushed to a CMQ queue and you can pull them concurrently.
		"Endpoint": "topic_queue_api",   # Endpoint that receives notifications, which varies by protocol: for HTTP, the endpoint must start with `http://`, and the `host` can be a domain or IP; for queue, `QueueName` should be entered.
		"NotifyStrategy": "BACKOFF_RETRY",  # CMQ push server retry policy. Valid values: 1) BACKOFF_RETRY; 2) EXPONENTIAL_DECAY_RETRY.
		"FilterTag": ["TAG"],  # Message filter tag (used for message filtering). The number of tags cannot exceed 5.
		# "BindingKey": ["a.b.c"],  # The number of `BindingKey` cannot exceed 5, and the length of each `BindingKey` cannot exceed 64 bytes. This field indicates the filtering policy for subscribing to and receiving messages.
		"NotifyContentFormat": "SIMPLIFIED"  # Push content format. Valid values: 1. JSON; 2. SIMPLIFIED, i.e., the raw format. If `Protocol` is `queue`, this value must be `SIMPLIFIED`. If `Protocol` is `http`, both options are acceptable, and the default value is `JSON`.
}
req.from_json_string(json.dumps(params))

# Create a subscription
resp = client.CreateCmqSubscribe(req)
:::
</dx-codeblock>
<dx-alert infotype="notice" title="">
`BindingKey` and `FilterTag` should be set according to the type of subscribed topic; otherwise, they will be invalid.
</dx-alert>
<table>
<thead>
<tr><th style='text-align:left;' >Parameter</th><th style='text-align:left;' >Description</th></tr></thead>
<tbody><tr><td style='text-align:left;' >NameServerAddress</td><td style='text-align:left;' >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/6fe68a1aa40ec2e9ac0e3d52329c23cf.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >SecretId, SecretKey</td><td style='text-align:left;' >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/bac87d3b033d65c5b0acb4ec588ca39f.png" referrerpolicy="no-referrer" alt="img"></td></tr></tbody>
</table>
2. Import [CMQ files](https://github.com/tencentyun/cmq-python-sdk) into the project. You need to select a branch based on the used Python version. The default SDK is for Python 2, and you can switch to the Python 3 branch to view the SDK for Python 3.
3. Create `my_topic` to publish messages.
<dx-codeblock>
:::  python
import os
import sys

sys.path.insert(0, os.path.dirname(os.path.abspath(__file__)) + "/..")

import logging
from cmq.account import Account
from cmq.cmq_exception import *
from cmq.topic import *

# `secretId` and `secretKey` of your Tencent Cloud account, which should be kept confidential
# You can get them at https://console.intl.cloud.tencent.com/cam/capi
secretId = 'AKIDSiiRtxxxx'
secretKey = 'GGzSeaM5xxxx'
# CMQ service call address
nameServerAddress = 'https://cmq-gz.public.tencenttdmq.com'

try:
	 # Initialize `my_account`
	 # Account class objects are not thread-safe. If you need to use them in multiple threads, initialize them for each thread
	 my_account = Account(nameServerAddress, secretId, secretKey, debug=True)
	 my_account.set_log_level(logging.DEBUG)
	 # Topic name
	 topic_name = sys.argv[1] if len(sys.argv) > 1 else "python_topic_route"
	 my_topic = my_account.get_topic(topic_name)
except CMQExceptionBase as e:
	 print("Exception:%s\n" % e)
:::
</dx-codeblock>
<table>
<thead>
<tr><th style='text-align:left;' >Parameter</th><th style='text-align:left;' >Description</th></tr></thead>
<tbody><tr><td style='text-align:left;' >NameServerAddress</td><td style='text-align:left;' >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/d304620abac50472de5d1ba898559ec3.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >SecretId, SecretKey</td><td style='text-align:left;' >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://qcloudimg.tencent-cloud.cn/raw/abc69c72893b65ad9d89f75febb2f0b5.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >topic_name</td><td style='text-align:left;' >Topic subscription name, which can be obtained on the <strong>Topic Subscription</strong> page in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>.</td></tr></tbody>
</table>
4. Send tag messages.
<dx-codeblock>
:::  python
 # Message tag
 tags = ["TAG", "TAG1", "TAG2"]
 for tag in tags:
		 # Send tag messages
		 message = Message("this is a test TAG message. TAG:" + tag, [tag])
		 re_msg = my_topic.publish_message(message)
		 # Sending result
		 print("Send Message Succeed! MessageBody:%s MessageID:%s" % (message.msgBody, re_msg.msgId))
:::
</dx-codeblock>
5. Send route messages.
<dx-codeblock>
:::  python
# Message route information
routes = ["a.b.c", "a.b.x", "a.c.d", "x.y.z", "x.y.c"]
for route in routes:
    message = Message("this is a test route message. Route:" + route)
# Send route messages    
re_msg = my_topic.publish_message(message, route)
# Sending result    
print("Send Message Succeed! MessageBody:%s MessageID:%s" % (message.msgBody, re_msg.msgId))

:::
</dx-codeblock>
6. The consumer can consume messages in the message queue subscribed to by the subscriber.

>?Above is a brief introduction to message production and consumption in two models. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-python-sdk-demo.zip) or [TDMQ for CMQ code repository](https://github.com/tencentyun/cmq-python-sdk).

