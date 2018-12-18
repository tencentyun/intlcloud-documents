Load balancing management provides the ability to set weights for resolution loads.
### Setting Load Balancing for the Resolution First
Load balancing of resolution is available for records of the same record type, the same host and the same line.
![](//mc.qcloudimg.com/static/img/51f1a5daa232d0b91db9ff5d2a5ac103/image.png)
### Entering the Load Balancing Page to View
The default is equal load, that is, the authoritative server will return all the record values in a random order, and the system takes the first IP address by default, so the probability of obtaining each resolution record is roughly equal.
![](//mc.qcloudimg.com/static/img/9cbe986b857e0cf7ff54e2e253b8ced6/image.png)
At this time, the weight is 0, and the resolution proportions are equal.
![](//mc.qcloudimg.com/static/img/a8a3180902b2040b91a97b33c2c04027/image.png)
### Modifying the Weights 
Click **Modify weight** to set the weight between 1 and 100, and the authoritative server will return an IP node according to the weight.
![](//mc.qcloudimg.com/static/img/9cfcfd37f383173ed5bd2c7f5da8fe7d/image.png)
