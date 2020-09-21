Serverless Framework supports the following CLI commands:

- **`serverless registry`**: views the list of available components.

- **`serverless registry publish`**: publishes the component to the Serverless registry.

   `--dev`: publishes the component on the `@dev` version for development or testing.

- **`serverless init xxx`**: downloads a specified template from the Registry by entering the name of the desired template after `init`, such as "$ serverless init fullstack".
    
    `sls init xxx --name my-app`: customizes the project directory name.

	 `--debug`：lists log information during the template download process.

- **`serverless deploy`**: deploys the component instance in the cloud.

    `--debug`: lists log information such as the deployment operations and the status output by `console.log()` during component deployment.
    
    `---inputs.publish`: during deployment, publishes all function versions under the project.
    
    `---inputs.traffic=0.1`: switches 10% of the traffic to the `$latest` function version during deployment and the rest of the traffic to the last published function version.

- **`serverless remove`**: removes the component instance from the cloud.

    `--debug`: lists log information such as the removal operations and the status output by `console.log()` during component removal.

- **`serverless info`**: gets and displays information related to the component instance.

   `--debug`: lists more `state` values.

- **`serverless dev`**: starts the development mode ("DEV Mode") and automatically deploys changed information when component status changes are detected. In the development mode, information such as execution logs, invocation information, and errors can be outputted on the command line in real time. In addition, it supports in-cloud debugging for Node.js applications.
