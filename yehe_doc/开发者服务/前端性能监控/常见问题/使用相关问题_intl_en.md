[](id:que1)
### What is the UIN passed in during SDK initialization?

 Unique Identity Number (UIN) is a unique user ID provided by the Aegis SDK. RUM doesn't verify the UIN and only uses it as an index for log query. During development, you can enter the user ID provided by your business or information such as `open-id` and `uuid` as long as it facilitates query.

[](id:que2)
### Why does custom speed test support data only between 0 and 60000?

In the logic of custom speed test, RUM calculates the mean and median values of any data reported by users and displays them. Since the volume of dirty data generated on the server is unknown, even a small amount of it can have a huge impact on the actual user data. Therefore, RUM restricts the user data on the server to values between 0 and 60000.

[](id:que3)
### Which field does RUM use to calculate the UV?
The Aegis SDK generates an `aid` for each user (device) as a unique ID, which is stored in `localStorage` in the browser for calculating the UV. `aid` is not affected by the login state and will be updated only when the user clears the browser cache.


[](id:que4)
### Why doesn't RUM use the user UIN to calculate the UV?

The UIN cannot be used to calculate the UV if the current user is not logged in. It is unreliable as a value specified during development since it cannot unify the state before and after user login.

[](id:que5)
### What is an API request log?

An API request log records the request and response content of a user API. Generally, such logs are reported only by used in the allowlist; however, if a JavaScript error occurs when a user is using an API, the API information of the user in the previous period of time will also be reported to the server to help you locate and analyze the problem.

### How is `FMP` calculated?

RUM listens on the first screen DOM changes within 3 seconds after a page is opened and takes the time when the number of DOM changes reaches the highest as the time when the first screen framework rendering is completed. (`setTimeout` is used to start first screen element collection 3 seconds after SDK initialization. As JavaScript is executed in a single-thread environment, the collection time point may be more than 3 seconds after SDK initialization.)

### How is the DOM parsing time in the performance data calculated?

It is the time between `domInteractive` and `domLoading` in the `PerformanceTiming` API.

### Is the user time or service time used when RUM collects data? How long is the delay?

The service time is used. The displayed time is around 1–2 seconds after the reported time, and log search may have a delay of 1–2 minutes.


