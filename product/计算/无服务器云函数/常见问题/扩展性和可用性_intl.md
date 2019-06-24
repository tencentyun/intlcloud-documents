### How is the availability of SCF?

SCF enables high availability through cross-region deployment, replication, and redundancy.

### Can a function be used when its code or configuration is changed?

Yes. There is a short window period of less than 1 minute in general when the function is updated, during which the request will be implemented by either the old or new function code.

### Is there a limit to the number of functions that can be executed in a single run?

SCF supports high numbers of concurrent function instances. However, it has a default security threshold, i.e., only up to 20 concurrent executions are allowed per function. This threshold can be increased by submitting a ticket.

### What if a failure occurs when a function handles an event?

In case of failure, a function that makes sync calls will return the exception information, while a function that makes async calls will automatically retry 3 times in the backend.
