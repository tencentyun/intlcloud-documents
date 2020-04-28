CMQ message timer allows you to specify an initial period during which messages to be added to the queue are invisible. This period is called **inflight**. For example, if you set the `DelaySeconds` parameter to 45 for a message, the consumer will not be able to see it in the first 45 seconds after it enters the queue. The default value of `DelaySeconds` is 0.

**Value range of message delay**: when specifying a queue for message production, you can add the `DelaySeconds` input parameter in the value range of 0–3600, i.e., the message can be invisible for up to one hour. If this parameter is left empty, the message will not be delayed.

**Use limits**: up to 20,000 inflight messages are allowed in one queue. If this limit is exceeded, newly produced messages will be invisible in the queue. Currently, this feature is not available in topic mode.
