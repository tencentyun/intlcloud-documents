### Version 2.9.1 
1. Fixed bugs.

### Version 2.9.0 
1. Supported MySQL 5.7.
2. Supported various encodings including UTF-8.
3. Supported distinction between NULL and empty string.
4. Supported the BLOB field.

### Version 2.8.2
1. Optimized SDK memory usage.
2. Supported the VPC authentication, allowing you to use the SDK via both private and public networks.

### Version 2.8.0
1. Optimized the internal authentication logic.
2. Reduced the number of user parameters that need to be configured.

### Version 2.7.2
1. Filled the `db` value in the DDL statement result.

### Version 2.7.0
1. Supported seconds-level HA switch at the data subscription channel backend.
2. Added the SDK monitoring metric report feature.

### Version 2.6.0
1. Supported subscribing to multiple channels via a single SDK.
2. Supported subscribing to "stop", "start" and other operations on Client.
3. Supported the serialization of `DataMessage.Record`.
4. Optimized the SDK performance and reduced the resource consumption.

### Version 2.5.0
1. Fixed bugs occurred with small probability in high-concurrency scenarios.
2. Supported the globally unique auto-increment ID recorded in transactions.

### Version 2.4.0
1. Optimized the subscription logic by working with the backend to accurately display SDK's current consumption time point.
2. Fixed the problem occurred while encoding a few special characters at the backend.
3. Fixed multiple compatibility issues. We recommend that users who use earlier versions upgrade the SDK to this version as soon as possible.

