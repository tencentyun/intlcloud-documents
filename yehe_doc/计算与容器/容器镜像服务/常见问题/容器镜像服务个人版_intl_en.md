
### What is the difference between TCR Personal and Enterprise Edition?
The TCR Personal Edition service is for individual developers. It only provides basic features for container image storage and distribution, and does not provide SLA commitments and relevant compensation. While the Enterprise Edition service is for enterprise users and can provide a secure, dedicated, and high-performance cloud native artifacts hosting and distribution service. For the differences between the two editions, please see [TCR Specifications](https://intl.cloud.tencent.com/document/product/1051/35480).

### What is the resource quota of the TCR Personal Edition?
The resource quota refers to the maximum number of resources that a user can use. The default quota of Personal Edition instance for each user is shown in the following table:

| Quota Item | Default Value |
| -------------------- | ------ |
| Image namespaces in a single region | 10 |
| Image repositories in a single region | 500 |
| Image tags for a single image | 100 |

You can go to [TKE console](https://console.cloud.tencent.com/tke2/overview) to view the quota details of the current account. If you need a higher quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS) for application.



### What should I do if I cannot find the pushed image when using the Personal Edition?
Since the image repository of TCR Personal Edition is shared with all other public cloud account resources, the images that have been pulled/pushed are blocked in the queue and are not displayed. You can try to push again, and we recommend that you migrate your services to [TCR Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051) to enjoy the service resources and storage resources of the entire instance.



### Can I migrate the Personal Edition instance to the Enterprise Edition?
Yes. TCR provides you with the data migration and business migration solutions from the Personal Edition to the Enterprise Edition. For more information, please see [Migration from TCR Personal Edition to TCR Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/39844).  
