### Matching Rules

The purchased reserved instance (RI) automatically matches to pay-as-you-go instances during the RI term. For now, Windows znd Linux instances are supported. If you have no instances that match the RI specifications, the RI will become idle but still incur fees. When you purchase an instance with matched specifications, the RI will immediately matches to it and the benefit applies.  

- RIs are automatically matched with pay-as-you-go instances without manual intervention.
- The RI billing benefit can apply to a maximum of 3,600 seconds (one hour) of instance usage per clock-hour. You can run multiple instances concurrently, but can only receive the benefit of the RI discount for a total of 3,600 seconds per clock-hour; instance usage that exceeds 3,600 seconds in a clock-hour is billed at the pay-as-you-go rate. 

For example, if you purchase one S3.16xlarge256 RI in Silicon Valley Zone 1, and run three pay-as-you-go S3.16xlarge256 instances of the same attributes concurrently in the same availability zone for one hour, one instance is charged at one hour of RI usage and the other two instances are charged at one hour of pay-as-you-go usage each. 

However, if you purchase one S3.16xlarge256 RI in Silicon Valley Zone 1 and run three pay-as-you-go instances (A, B, and C) of the same attributes in the same availability zone for 20 minutes each within the same hour, the total running time for the instances is one hour, which results in one hour of RI usage and 0 hours of pay-as-you-go usage, as shown below.

![1558602502993](https://main.qcloudimg.com/raw/a812f74455b8b9d8ebbc84e90e26bc04.png)

If the three eligible instances are running concurrently, the RI billing benefit is applied to all the instances at the same time for up to a maximum of 3,600 seconds in a clock-hour; thereafter, the pay-as-you-go price applies.

![1558602155668](https://main.qcloudimg.com/raw/24926b2c2675e2d6959adcf62054f5b1.png)

#### Effective time

RIs are billed on every hour. They take effect on the previous hour of the creation time and expire on the next hour of the expiration time. 

Example 1: assume you purchased a 1-year term CVM R1 on May 25, 2019 11:15:24, the RI will be valid from May 25, 2019 11:00:00 to May 25, 2020 11:59:59.

Example 2: assume you purchased a 1-year term CVM R1 on May 25, 2019 11:00:00, the RI will be valid from May 25, 2019 11:00:00 to May 25, 2020 11:59:59.
