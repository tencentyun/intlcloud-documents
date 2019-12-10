### Is there any space in the environment for write operations?

Yes. SCF function has a temporary disk space of 500 MB (/tmp) during execution. You can perform read and write operations in this space while executing the code, but data written in this space will not be retained after the function is executed.
> 
> - The temporary disk spaces of different instances are isolated, i.e., each instance has its own independent temporary space.
> - In the operating environment, all directories are read-only except for `/tmp`.

### What if an error occurs after there is no more space for write operations?

If data is written to the `/tmp` directory continuously and the instance is used constantly due to frequent invocations, the directory may be full and write is no longer possible.
If this happens, check the state of writes in the directory and use codes to delete temporary files no longer needed to free up the space.

### What is the time zone of the environment?

UTC (GMT+0) is used in the SCF operating environment, which is 8 hours behind Beijing time.

### How to deal with the impact of time zones?

You can use a time processing library or code package in your programming language to identify UTC time zone and convert it to Beijing time (GMT+8). You can also set the `TZ=Asia/Shanghai` environment variable to specify the time zone.

### Can I use threads and processes in my function code?

Yes. You can use normal programming language and operating system features, such as creating additional threads and processes. Resources allocated to the function, including memory, execution duration, disk, and network, are shared by the threads or processes it uses.

### Can I initiate network connections in my function code?

Yes. You can use normal programming language and operating system features, such as initiating TCP and UDP connections. Through relevant language libraries, you can also perform operations such as connecting to databases and accessing APIs.

### What restrictions apply to function code?

We try not to impose restrictions on normal activities at the programming language and operating system levels, but certain activities such as inbound network connection are disabled.
