### How is CDH billed?

At present, CDH is billed in a prepaid manner. When assigning a dedicated CVM instance, you don't need to pay for the CPU, memory or local storage, but you need to pay for the cloud disk and Internet bandwidth mounted on the instance.

For details on the billing method, see [CDH Billing Methods](/document/product/416/7585).

### Is a dedicated CVM instance assigned on CDH billed?

When you purchase a CDH, the price you pay already includes the CPU, memory and local storage fees of the physical server, so you don't need to pay for these resources when assigning an instance. However, you need to pay for the cloud disk and Internet bandwidth mounted on the instance. For details, see the instance billing section in [Billing Methods](/document/product/416/7585).

### Can I purchase a CDH in a postpaid manner?

No. At present, CDH can be purchased only in a prepaid manner.

### When a CDH is moved toe the recycle bin, what happens to the dedicated CVM instances on it?

If you don't renew a CDH when it expires, its resources will be moved to the recycle bin.

After the host is moved to the recycle bin:

- The dedicated CVM instances on it will stop service and disappear from the instance list in the CVM Console.
- If the host is renewed within seven days of expiration, all the instances on it will automatically resume service with no manual power-on required.
- If the host fails to be renewed after more than seven days, the host resources will be terminated and the instances will be terminated alongside.
