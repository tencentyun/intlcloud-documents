Image repository triggers automate actions such as service update, webhooks, and message push after images are created. By using triggers with continuous integration, you can implement continuous deployment.

An image repository trigger contains the following attributes:
- Trigger Name: indicates the name of the trigger.
- Image Repository: specifies an image repository to be bound with the trigger. Currently, an image repository can be bound with up to 10 triggers.
- Trigger Condition: specifies that a trigger action is performed only if an image that has a specific tag is submitted.
- Trigger Action: currently, only the TKE update action is supported. More trigger actions, such as webhooks and message push, will be available soon.

## Triggering Conditions
Currently, Tencent Cloud TKE Image Registry supports three types of tag trigger expressions, which can be used to configure trigger conditions:
- All: the action is triggered whenever a tag is created or updated in the image repository.
- Specified tags: enter multiple tags and separate them with semicolons (;). The action is triggered when images with the specified tags are created or updated in the image repository.
- Regular expression: the action is triggered when a matching tag is created or updated in the image repository.

## Action
Currently, service update is the only supported trigger action. The configuration of the trigger action includes setting the region, cluster, namespace, service, container image, and other parameters of TKE.
When a trigger condition is met, the specified container image of the service is updated based on the set parameters.

## Triggering History
Every time a repository trigger performs an action, a triggering history entry is generated, which contains information such as the trigger name, triggering condition, action, trigger result, and triggered time.
