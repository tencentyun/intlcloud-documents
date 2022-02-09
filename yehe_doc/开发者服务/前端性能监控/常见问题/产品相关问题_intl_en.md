
[](id:que1)
### What is the purpose of the Aegis SDK?

The Aegis SDK is a data reporting SDK embedded into the user page or installed in the user code through npm. It mainly collects the performance and quality data of the user side.

[](id:que2)

### How long will data be retained?

- Raw data reported by users such as error, custom reporting, and page view data will be retained for 30 days.
- Performance metric data such as page performance, API monitoring, and static resource monitoring data will be retained for 15 days.
- Data calculated by RUM at a fixed time everyday such as daily project score and daily total PV/UV data will be retained for 90 days.

[](id:que4)
### Which platforms does RUM currently support and provide SDK for?

RUM currently supports data reporting on various platforms such as web, Hippy, mini program (WeChat and QQ), and React Native. It will provide SDKs for more platforms in the future.

### What is offline log?
Offline log is a solution where most logs are stored locally and will only be reported to RUM when necessary.

