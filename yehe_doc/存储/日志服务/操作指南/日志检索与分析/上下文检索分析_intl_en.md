
This document describes how to view the context of a log in the original file in the CLS console.

## Overview

Log context search refers to searching for the log’s context, that is, several logs before or after the log itself. This feature allows you to troubleshoot quickly whenever an error occurs.

## Advantages

- Log context search frees you from the hassles associated with machine logins. On the log search page, you can quickly view the log context of any file/machine.
- Knowing the actual error occurrence time, you can specify a time range on the log search page to quickly locate the suspicious log and query its context for troubleshooting.
- Storage capacity of the server or data loss caused by log rotation will not be a problem. The data history can be viewed on the log search page anytime.


## Prerequisites

- Log context search and analysis are available only for version 2.3.5 and above. You are advised to [install or upgrade to the latest version](https://intl.cloud.tencent.com/document/product/614/17414).
- Context search is supported for only logs collected by LogListener.
- You have enabled and configured index. For more information, please see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/16981).

## Example

The common process of an order is as follows: log in > browse merchandise > select merchandise> add merchandise to the shopping cart > place an order > pay for the order > make a deduction > generate the order.
Use case: if one of the orders of a user fails, you can query the error log using the order number. Then, locate the log’s context to find out the cause (for example, order deduction failed).
You can troubleshoot in CLS as follows:
1. Log in to the CLS console and go to the **Search and Analysis** page. Then, specify a time range based on the error occurrence time and enter the **keyword** (order number) to locate the error log of the order.
2. Scroll up/down based on the error log until you locate the desired context of the log.

<img src="https://main.qcloudimg.com/raw/85d5656e2d5b868872b2497757c5a2b0.svg" style="width: 50%"/>


## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to go to the **Search and Analysis** page.
3. Select the **Region**, **Logset**, and **Log Topic** as needed.
4. Enter the search syntax, select a time range, and click **Search and Analysis**.
5. On the **Raw Data** tab, find the time of the error log and click <img src="https://main.qcloudimg.com/raw/1327fb192ece11abdf3a130feaa4e78a.png"></img> to go to the context search and analysis page.
6. On the context search and analysis page, 10 logs before and 10 after the error log will be displayed.

On this page, you can:
 - Scroll up/down to view the context.
    - Click **Show Earlier** to page up. Up to 20 previous logs can be displayed at a time.
    - Click **Show More** to page down. Up to 20 later logs can be displayed at a time.
 - Enter the keyword in the **Highlight** text box to fill the keyword in yellow.
 - Enter a string in the **Filter Logs** text box to highlight the string.



