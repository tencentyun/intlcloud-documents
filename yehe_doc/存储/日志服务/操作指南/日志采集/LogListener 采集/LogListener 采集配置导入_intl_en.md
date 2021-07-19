This document describes how to use LogListener to quickly import the collection configuration rules of other log topics.

## Overview

LogListener collection configuration refers to the collection path, use limits, collection mode, and other collection rules configured in the LogListener collection server before log collection. The collection configuration rule import feature allows users to import the collection configuration of an existing log topic to quickly configure LogListener collection rules when they add or modify collection configuration. This eliminates repetitive and tedious operations for configuring multiple log topics and improves the efficiency of collection configuration.

>? 
> - By default, the collection of a log file can only be configured in only one LogListener.
> - To apply multiple collection configurations to one file, you need to add a soft link to the source file and add the soft link to another group of collection configuration.
> - Only LogListener 2.3.9 or above allows adding multiple collection paths.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. In the left sidebar, click **Log Topic** to go to the log topic management page.
3. Click the ID/name of an existing log topic to go to the log topic information page.
4. Click the **Collection Configuration** tab to go to the **Collection Configuration** tab page.
5. Click **Import Configuration Rule** in the upper-right corner.

6. In the configuration rule list displayed in the pop-up window, select the configuration rule of a log topic to import and click **OK** to import it to the collection configuration of the current log topic.

>?
> - The configuration rule list displays all log topics that support the cross-region log topic configuration rule import feature in the current region by default.
> - Only the collection rules of log topics for which a collection path is configured can be imported to the collection configuration of the current log topic.
>

## Collection Mode

LogListener can collect text logs in the following collection modes: [Full Text in a Single Line](https://intl.cloud.tencent.com/document/product/614/32287), [Full Text in Multi Lines](https://intl.cloud.tencent.com/document/product/614/32284), [Full Regular Format (Single-Line)](https://intl.cloud.tencent.com/document/product/614/39589), [Full Regular Format (Multi-Line)](https://intl.cloud.tencent.com/document/product/614/39590), [JSON Format](https://intl.cloud.tencent.com/document/product/614/32286), and [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285).

