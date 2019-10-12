## Example of CMQ Trigger

Assume that CMQ trigger is configured for SCF. 3 messages are sent to CMQ per second. A memory of 128 MB is configured for SCF. It takes 760 ms (calculated by 800 ms) for SCF to process messages and put in to a message queue per run.

Resource usage per day = (128/1024) x (800/1000) x 3 x 3600 x 24 = 25920 GBs

Invocations per day = 3 x 3600 x 24 = 259200

Fees per month (calculated by 30 days):

Fee for resource usage per month = (25920 x 30 - 400000) x 0.00001666 = 6.29 USD

Fee for calls per month = (259200 x 30/1000000 - 1) x 0.2 = 1.35 USD

In this case, the total cost = 6.29 USD (fee for resource usage) + 1.35 USD (fee for calls) = 7.64 USD

## Example of File Upload

Assume that a user uses a cloud API to call SCF. The number of calls is 50 per minute. A memory of 256 MB is configured for SCF. It takes 3680 ms (calculated by 3700 ms) for SCF to generate a 5 KB file and upload it to a user-built external site.

Resource usage per day = (256/1024) x (3700/1000) x 50 x 60 x 24 = 66600 GBs

Invocations per day = 50 x 60 x 24 = 72000

Traffic per day = 5 x 50 x 60 x 24 = 360000 KB = 351.5625 MB

Fees per month (calculated by 30 days):

Fee for resource usage per month = (66600 x 30 - 400000) x 0.00001666 = 26.62 USD

Fee for calls per month = (72000 x 30/1000000 - 1) x 0.2 = 0.23 USD

Fee for public network outbound traffic = (351.5625 x 30/1024) x 0.12 = 1.24 USD

In this case, the total cost = 26.62 USD (fee for resource usage) + 0.23 USD (fee for calls) + 1.24 USD (fee for public network outbound traffic) = 28.09 USD

