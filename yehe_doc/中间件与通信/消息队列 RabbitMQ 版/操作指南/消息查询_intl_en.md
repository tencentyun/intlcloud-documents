## Overview

You can view the content or parameters of a message by using the message query feature in the TDMQ for RabbitMQ console. This feature allows you to view message details after querying the production records of a batch of messages over a specific time period or the production record of a specific message by its ID.

## Query limits

- You can query messages in the last 3 days.
- You can query up to 65,536 messages at a time.

## Prerequisite

You have deployed the producer and consumer services as instructed in the [SDK documentation](https://intl.cloud.tencent.com/document/product/1113/43132), and they produced and consumed messages in the last 3 days.

## Directions

1. Log in to the [TDMQ for RabbitMQ console](https://console.cloud.tencent.com/tdmq/rabbit-cluster) and click **Message Query** on the left sidebar.
2. On the **Message Query** page, select the region first, and then the time range, vhost, and queue for query. You can also enter a message ID for exact match query.
3. Click **Query**, and the list below will display paginated results.
![](https://qcloudimg.tencent-cloud.cn/raw/e2cfb55d14ca2b4bd3ba1d50d12e3786.png)
4. Click **View Details** in the **Operation** column of the target message to view its basic information, content (message body), and parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/07fdf0c52915ec1ac060fc170f3391d5.png)

