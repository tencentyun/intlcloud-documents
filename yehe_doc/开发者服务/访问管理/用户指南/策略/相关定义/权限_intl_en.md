Permissions are used to allow or deny specified operations or access to specified resources under specified conditions.

By default, a root account is the resource owner and has full access to all resources under the account, while a sub-account does not have access to any resources. Resource creators does not automatically possess access to resources they created and needs be authorized by the resource owner.

A policy is a syntax rule used to define and describe one or more permissions. CAM supports two types of policies: preset policies and custom policies. Preset policies are common permission sets created and managed by Tencent Cloud, such as super admin and cloud resource admin. These are read-only and cannot be edited. Custom policies are user-defined permission sets that describe resource management with a finer granularity. The former cannot specifically describe individual resources and has a coarser granularity, while the latter can flexibly meet differentiated permission management needs.

A user or user group can be associated with one or multiple policies for authorization. The authorized policy can either be a preset or custom.
