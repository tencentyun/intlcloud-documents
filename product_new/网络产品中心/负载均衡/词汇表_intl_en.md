### Cloud Load Balancer
Cloud Load Balancer (CLB) is a secure, stable, and elastically scalable traffic distribution service provided by Tencent Cloud. It can improve system availability by avoiding single points of failure.

### CLB Instance
A CLB instance is a running CLB service. To use CLB service, create a CLB instance first. 

## Virtual IP
Virtual IP (VIP) is the IP address assigned by the system to a CLB instance. You can choose whether to open it to the internet so as to create a private network or public network CLB instance. You can resolve the domain name to public VIP to provide services.

### CLB Listener
A CLB listener provides request distribution rules including listening ports, load balancing policies, and health check configurations. Requests are forwarded to the real server according to listener configurations. A CLB instance should have at least one listener.

### Real Server
A real server (RS) is a set of CVM instances that are used to process the CLB distributed requests.

### VPC
Virtual Private Cloud (VPC) is a private network space in Tencent Cloud that provides network services for your Tencent Cloud resources. A VPC is logically isolated from others.

### Security Group
A security group is a virtual firewall capable of filtering stateful packets. It achieves access control on instances by specifying IP, protocol, and port rules for instance access.

### Region
A region is where a CLB instance and other resources are launched. Please select the region close to your business client. Generally, a CLB instance needs to be in the same region as your real server. If needed, you can activate [cross-region CLB binding](http://intl.cloud.tencent.com/document/product/214/12014) for cross-region communication.
