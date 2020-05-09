
## Ease of Use

### Reduced component overheads

When using SCF, you don't have to take care of peripheral components such as load balancing, automatic scaling, and gateways; instead, you only need to write core codes, which greatly reduces service architecture complexity.

### Automatic scaling

SCF can scale based on the amount of requests with no manual configuration required. Regardless of whether your application receives only couples of requests daily (e.g., scheduled transactions such as log collection) or handles thousands of requests per second (e.g., backend of a mobile app), SCF can automatically arrange reasonable computing resources to meet the business needs.

## Efficient Development

### Accelerated development

SCF does not require specific frameworks or dependencies, so developers can focus on the development of core code. In addition, they can form multiple small teams, and the development of individual modules does not require knowledge of the details of code written by other teams, which significantly accelerates independent development and iteration and helps optimize the timing of product launches.

### Reuse of third-party services

You can use SCF to write some single-purpose, logically independent business modules, so that you can fully reuse mature third-party code implementations, such as using OAuth to implement a login module.

### Simplified OPS

Each function is executed, deployed, and scaled separately and can be automatically deployed after you upload the corresponding code, which eliminates the trouble with deploying and upgrading standalone applications.

## Stability and Reliability

### High-availability deployment

SCF can automatically select a random availability zone in each region for function execution. If an availability zone is down due to a natural disaster or power failure, SCF can automatically select the infrastructure of other availability zones for code execution, eliminating the risk of service interruption inherent in single-availability zone operations.

### Supplement to other computing services

Resident workloads can be sustained by CVM or TKE, while event-triggered workloads can be sustained by SCF. Different Tencent Cloud services can be leveraged to meet the needs of different business scenarios and make your service architecture even more robust.

## Simplified Management

### Simple security configuration

With SCF, complex configuration and management of OS intrusions, login risks, file system security, network security and port monitoring become a thing of the past. Everything is handled by the platform which ensures user isolation through customized containers.

### Visual Management

You can directly manage the function code and execution time (i.e., function trigger) in the console, and deploy and test functions in one click with no complicated configuration files needed.

## Significantly Reduced Overheads

### Usage-based billing

SCF does not incur any fees when it is not in use, so the costs will be significantly reduced for non-resident business processes. When the SCF executes code, you will be billed for the number of requests and the execution duration of the computing resources. This billing mode has obvious advantages and is very friendly to developers in the start-up stage.

