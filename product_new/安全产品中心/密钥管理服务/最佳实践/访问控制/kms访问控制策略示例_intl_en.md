
#### KMS policy for full read/write permission
The following policy grants a sub-account permissions for all operations. The Action element specifies all KMS-related APIs.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/kms:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
#### KMS policy for read-only permission
The following policy grants a sub-account permission to only query your KMS resources, but not create, update, or delete the resources. 
We recommend granting the sub-account full read permission, because the user has to view the resource before working on it in the console.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/kms:ListKey",
                "name/kms:GetKeyAttributes"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

#### Grant a sub-account permission to perform administrative operations

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/kms:CreateKey",
                "name/kms:ListKey",
                "name/kms:GetKeyAttributes",
                "name/kms:SetKeyAttributes"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

#### Grant a sub-account permission to perform data-related but not administrative operations

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/kms:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/kms:CreateKey",
                "name/kms:ListKey",
                "name/kms:GetKeyAttributes",
                "name/kms:SetKeyAttributes"
            ],
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```
