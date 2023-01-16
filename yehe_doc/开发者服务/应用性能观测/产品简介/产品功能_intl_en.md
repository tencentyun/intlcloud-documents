## Call Tracing
### Multidimensional trace query
APM supports filtering call traces by API, response time, sampling time, error status, and duration. It helps you quickly locate database query traces containing specific exception information among massive amounts of trace data and then swiftly troubleshoot errors.

### One-Stop call trace analysis
APM's tracing feature can automatically build the complete path of each request across services in a microservice architecture. It collects diverse information from request parameters, transaction data, errors, and exceptions to method stacks and underlying instance environment information, enabling full-trace analysis from one platform and improving the troubleshooting efficiency. This solves troubleshooting challenges like difficult aggregation of scattered logs in non-standard formats as well as difficulties in associating upstream/downstream service logs.

## Application Performance Analysis

### Automatic discovery of application dependency topology

APM automatically discovers application logic topologies through the distributed call tracing model and then draws global topologies at the application level. This visually displays complex dependencies between applications and enables you to quickly locate application or component bottlenecks through real-time data drill-down and smart application status analysis. APM can also display the upstream/downstream dependencies of an application to show how the upstream load may affect downstream services, so that you can comprehensively analyze the health status and performance metrics of the application.

### Top N API analysis
On top of the three golden metrics of application monitoring, APM adds Apdex metrics to scientifically evaluate the user satisfaction. By leveraging the rich experience of CM in visual reports, it further allows you to flexibly switch between comparison curves and accurately determine application conditions and change trends. In addition, it intelligently monitors the top 5 time-consuming or erroneous APIs to help you troubleshoot issues fast and focus more on your users, so you can accurately track the performance of your applications.

### Multidimensional analysis
APM actively aggregates performance and exception metrics in various dimensions such as API, exception, and database call to help you swiftly identify slow APIs, SQL statements, and frequent exceptions. By leveraging the quick trace drill-down feature, you can greatly shorten the MTTR.

## Database Call Monitoring
APM can comprehensively monitor many types of databases such as MySQL, Oracle, MongoDB, and Redis. It automatically collects the database performance metrics relevant to the business system, helping you stay on top of slow SQL statements, calls, and read performance in your database and accurately locate database performance problems.
