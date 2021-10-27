## Overview

This document describes how to receive alarm notifications via custom callback APIs (webhooks).

## Use Limits

Each custom callback API can send no more than 20 messages per minute. If many alarm policies are configured, we recommend that you create multiple custom callback APIs and associate them with different alarm policies. Otherwise, multiple alarm policies may trigger alarms simultaneously, and you may fail to receive some alarm notifications as a result.

>? After you create a custom callback API and set the callback address, CLS automatically sends requests to the custom callback API based on the configuration.
>

## Directions


### Generating custom callback links for target services

Generate custom callback links (webhooks) for custom services requiring callbacks (such as DingTalk and Slack) to receive alarm notifications.

### Configuring custom API callbacks (custom webhooks)

On the **Notification Channel** page in the CLS console, enter the custom callback link address, and set the custom request content as required. For more information on the configuration, please see Adding Notification Channel Groups.


After custom API callbacks are configured, when alarm policies are triggered, CLS will call the custom APIs according to the configured request formats.


