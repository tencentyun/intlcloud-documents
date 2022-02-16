## Overview

This document describes how to migrate a service from a shared API Gateway instance to a dedicated instance and provides answers to FAQs.

For more information on dedicated instance, see [Instance Specification](https://intl.cloud.tencent.com/document/product/628/40305).



## Migration Process

| Steps | Operation Details | Operator | 
| ----- | ------------------------------------------------------------ | ------------------ | 
| 1 | You provide the information of the service to be migrated, including region, `appId`, and service ID, such as Guangzhou, 123688xxx, and service-0x6u6xxx. | You |    
| 2 | API Gateway evaluates the configuration of the service to be migrated and outputs an evaluation report. | API Gateway |   
| 3 | If migration is feasible as evaluated in step 2, you need to evaluate the dedicated instance's specification (based on the business QPS) and VPC parameters (if the original service backend is across VPCs, you also need to configure a CCN instance for VPC interconnection). | You and API Gateway |     
| 4 | After creating a dedicated instance in step 3, you provide the instance ID to API Gateway for double check. | API Gateway |      
| 5 | After step 4 is completed, you confirm the migration time. | You |   
| 6 | At the scheduled time, API Gateway initiates the service migration (usually completed in 1 minute), and you observe the business monitoring data. **If the service goes exceptional during or after the migration, API Gateway will roll back the service immediately.** | API Gateway and you |      
| 7 | After the migration is completed, API Gateway will continue to observe the service for a period of time. If there is any exception, it will roll back the service immediately and notify you. | API Gateway |   



## FAQs

### Will the service be interrupted during the migration?

In theory, the migration is imperceptible to end users. If an exception occurs, the service will be rolled back immediately.

**At present, we guarantee that the domain name of the API Gateway service won't change after the migration, but the ingress and egress IPs will change. If your business client relies on the ingress IP or your backend has an egress IP allowlist, you need to communicate with us in advance.**

### Can multiple services be migrated to a dedicated instance at the same time?

This needs to evaluated based on the actual conditions:
Scenario 1: if multiple services to be migrated only have the public network access, they can be migrated to the same dedicated instance.

Scenario 2: if multiple services to be migrated have the private network access (to HTTP 8xxx ports and HTTPS 9xxx ports currently):
 - If their private network ports are the same, they can be migrated to the same dedicated instance.
 - Otherwise, they cannot be migrated to the same dedicated instance.

Scenario 3: in scenario 2, if the client supports changing the multiple private network access ports from 8xxx to 80 or from 9xxx to 443, the services can be migrated to the same dedicated instance.

### Can service in all shared instances be migrated to a dedicated instance in an imperceptible manner?

No. For historical reasons, if the original service's domain name suffix is `apigateway.myqcloud.com`, we recommend you not migrate it currently, as migration will be perceptible. However, there is an alternative: you can create a service in the dedicated instance, and then use API Gateway's existing API replication feature to sync the API configuration of the original service to the new service. **If the `myqcloud` domain name is configured in a custom domain name or WAF or hardcoded in the client, it needs to be updated synchronously.**
![](https://qcloudimg.tencent-cloud.cn/raw/d5fa98418bbe4e9c6474b11a9d780872.png)
Replication page:
![](https://qcloudimg.tencent-cloud.cn/raw/700b3c19c567d00ba21776dbac288bba.png)

​           
