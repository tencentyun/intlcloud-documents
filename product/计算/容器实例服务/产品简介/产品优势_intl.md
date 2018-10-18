## Product Features
### **Serverless**

You don't need to purchase an underlying server to run a container, what you purchase is the container.

### **Secure and reliable**

CIS is as secure as CVM. Containers are running in your CVM with a securely isolated network environment.

### **Rapid creation**

You can create a container instance in just a few seconds.

### **Flexible configuration**

You can appropriately configure a custom container instance to maximize its resource utilization during runtime.

Only a fixed series of configurations are available in the internal trial.

### **Simple management**

The lifecycle of a container instance is controlled by a program running internally, and ends at the same time when the program ends, without the need of additional resource management for cutting costs.

### **Compatible with Kubernetes API**

It supports using the Kubernetes API for scheduling management.

### **Linux/Windows containers**

Linux/Windows containers are supported.

Only Linux containers are available in the internal trial.

## Differences Between CIS and TKE

| Feature | Kubernetes Service (TKE) | Container Instance Service (CIS) |
|---------|---------|---------|
| Kubernetes | Naturally supports | Supports through upper-layer scheduler management |
| Underlying servers | A TKE cluster consists of CVMs (nodes) you purchased. You take full control over these nodes, including purchase and return, adding and removing nodes to and from the cluster, etc. | You don't need to manage them |
| Management | You need to use Kubernetes to manage resources such as clusters and nodes, as well as services and applications, which is complicated | You only need to manage applications, which is relatively simple |
| Cluster | Supports | As a serverless service, each CIS is an independent instance, so no cluster is used |
| Service | Supports | Supports through upper-layer scheduler management |
| VPC | Supports | Supports |
| Application scenarios | TKE is suitable for deploying large-scale applications or micro-service frameworks with a complex hierarchy and an independent Kubernetes management layer in scenarios focusing more on management | CIS is suitable for deploying applications with a simple hierarchy, or can be used as a serverless resource pool for some application frameworks in scenarios demanding light management |

