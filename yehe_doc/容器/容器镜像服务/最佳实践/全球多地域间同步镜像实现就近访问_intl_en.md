## Overview
When an enterprise expands the container service to multiple regions, it may want that container images can be pulled from the nearest nodes to accelerate pull and reduce the cross-region public network traffic costs; it may also want to implement hot backup across multiple regions and transfer images between multiple image registry services in the same region for cross-team sharing or flow from the development repository to the production repository. In the aforementioned scenarios, the traditional best practice is to create and maintain multiple container image registries (Docker Registry) in one or multiple regions and write scripts to call `docker push` or `docker pull` to implement cross-registry image replication. TCR Enterprise Edition also supports on-demand cross-instance image synchronization as well as single-instance multi-region replication. You can select and combine them flexibly as needed to meet your requirements. The two features have the following strengths:

#### Instance synchronization
Specified images can be automatically synced between multiple instances in the same region or multiple regions as needed.
- On-demand synchronization: target instances and images to be synced can be precisely matched and selected based on custom rules.
- Automatic synchronization: after the image to be synced is pushed to the source instance, it will be automatically synced to the target instance.
- Cross-tenant synchronization: public images can be synced between instances across multiple root accounts in the same enterprise.
- Helm Chart and container image can be filtered, and you can choose to sync only one type of cloud native artifacts.
- You can query synchronization logs, which can be used with a webhook to implement synchronization success event notification.

#### Instance replication
TCR enables you to configure replicas (replica instances) in multiple regions for a single instance and supports nearby access.
- Single instance: if a single instance needs to be accessed in multiple regions, you can use the same image repository name/tag to maintain consistent container configurations.
- Nearby access: in multi-region deployment, image data in the same region can be pulled to improve the deployment efficiency and stability.
- Reduced costs: nearby image pull over private network can reduce the public network traffic fees or Direct Connect fees incurred in cross-region image registry access.
- Simplified management: you don't need to manage multiple instances, configure synchronization rules between instances, or care about the synchronization status of the specified image.
- Quick synchronization: the image layer data is replicated across regions in real time in a streaming manner; therefore, once pushed to one region, an image can be pulled from multiple regions.

## Use Cases
### Scenario 1: nearby access in multiple global regions for international business
A game developer wants to deploy a containerized gaming business in multiple regions around the globe at the same time and needs to implement multi-region synchronization and nearby access of container images. In addition, as restricted by data compliance regulations, it requires separate management of data in and outside the Chinese mainland for data transfer control. It uses the following solution to implement multi-region data synchronization and nearby access, maintain unified configurations, and greatly improve the business release efficiency and stability.

![](https://qcloudimg.tencent-cloud.cn/raw/892c4b757db9af5b0e7b62b632710018.png)

In this solution, the customer creates two independent instances at the same time in Beijing and Frankfurt, configures instance synchronization rules, and syncs the images released for the production environment as needed. In addition, it configures multiple replica instances in both the Beijing and Frankfurt instances. The Beijing instance contains three replica instances: Shanghai, Chengdu, and Guangzhou. When the latest game version needs to be released, the Beijing development team pushes the latest container image tags for the Chinese mainland and the regions outside the Chinese mainland. Here, the tag for regions outside the Chinese mainland will be automatically pushed to the Frankfurt instance and replicated to regions including Silicon Valley, Virginia, Mumbai, and Singapore. When the container cluster in Singapore updates the image to the latest tag, it can access the replica instance in Singapore over the private network for quick and stable production container update.

### Scenario 2: image transfer between multiple subsidiaries and businesses in a large enterprise
A large enterprise has many subsidiaries and business groups, among which a subsidiary has multiple businesses and independent IT teams for them. To separately manage the permissions and costs of cloud resources, many subsidiaries and businesses use different Tencent Cloud root accounts. The enterprise uses the following solution to share the basic images within it and share images between multiple businesses:

![](https://qcloudimg.tencent-cloud.cn/raw/9ba42f29cd0dc8c7d5ae9e916c0718b6.png)

In this solution, cross-tenant instance synchronization is configured between instances under multiple subsidiary accounts to share public images. The basic platform admin configures the basic image synchronization between business instances in each subsidiary in a unified manner. Some businesses plan to use multiple instances to separately manage images during business development, testing, and production and automatically transfer business images between each production stages based on image tag.

> ! Both of the above scenarios are quite complex, and you can choose a certain part of the solutions to meet your requirements in regular businesses, such as cross-region hot backup, multi-region nearby access, and intra-region cross-instance business image flow.
> In addition, an Enterprise Edition instance allows you to leverage the custom domain name feature. Together with DNS, you can use the same domain name for multiple instances to implement unified image release configuration and multi-region nearby access over private network, which helps you manage instances more flexibly.

## Operation Guide
### Prerequisites
- You have [purchased a TCR Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088) with standard specification (for the instance synchronization feature) or premium specification (for the instance synchronization or replication feature).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

### Configuring instance synchronization
For detailed directions, see [Configuring Instance Synchronization](https://intl.cloud.tencent.com/document/product/1051/35494).
Instance synchronization supports cross-tenant instance synchronization, and you can configure it when creating a synchronization rule.


### Configuring instance replication
For detailed directions, see [Configuring Instance Replication](https://intl.cloud.tencent.com/document/product/1051/39845).
Instance replication doesn't support replication between regions in and outside the Chinese mainland; for example, you cannot configure a replica instance in the Silicon Valley region for a premium instance in the Beijing region.


### Configuring custom domain name
For detailed directions, see [Configuring Custom Domain Name](https://www.tencentcloud.com/document/product/1051/43983).
Custom domain name DNS needs to be configured independently. For Tencent Cloud, you can use Private DNS. For Tencent Cloud International, Private DNS is not supported currently, and we recommend you use a self-built DNS service.


## Troubleshooting Guide
#### 1. What should I do if instance synchronization failed?
You can go to the TCR console, view the relevant rules and synchronization logs, and manually trigger synchronization. If the synchronization is slow or still fails, [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for assistance.
#### 2. What should I do if instance replication failed?
Currently, instance replication doesn't allow you to view the synchronization logs of the specific repository. Wait patiently during instance replication and try accessing the image after the status becomes "Synced successfully". If the instance replication status doesn't become "Synced successfully" or you still cannot get the image after successful synchronization, [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for assistance.
#### 3. How do I know whether the specified image has been replicated to a replica instance?
Currently, instance replication allows you to view historical synchronization tasks. You can check the task details logs to determine the synchronization status of the specified image repository or image.
#### 4. How do I accelerate cross-region instance synchronization?
Currently, you cannot accelerate cross-region synchronization of the specified account or instance. The synchronization speed is subject to the cross-region CCN bandwidth, which is shared between multiple tenants. If you want a special guarantee, [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for assistance.



