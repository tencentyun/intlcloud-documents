## Overview 

In service rollout and upgrade scenarios, the stability of the deployment process and application is extremely important. This document describes how to use batch deployment to ensure deployment stability when the application is deployed again. 

The batch deployment feature allows you to deploy applications in multiple batches. Each batch updates only a part of the running instances of an application. In addition, you can suspend manual verification and rollback to avoid the impact of faults and the fluctuations in the deployment process. 


## Prerequisites 

You have [created and deployed an application](https://intl.cloud.tencent.com/document/product/1094/40362).  

## Directions 

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem) and click **Application Management** in the left sidebar to go to the application list page. 
2. Select the target application and click the application ID to go to the application details page. 
3. On the application details page, click **Deploy** to go to the redeployment details page.    
	![](https://main.qcloudimg.com/raw/f5a2311e83d298273c933d89eab92671.png)
4. On the deployment details page, configure batch deployment in the **Deployment Policy** area.    
	![](https://main.qcloudimg.com/raw/344bdbf8f0239a1e0d2c9f9a5f434d4e.png)
   - If your application has more than one running instance, redeployment automatically triggers batch deployment. 
   - **Trial Batch**: you can specify a trial batch that contains no more than 50% of the total number of instances. After the execution of the trial batch is completed, you need to manually start the remaining batches.
   - **Deployment Batches**: select the number of batches to launch. Then all instances will be evenly distributed across batches.
   - **How to trigger**: you can choose either to manually or automatically (at an interval of 5 minutes) start the next batch.
   - Deployment flowchart: you can expand the flowchart to view the deployment process and batch details.
5. Click **Deploy** to redirect to the **Instance List** page to start deployment.    
	![](https://main.qcloudimg.com/raw/be40523f08eaf6f04a0a5f0535f8d4d3.png)
6. Click **View Details** in the **Status** parameter in the **Application Overview** area. You can view and manage the batch deployment process in the deployment list.    
	![](https://main.qcloudimg.com/raw/dce950b78faa40a66b7b9ff4eaa131ed.png)
Rollback is to terminate the current deployment process and restore all instances to their previous versions.
