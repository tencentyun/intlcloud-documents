## Overview
You can configure email templates in the SES console. This document describes how to create an email template.

## Directions
1. Log in to the [SES console](https://console.cloud.tencent.com/ses/domain), click **Configuration** > **Email Template** to enter the **Email Template** page, and click **Create**.
![](https://main.qcloudimg.com/raw/d857206e82427fc3313660237880b2ef.png)

2. In the **Create Email Template** dialog box, enter a template name, select a template type, upload an email body, click **Preview** to preview the template, and click **Submit** to complete the configuration.
![](https://main.qcloudimg.com/raw/56f4d929563e2aeeace698b9b80b61e2.png)
>?
>- There are two types of templates: HTML rich text and plain text. The former supports more styles to show rich content, while the latter supports text only. Select a type as needed.
>- Variables in the email are represented by `{{variable name}}`, such as "Dear `{{name}}`". The template used in **Email Sending** supports only one variable, while that used in **Batch** supports multiple variables.
