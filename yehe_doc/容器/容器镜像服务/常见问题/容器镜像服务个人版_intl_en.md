
### What is the difference between TCR Personal and Enterprise Edition?
The TCR Personal Edition service is for individual developers. It only provides basic features for container image storage and distribution, and does not provide SLA commitments and relevant compensation. While the Enterprise Edition service is for enterprise users and can provide a secure, dedicated, and high-performance cloud native artifacts hosting and distribution service. For the differences between the two editions, please see [TCR Specifications](https://intl.cloud.tencent.com/document/product/1051/35480).

### What is the resource quota of the TCR Personal Edition?
The resource quota refers to the maximum number of resources that a user can use. The default quota of Personal Edition instance for each user is shown in the following table:

| Quota Item | Default Value |
| -------------------- | ------ |
| Image namespaces in a single region | 10 |
| Image repositories in a single region | 500 |
| Image tags for a single image | 100 |

You can also go to the **Instance Management** page to select a Personal Edition instance and view the current usage details of the account quota. Personal Edition instances don't support quota adjustment. If you need a higher quota, switch to Enterprise Edition.





### Why can't I use image building and trigger in TCR Personal Edition?
To provide more stable and powerful services such as code compilation and image building and deployment, TCR Enterprise Edition now shares the container DevOps features of CODING DevOps. For more information, see [Tencent Container Registry](https://intl.cloud.tencent.com/products/tcr).



### What should I do if I cannot find the pushed image when using the Personal Edition?
Since the image repository of TCR Personal Edition is shared with all other public cloud account resources, the images that have been pulled/pushed are blocked in the queue and are not displayed. You can try to push again, and we recommend that you migrate your services to [TCR Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051) to enjoy the service resources and storage resources of the entire instance.



### Can I migrate the Personal Edition instance to the Enterprise Edition?
Yes. TCR provides you with the data migration and business migration solutions from the Personal Edition to the Enterprise Edition. For more information, please see [Migration from TCR Personal Edition to TCR Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/39844).  
