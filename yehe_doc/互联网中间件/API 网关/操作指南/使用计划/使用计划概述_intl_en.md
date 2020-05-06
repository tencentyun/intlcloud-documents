API Gateway uses usage plans to control the authentication, request traffic, quotas, and API user permissions after a service is published.

Currently, the content that can be adjusted and controlled by a usage plan includes:
* Authentication and security control
* Traffic control

A usage plan will take effect after it is bound to a service environment.

Multiple usage plans can be bound to the same service environment, and one usage plan can be bound to multiple service environments.

>Two or more usage plans bound to the same key cannot be bound to the same environment in the same service. Similarly, if two or more usage plans have been bound to the same environment in the same service, they cannot be bound to the same key.
