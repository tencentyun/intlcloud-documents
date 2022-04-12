## Full Access Policy in HTTPDNS
- Grant a sub-user or collaborator full access (for creating, managing, etc.).
- Policy name: QcloudHTTPDNSFullAccess
```
{
"version": "2.0",
"statement": [
   {
     "effect": "allow",
     "action": [
     "httpdns:*"
     ],
    "resource": "*"
  }
]
}
```

## Read-Only Policy in HTTPDNS
- Grant a sub-user read-only access to HTTPDNS (i.e., the permission to view but not to create, update, or delete all HTTPDNS resources). In the console, the prerequisite to manipulate a resource is the ability to view the resource; therefore, we recommend you grant the sub-account full read access to HTTPDNS.
- Policy name: QcloudHTTPDNSReadOnlyAccess
```
{
"version": "2.0",
"statement": [
   {
      "effect": "allow",
      "action": [
      "httpdns:Describe*"
      ],
      "resource": "*"
    }
]
}
```




