### What should I do if "504 Gateway Time-out" is displayed in logs when I call the API Gateway service?

If "504 Gateway Time-out" is displayed in logs when you call the API Gateway service, you can troubleshoot the problem in the following ways:

#### Check whether the API Gateway backend service can be directly accessed
 - If the backend service is HTTP-based and is not in any VPC, you can access it over the public network to check whether the access times out.
 - If the backend service is a CLB resource in a VPC, access the private IP of the CLB instance from another CVM instance in the same VPC to check whether the access times out.
 - If the backend service is TSF, you can access the timed-out instance through another service instance in the same namespace under TSF to check whether the access times out.

If the access still times out in the above tests, the backend service may have problems. In this case, you are recommended to check whether it is normal.

#### Check the timeout period set in API Gateway and the backend service
When configuring an API in API Gateway, you need to add the timeout period in the backend configuration. If the backend service fails to return the result in the specified timeout period, the gateway will return the 504 error.

#### Check whether the security group is set correctly
- If the backend address points to a CLB instance in a VPC, check whether the CVM security group bound to the CLB instance opens the API Gateway IP. If no security group is set, please check whether there are other port and network limits for the backend address.
Open IP in a security group: the backend CVM security group bound to the CLB instance needs to open the API Gateway private IP range. For private IP ranges in different regions, please see [Private IP Ranges and Public VIPs of API Gateway in Different Regions](https://intl.cloud.tencent.com/document/product/628/34060). The port of the service deployed on the CVM instance also needs to be opened. For more information on how to set the security group, please see [Security Group Operations](https://intl.cloud.tencent.com/document/product/213/12452).
- If your API is a microservice API, and the service is deployed on a CVM instance, you need to open the client IP and service port in the security group on the CVM instance.
- If your API is a microservice API, and the service is deployed in a container, as the container pod may not be fixed to a CVM instance, you are recommended to configure the same security group for all servers in the cluster and open the client IP and container port in the security group.
- If your backend address is a general HTTP address that can be accessed over the internet, you also need to check whether the firewall and security group are set and open the gateway public VIP.

>As the public VIP and private IP range of API Gateway may change, you are recommended to use key pair authentication to ensure request security.



