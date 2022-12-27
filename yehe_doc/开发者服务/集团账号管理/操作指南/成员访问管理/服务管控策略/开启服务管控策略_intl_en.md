The service control policy feature is disabled by default. You need to enable it before using it.

## Background

After the service control policy feature is enabled, your organization will have the following changes:

All departments and members in your organization are bound to the system policy `FullQcloudAccess` by default, which allows them to perform any operations on all your Tencent Cloud resources.

When a department or member is created, it will be automatically bound to the system policy `FullQcloudAccess`.

After a Tencent Cloud account accepts the invitation to join your organization, it will be automatically bound to the system policy `FullQcloudAccess`.

When a member is removed, all service control policies bound to it will be unbound automatically.

## Directions

1. Log in to the [TCO console](https://console.intl.cloud.tencent.com/organization).

2. On the left sidebar, select **Organization account** > **Service control policy**.

3. Toggle on **Service control policy**.

## Subsequent steps

You can create a custom service control policy (such as denying an operation on a resource) and bind it to a department or member in your organization. For detailed directions, see the following documents:

- [Creating Custom Service Control Policy](https://www.tencentcloud.com/document/product/1031/51871)
- [Binding Custom Service Control Policy](https://www.tencentcloud.com/document/product/1031/51875)