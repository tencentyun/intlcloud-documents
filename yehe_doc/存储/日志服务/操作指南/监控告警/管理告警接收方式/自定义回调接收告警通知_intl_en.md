## Overview

This document describes how to receive alarm notifications via custom callback APIs (webhooks).

## Use Limits

Each custom callback API can send up to 20 messages per minute. If many alarm policies are configured, we recommend that you create multiple custom callback APIs and associate them with different alarm policies; otherwise, multiple alarm policies may trigger alarms simultaneously, and you may fail to receive some alarm notifications as a result.
>?
>- After you have successfully created custom callback APIs and set callback addresses, CLS will automatically send requests to these APIs as configured.
>- Custom callback APIs require access over the public network, as CLS cannot call back private network addresses.

## Directions


### Generating custom callback links for target services

Generate custom callback links (webhooks) for custom services requiring callbacks (such as DingTalk and Slack) to receive alarm notifications.

### Configuring custom API callbacks (custom webhooks)

On the **Notification Channel** page in the CLS console, enter the custom callback link address, and set the custom request content as required. For more information on the configuration, please see [Adding Notification Channel Groups](https://intl.cloud.tencent.com/document/product/614/41987).


After custom API callbacks are configured, when alarm policies are triggered, CLS will call the custom APIs according to the configured request formats.


