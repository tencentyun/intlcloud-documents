### What is an event source?

An event source is an application created by a Tencent Cloud service or developer to generate events that trigger an SCF function.

### What event sources are supported?

Currently, triggering by manual triggers (APIs), timer triggers, COS, CMQ topics, API Gateway, and CKafka is supported, and more trigger types will be available in the future.


### How is the delay when a function responds to an event?

SCF can achieve request response in a matter of milliseconds for regular requests. However, the delay will become higher when the function is created, updated, or idle for a long time.
