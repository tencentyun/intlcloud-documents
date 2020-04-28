

 When pushing messages in the console, you can select from two environments for push testing.

**Development environment**: you need to make sure that the application has been packaged with the signature certificate of the development environment and then use `Xcode` to directly compile and install it to the device.
**Production environment**: you need to make sure that the application has been packaged with the signature certificate of the production environment in one of the following three ways: `Ad-Hoc`, `TestFlight`, and `AppStore`.

## Specifying Push Environment on Server
When you use a `RESTful API` to push messages, you need to go to [`PushAPI`](https://cloud.tencent.com/document/product/548/39064#.E8.AF.B7.E6.B1.82.E5.8F.82.E6.95.B0) and specify the `environment` field, which has two optional values: `product` and `dev`.

**Development environment**: you need to specify `environment` as `dev`.
**Production environment**: you need to specify `environment` as `product`.


## Push Certificate Description
In the console, you need to upload the two-in-one push certificate for both the development and production environments (Apple Push Notification service SSL (Sandbox & Production)). This certificate can be used to push messages to both the production and development environments and is selected according to the actual signature certificate used by the application. For the selection method, please see above.

>
- Application signature certificate divides into development environment (corresponding to `xxx Developer:xxx`) and production environment (corresponding to `xxx Distribution:xxx`). Please choose according to the actual situation.
- Application push certificate is a merged certificate compatible with both the development and production environments.
