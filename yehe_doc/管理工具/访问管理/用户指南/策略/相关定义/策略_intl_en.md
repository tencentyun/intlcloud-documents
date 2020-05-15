A policy is a syntax rule used to define and describe one or more permissions. CAM supports two types of policies: preset policies and custom policies. It offers multiple ways to create and manage policies from different perspectives. If you need to add permissions to a CAM user or group, you can directly associate a preset policy or create a custom policy for association. Each policy can contain multiple permissions, and you can also choose to bind multiple policies to one CAM user or group.

### Preset Policy
Preset policies are common permission sets created and managed by Tencent Cloud that are frequently used by users, such as super admin and full resource access. Preset policies cover a wide range of operation objects at a coarse operation granularity. They are preset by the system and cannot be edited by users.

### Custom Policy
Custom policies are user-defined permission sets that describe resource management with finer granularity. It allows fine-grained permission division and can flexibly meet your differentiated permission management needs. For example, you can associate a policy with a database admin so that the admin has the permissions to manage TencentDB instances but not CVM instances.
