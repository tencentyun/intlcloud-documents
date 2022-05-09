
<dx-alert infotype="explain" title="">
The entries of TCR Enterprise and TCR Individual in the console are merged. To provide you with more powerful and stable code compilation, image building and image deployment services, the image building of TCR Individual is now supported by CODING DevOps service. You can select the desired image repository in the new console to configure images. You can configure webhook through “Operation Center - Trigger” to realize connection with the external release system. The image building and trigger features in the legacy console are only provided for existing users, and configurations cannot be added.
</dx-alert>


An image repository trigger can automatically push images. It does not support connecting with external webhook servers.

An image repository trigger contains the following four attributes:
- Trigger name: It indicates the name of the trigger.
- Image repository: It specifies an image repository to be bound with the trigger. Currently, an image repository can be bound with up to 10 triggers.
- Trigger condition: It specifies that a trigger action is performed only if an image that has a specific tag is submitted.
- Trigger action: It only supports triggering updates of TKE.

## Triggering Conditions
Currently, Tencent Cloud TKE Image Registry supports three types of tag trigger expressions, which can be used to configure trigger conditions:
- All: The action is triggered whenever a tag is created or updated in the image repository.
- Specified tags: Enter multiple tags and separate them with semicolons (;). The action is triggered when images with the specified tags are created or updated in the image repository.
- Regular expression: The action is triggered when a matching tag is created or updated in the image repository.

## Trigger Action
Currently, service update is the only supported trigger action. The configuration of the trigger action includes setting the region, cluster, namespace, service, container image, and other parameters of TKE.
When a trigger condition is met, the specified container image of the service is updated based on the set parameters.

## Triggering History
Every time a repository trigger performs an action, a triggering history entry is generated, which contains information such as the trigger name, triggering condition, trigger action, trigger result, and triggered time.







