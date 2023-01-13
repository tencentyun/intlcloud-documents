On the **Application configuration** page, you can customize the exception types in the application details and URL convergence rules and configure whether to include errors with specified status codes in the number of errors.


## Prerequisites
1. Go to the [**System management**](https://console.cloud.tencent.com/apm/monitor/settings) page in the APM console.
2. Go to the **Application configuration** page.

## Directions

### Exception filtering

This parameter filters the exception type in the exception analysis chart on the application details page. You can use the regex to match the full name of the exception class and separate multiple items by comma, such as `java.lang.inter,java.lang.index`. The exception types entered here will neither be displayed on the **Application details** page nor included in the number of exceptions and exception analysis.

### Error code filtering

This parameter filters the status code of errors included in the number of errors. You can set the error codes that need to be ignored here and separate them by comma, such as "429,512". Errors with the status codes entered here will not be included in the number of errors.

### URL convergence

This parameter converges multiple similar URLs into one, such as URLs starting with `/service/demo/`.

### Convergence threshold

This parameter specifies the minimum quantity for URL convergence. For example, if the threshold is `100`, convergence will be performed when the number of URLs in line with the regex reaches 100.

### Convergence rule regex

This parameter specifies the URL convergence rule in regex. For example, to converge URLs starting with `/service/demo/` when their number exceeds 100, the convergence threshold should be `100`, and the convergence rule regex should be `/service/demo/(.*?)`.

### Exclusion rule regex

This parameter excludes specified URLs from convergence. For example, to exclude URLs starting with `service/demo/example` from convergence, the regex should be `/service/demo/example/(.*?)`.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/v3GA238_1.png"  width="65%">