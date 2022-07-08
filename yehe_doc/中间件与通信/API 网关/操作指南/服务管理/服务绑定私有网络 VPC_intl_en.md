## Overview
After binding a [VPC](https://console.cloud.tencent.com/vpc) attribute to the service, you can create APIs interconnected with backend resources in the VPC in the service.

## Binding Service to VPC in Shared Instance
### Binding VPC during service creation
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/service).
2. Click **Service** on the left sidebar.
3. In the current region, click **Create** in the top-left corner to create a service. In **Basic Information Configuration**, select **Shared Type** for the instance type. In **Network and Optional Configuration**, you can bind the created service to a VPC in the same region.

### Binding VPC on service details page
If you don't bind any VPCs during service creation, you can bind one on the service details page to interconnect with VPC resources.
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/service).
2. Click **Service** on the left sidebar.
3. Select the target service and click the **service name** to enter the service details page.
4. Select **Basic configurations** on the service details page to enter the **Basic configurations** page.
5. On the **Basic configurations** page, find the **VPC** field in **Network**, click the **edit icon** after the field, and then you can bind the service to a VPC in the pop-up window.


## Binding Service to VPC in Dedicated Instance
As a dedicated instance has the VPC attribute, you don't need to manually bind it to a VPC. When creating a service in the instance, the VPC field will be automatically set to the VPC of the instance.
