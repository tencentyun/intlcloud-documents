Serverless Framework supports the following CLI commands:
- **`serverless registry`**: views the list of available components.

- **`serverless registry publish`**: publishes component to Serverless registry.
`--dev`: publishes component on `@dev` version for development or test.

- **`serverless init -t`**: download the specified template from the registration center.

- **`serverless deploy`**: deploys component instance in cloud.
`--debug`: lists log information such as deployment operations and status output by `console.log()` during component deployment.
`--all`: traverses components in subdirectories under the root directory, generates dependencies, and deploys resources based on dependency order.

- **`serverless remove`**: removes component instance from cloud.
`--debug`: lists log information such as removal operations and status output by `console.log()` during component removal.
`--all`: traverses components in subdirectories under the root directory, generates dependencies, and removes resources based on dependency order.

- **`serverless info`**: gets and displays information related to component instance.
`--debug`: lists more `state` values.

- **`serverless dev`**: starts development mode ("DEV Mode") and automatically deploys changed information when component status changes are detected. In development mode, information such as execution logs, invocation information, and errors can be output on the command line in real time. In addition, it supports in-cloud debugging for Node.js applications.

