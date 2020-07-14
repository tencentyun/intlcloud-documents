CMQ provides a message rewind feature similar to that in Kafka. After your business successfully consumes and deletes a message, you can use this feature to consume the message again, which facilitates operations such as reconciliation and business system retry for core finance businesses.

## Feature Description


As shown above, the message lifecycle is circled in the blue box. After message rewind is enabled, messages consumed and deleted by consumers will be moved to the **rewindable message** section and retained on the CMQ backend. However, if the message existence exceeds the message lifecycle of the queue (assumed as 1 day), the message will be automatically deleted and cannot be rewound. The specific product logic is as follows:

- **Enable:** if message rewind is not enabled, after a message is consumed by a consumer and its deletion is confirmed, it will be deleted immediately. When enabling this feature, you need to specify the rewind time range, which must be equal to or shorter than the message lifecycle.

- **Milestone:** according to the policy above, after message rewind is enabled, the number of rewindable messages will keep increasing as consumers continuously consume and delete messages.

- **Disable:** after message rewind is disabled, messages in the rewindable message section will be deleted immediately and cannot be rewound.

- **Queue attribute:** message rewind is an attribute of a queue and can be set when you create the queue or modify its configuration. After specifying a rewind time, all consumers will consume messages produced after this time point.

- **Billing:** after message rewind is enabled, rewindable messages will incur certain retention fees. The unit price is calculated as a part of message retention fees.

- **Specify rewind time**: when a consumer initiates rewind consumption, the queue name and specific rewind time need to be specified, and messages will be rewound from the maximum time point. The time is a `key`, and reverse consumption is not supported. You can consume from timeA to timeB/timeC but not vice versa as shown below.

- **Specify rewind time range:** it ranges from 0 to 15 days. Only after message rewind is enabled in the console can deleted messages be rewound. You are recommended to always enable this feature for key applications and set the message rewind time range to the same as the message lifecycle.

- **Unable to specify message rewind for retained messages:** if a message is retained and not consumed, you cannot specify a specific position for its consumption.

## Rewindable Range

The **maximum rewindable time** is the current time minus the configured rewindable time range. Messages cannot be rewound if produced before this time.




## Timeline

**Message rewind** is sorted by message production time and is irrelevant to the order of deletion.



