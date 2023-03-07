[Terraform TencentCloud Provider](https://github.com/tencentcloudstack/terraform-provider-tencentcloud) is maintained by the Tencent Cloud IaC team and welcomes contributions from developers.

>?
> This document is intended for Terraform TencentCloud Provider code developers.


## Contribution

Contribute your code in the following steps. You can have a look at [How It Works](https://www.tencentcloud.com/document/product/1172/52386) and [Requirements and Suggestions](https://www.tencentcloud.com/document/product/1172/52388) to get a general picture of the provider.

### 1. Configuring the development environment

Before starting the development, you need to install Terraform and Go to pull the code repository, compile the program, and set the test as instructed in [Development and Debugging](https://www.tencentcloud.com/document/product/1172/52387).

### 2. Writing the code

Write the code as instructed in the corresponding document based on the type of your code.

| Contribution Type | Description |
|---------|---------|
| [Resource and Data Sources](https://www.tencentcloud.com/document/product/1172/52377) | Add a resource or data source to Terraform TencentCloud Provider so as to manage Tencent Cloud product features or query the remote data of Tencent Cloud. |
| [Bug Fix or Enhancement](https://www.tencentcloud.com/document/product/1172/52378) | Most requests are for feature enhancement or bug fix. |
| [Tagging Support](https://www.tencentcloud.com/document/product/1172/52380) | Current resources require tag support and a unified tag service API. |
| [Documentation Changes](https://www.tencentcloud.com/document/product/1172/52379) | Documentation updates and changes are included. |

### 3. Writing the test

Cover all your contributed code in tests as instructed in [Writing Test Case](https://www.tencentcloud.com/document/product/1172/52381).

### 4. Creating a pull request

When your contribution is ready, [create a pull request](https://www.tencentcloud.com/document/product/1172/52382) in the repository of your provider.

### 5. Updating the changelog

An open-source project requires maintaining a user-friendly and readable `CHANGELOG.md` so that users can quickly know whether they will be affected by the release and assess the upgrade risk if applicable. For more information, see [Submitting Changelog](https://www.tencentcloud.com/document/product/1172/52383).

## Modules

Besides the source code, you can also submit modules to the provider as instructed in [Modules](https://www.tencentcloud.com/document/product/1172/52310).