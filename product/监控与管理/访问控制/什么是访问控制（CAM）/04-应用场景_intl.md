### Enterprise sub-account permission management

Enterprise employees should have the minimal access permissions to the enterprise's cloud resources, based on their positions.
Scenario: An enterprise has many cloud resources (CVM, VPC instances, CDN instances, COS buckets and objects, etc.) and many employees (developers, testers, OPS personnel, etc.). Some developers need the read and write permissions to the project-related cloud resources on the development servers. Testers need the read and write permissions to the project-related cloud resources on the test servers. OPS personnel are responsible for the purchase and daily operation of the servers. if the responsibilities or projects of an employee have changed, the corresponding permissions should be terminated.

### Cross-enterprise permission management

Different enterprises need to share cloud resources.
Scenario: An enterprise that has many cloud resources wants to focus on product research and development, and to delegate its OPS of cloud resources to another operating enterprise. When their delegation contract terminates, the enterprise will revoke the corresponding management permissions.
