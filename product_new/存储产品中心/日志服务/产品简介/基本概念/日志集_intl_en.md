

A logset is a project management unit within the Cloud Log Service, used to distinguish between the logs of different projects. A logset corresponds to a project or application. It is recommended to manage the logs of different projects and products using different logsets. For example, your company runs two types of services, e-commerce services and payment services. You should create a logset for each service type.

A logset can contain multiple [log topics](https://intl.cloud.tencent.com/document/product/614/32849) and each log topic has the following basic attributes:
- Logset name: the name of a logset.
- Logset ID: the unique ID of a logset.
- Region: the [regions](https://intl.cloud.tencent.com/document/product/614/18940) to which the logset belongs.
- Storage period: the storage period for the data in the current logset. The period can be 3-90 days.
