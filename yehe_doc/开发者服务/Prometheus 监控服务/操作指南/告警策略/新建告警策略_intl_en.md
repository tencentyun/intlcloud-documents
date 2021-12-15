This document describes how to create an alerting rule in the TMP console. With such a rule, you will receive notifications when some metrics are exceptional, so that you can take corresponding measures promptly.

## Prerequisites

- You have created a [managed TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have created a TMP instance.
- You have installed the Prometheus agent and other monitoring components.

## Directions

For more information on alerting rule, please see Alerting Rule Description.

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the corresponding TMP instance and click **Alerting Rule** on the left.
3. On the alerting rule management page, click **Create** and configure the alerting rule information in the pop-up window.
	- **Rule Template Type**: select a rule template type. For more information, please see Alerting Rule Type Description.
	- **Rule Name**: you can use the default rule name or customize it.
	- **PromQL-Based Rule**: you can use the default value or customize it. It indicates an alert trigger condition based on a PromQL expression, which is used to calculate whether there is time series data meeting the condition.
	- **Duration**: you can use the default value or customize it. It indicates how long a trigger condition can last before an alert is sent.
	- **Alert Object**: you can customize the alert title.
	- **Alert Message**: you can use the default value or customize it. It indicates the custom alert content.
	- **Advanced Configuration**: you can toggle it on for configuration, which contains configuration items for labels and annotations.
		- **Labels**: you can use the default value or customize it. It indicates a set of specified labels to be added to alerts. You can match the corresponding processing method based on the labels of a received alert.
		- **Annotations**: you can use the default value or customize it. It indicates the user-defined additional alert information.
	- **Alert Notification**: you can customize the alert notification template, which contains the template name, notification type, recipient, and receiving channel. For more information, please see Notification Template.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/790f6fd086ece617708fcab0fdc58398.png)

