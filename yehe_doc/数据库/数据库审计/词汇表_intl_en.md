### Database Audit
Database Audit can record the activities of TencentDB instances in real time, manage the compliance of database operations with fine-grained audit, and alert risky database behaviors such as SQL injections and exceptional operations.

### Audit Policy
An audit policy defines what behaviors are to be audited and how to audit them. **Audit policy** = **audit object** + **audit rule** + **responsive action**. In other words, when configuring an audit policy, you need to specify the things to be audited, and if the characteristics of certain (user or system) behaviors hit an audit rule after being analyzed during the validity period of the policy, then the audit engine will take responsive actions as defined in the policy.

### Audit Object
It is the target instance (database) you set.

### Audit Rule
A rule is a collection of behaviors that need to be audited as defined in an audit policy. It consists of rule parameters, each of which defines a specific characteristic for behavior matching.
