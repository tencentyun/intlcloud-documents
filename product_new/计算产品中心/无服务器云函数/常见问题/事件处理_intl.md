### What is an event source?

An event source is an application created by a Tencent Cloud service or developer to generate events that trigger an SCF function.

### What event sources are supported?

Currently, triggering by manual triggers (APIs), timer triggers, COS, CMQ topics, API Gateway, and CKafka is supported, and more triggers will be available in the future.

### How does an application trigger a function directly?

The function can be triggered directly by calling the Invoke API of SCF. The owner of the function or an account that has the permission to call the function's Invoke API can make calls directly.

### How is the delay when a function responds to an event?

SCF can achieve request response in a matter of milliseconds for regular requests. However, the delay will become higher when the function is created, updated, or idle for a long time.
