### CMQ SDK for HTTP 1.0.7 (March 25, 2020)
- Changed `artifactId` to `cmq-http-client` on the new version.
- Fixed the bug where messages exceptionally got lost.
- Removed unused clients and fixed issues #6 and #7.

[Code repository address >>](https://github.com/tencentyun/cmq-java-sdk/tree/1.0.7) 



### CMQ SDK for TCP 1.1.1 (February 12, 2020)
#### New features
- Added stream management APIs, such as those for queue creation and subscription creation.
- Completed relevant unit testings, which are not enabled during construction by default.
- Made the `pom` file compatible with Maven 3.0+.

#### Bug fixes
- Fixed the issue where transaction messages exceptionally got lost.
- Fixed the issue where the timeout period in the configuration did not take effect for TCP.
- Fixed the exception of "repeated authentication" in concurrence scenarios.

[Code repository address >>](https://github.com/tencentyun/cmq-java-tcp-sdk/tree/v1.1.1) 


### CMQ SDK for HTTP 1.0.6 (November 12, 2019)
#### New features
- SDK configuration is objectified and parameters such as timeout period and whether to print slow operation logs are added. For more information, please see the `CmqConfig` object.
- The new message sending and receiving APIs feature 6 times higher performance.
- Logs for slow operations and exceptions can be printed automatically (which requires a log file to be configured).
- The return of `requestId` is added for the new sending API for problem tracking.

#### Bug fixes
- Fixed the occasional exception of JSON serialization.
- Fixed other code specification issues.
- Fixed log configuration issues.
- The SDK uses SLF4J to print logs, but there is no specific log configuration file. You can add a configuration file of logging frameworks such as Log4j or Logback to `classpath`.

#### Usage recommendations
- Receive messages by using the new (batch) `receiveMessage` API (long polling wait time is subject to queue settings).
- Send messages by using the new (batch) `send` API (which can return the `requestId`).

[Code repository address >>](https://github.com/tencentyun/cmq-java-sdk/tree/1.0.6)     


### CMQ SDK 1.05 (June 28, 2019)
CMQ now supports SDK calls based on the TCP protocol, which feature lower computing resource usage, higher client thread security, transfer efficiency, and feature diversity, and better user experience.

### CMQ SDK 1.0.4 (April 7, 2017)
- The CMQ SDK now supports SHA256 signature algorithm. You can call `setSignMethod` during account initialization to set the signature algorithm (for specific algorithm names, please see the code description).
- Known bugs are fixed.

### CMQ SDK 1.0.3 (March 13, 2017)
CMQ now supports message rewind, message delay, and subscription routing.

### CMQ SDK 1.0.2 (December 1, 2016)
- The SDK supports topic and subscription modes.
- CMake is used for project management in the SDK for C++.
- Maven is used for project management in the SDK for Java.

### CMQ SDK 1.0.1 (October 12, 2016) 
- Optimized the user experience in case of client timeout.
- Fixed the bug of authentication failure in the SDK for PHP.
- Fixed the bug of message sending in PHP.

### CMQ SDK 1.0.0 (September 7, 2016) 
- The versions for C++, Java, Python, and PHP are released.
- The SDK encapsulates APIs for operations such as sending, receiving, and deleting messages.


