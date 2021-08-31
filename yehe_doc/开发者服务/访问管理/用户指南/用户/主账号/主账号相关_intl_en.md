## Introduction
This document describes how to configure root account permissions and message channels.
## Prerequisites
You have signed up for a Tencent Cloud account, which is the root account. For more information, please see [Sign up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).
## Directions
### Root account does not require authorization
By default, a root account owns all the Tencent Cloud resources under it and can access any resources with no authorization required. Therefore, we do not recommend using the root account to access resources. You should create sub-accounts and grant them permissions based on the principle of least privilege and then use such sub-accounts with limited permissions to access your Tencent Cloud resources. For more suggestions on using account permissions, please see [Best Practices](https://intl.cloud.tencent.com/document/product/598/10592).
### Root account message channels
The recovery mobile number and email address set when you signed up for your Tencent Cloud root account will also be used as the default message channels. Please note that modifications made in [Account Center](https://console.cloud.tencent.com/developer/security) are not synced to the [CAM Console](https://console.cloud.tencent.com/cam). If you wish to modify these message channels, please see [Root Account Message Subscriptions](https://intl.cloud.tencent.com/document/product/598/34898).
>!In order to avoid potential losses caused by missed messages, please go to the [CAM Console](https://console.cloud.tencent.com/cam) to check whether the contact mobile number or email address used for message subscription is correct.

## Relevant Documents
For more information on how to change the recovery mobile number or email address for a root account, please see [FAQs About Email Address and Mobile Number](https://intl.cloud.tencent.com/document/product/378/17357).
For more information on how to create a sub-user, please see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
For more information on how to configure sub-account permissions, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).






