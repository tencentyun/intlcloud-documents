

TDMQ for CMQ currently supports SDKs for Java, Python, PHP, and C++. More languages will be supported in the future. Developers are encouraged to develop SDKs for more languages based on the API descriptions.


To allow CMQ users to migrate to TDMQ for CMQ without modifying the business code, the following APIs remain the same as those on earlier versions.

 | API Feature | Action ID | Description |
 | :----------------------------------------------------------- | :------------------ | :------------------------------- |
 | [Sending message](https://intl.cloud.tencent.com/document/product/1111/46415) | SendMessage         | Sends a message to a specified queue.   |
 | [Batch sending messages](https://intl.cloud.tencent.com/document/product/1111/46416) | BatchSendMessage    | Batch sends messages to a specified queue.   |
 | [Consuming message](https://intl.cloud.tencent.com/document/product/1111/46417) | ReceiveMessage      | Consumes a message in a queue.       |
 | [Batch consuming messages](https://intl.cloud.tencent.com/document/product/1111/46418) | BatchReceiveMessage | Batch consumes messages in a queue.       |
 | [Deleting message](https://intl.cloud.tencent.com/document/product/1111/46419) | DeleteMessage       | Deletes a consumed message.     |
 | [Batch deleting messages](https://intl.cloud.tencent.com/document/product/1111/46420) | BatchDeleteMessage  | Batch deletes consumed messages. |
 | [Publishing message](https://intl.cloud.tencent.com/document/product/1111/46421) | PublishMessage      | Publishes a message to a specified topic.     |
 | [Batch publishing messages](https://intl.cloud.tencent.com/document/product/1111/46422) | BatchPublishMessage | Batch publishes messages to a specified topic.      |

 Other APIs need to be developed as instructed in [HTTP Control Flow SDK](https://intl.cloud.tencent.com/document/product/1111/46413).

