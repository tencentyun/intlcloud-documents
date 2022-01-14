

## Resource Constraint

This is an open-source project for both individual and team developers, and we welcome code contribution. Please observe the following rules for more efficient communication and development as well as a better user experience:
- Output product details, field lists, and corresponding APIs.
- Expose TencentCloud APIs for CRUD operations as required by products (at least the APIs for creation and deletion must be supported).
- Unique IDs or values such as names and SNs must be returned after resources are created.
- Input arguments must be able to be queried to ensure that the configuration and actual resource state are consistent.
- You must provide unit tests and ensure that they are passed.
- Single responsibility principle: do only one thing per change and avoid relying on or affecting other changes.


## Code Development
You need to fork a copy of the code from the master repository to a subrepository. Develop the code as instructed in [Development Notes](https://intl.cloud.tencent.com/document/product/1043/44221) and [Development and Debugging](https://intl.cloud.tencent.com/document/product/1043/44222), and ensure that the code can be executed after self-tests and unit tests are passed before committing it for push.
After the code is pushed, create a merge request to the [master repository](https://github.com/tencentcloudstack/terraform-provider-tencentcloud) for code review.
