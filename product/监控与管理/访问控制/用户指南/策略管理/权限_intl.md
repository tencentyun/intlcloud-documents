Permission is used to authorize or deny specific access to resources.
    
By default, the root account is the owner of resources and thus has full permission to access all of its resources. The sub-accounts have no permissions to access any resources; the resource creators do not automatically have permissions to access resources they created. They need permissions authorized by the resource owner to access the resources.
    
The Policy is the syntax rule used to define and describe one or more permissions. CAM supports two types of policies: preset policy and custom policy. The preset policy (read-only) is a collection of common permissions created and managed by Tencent Cloud, such as SuperAdmin, cloud resource Admin. The custom policy is a collection of user-created permissions that describe resources management at a granular level, thus providing greater flexibility to meet different user needs than the preset policy, which cannot specifically describe resources.
    
You can grant permissions to users or user groups by associating them with one or more policies. The authorized policy can be either a preset policy or a custom policy.
