When a general message is sent to a general message queue, its initial status is **Active**. After it is fetched out, its status will become **Inactive** within the time period specified by `VisibilityTimeout`. If the message is not deleted after the period specified by `VisibilityTimeout` elapses, its status will become **Active** again; otherwise, its status will become **Deleted**. The maximum retention period of the message is subject to the `MessageRetentionPeriod` attribute value specified when the queue is created. After this period elapses, the message will become **Expired** and be repossessed.

Consumers can read **Active** messages only, which ensures that a message will not be repeatedly consumed simultaneously but can be repeatedly consumed sequentially.

![](https://main.qcloudimg.com/raw/063f581951bdf7a4fef8706fd8a878ad.jpg)

- Component 1 sends message A, which has multiple redundancies across TDMQ for CMQ servers, to a queue.

- After getting ready to process messages, component 2 will retrieve messages from the queue, and message A will be returned. When being processed, message A still stays in the queue. Within the **hidden duration of fetched messages**, other businesses cannot get message A.

- Component 2 can delete message A from the queue to avoid receiving and processing it again after the **hidden duration of fetched messages** elapses. It can also retain message A so that other businesses can consume message A repeatedly.
