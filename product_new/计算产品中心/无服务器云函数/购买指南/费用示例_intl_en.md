## Example of CMQ Trigger

Assume that a CMQ trigger is configured for a function with 3 messages sent to the message queue per second. A memory of 128 MB is configured for the function. The function processes the message and adds it to the message queue. The running time is 760 ms and billed as 800 ms.

Assume that the resource usage and number of invocations per day are as follows:
- Resource usage per day = (128/1024) x (800/1000) x 3 x 3600 x 24 = 25920 GBs.
- Number of invocations per day = 3 x 3600 x 24 = 259200

The monthly cost (30 days) is calculated as follows:
- Resource usage fee per month = (25920 x 30 - 400000) x 0.00011108 = 6.29 USD.
- Fee for number of invocations per month = (259200 x 30/1000000 - 1) x 1.33 = 1.35 USD.

In this case, the total cost is: resource usage fee 6.29 USD + fee for number of invocations 1.35 USD = 7.64 USD.




## Example of File Upload

Assume that a user invokes a function using API at a frequency of 50 invocations per minute. The memory configured for the function is 256 MB. The function generates a 5 KB file for each invocation and upload it to an external site of the user. The running time of the function is 3680 ms and billed by 3700 ms.

Assume that the resource usage and number of invocations per day are as follows:
- Resource usage per day = (256/1024) x (3700/1000) x 50 x 60 x 24 = 66600 GBs.
- Number of invocations per day =50 x 60 x 24 = 72000.
- Traffic per day = 5 x 50 x 60 x 24 = 360000 KB = 351.5625 MB.

The monthly cost (30 days) is calculated as follows:
- Resource usage fee per month = (66600 x 30 - 400000) x 0.00011108 = 26.62 USD.
- Fee for number of invocations per month = (72000 x 30/1000000 - 1) x 1.33 = 0.23 USD.
- Fee for public network outbound traffic = (351.5625 x 30 / 1024) x 0.8 = 1.24 USD.

In this case, the total cost is: resource usage fee 26.62 USD + fee for number of invocations 0.23 USD + fee for public network outbound traffic 1.24 USD = 28.09 USD.
