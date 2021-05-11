Serverless SSR is deployed based on Serverless Framework and supports the following CLI commands:

- **`serverless registry`**: views the list of available components.

- **`serverless registry publish`**: publishes component to Serverless registry.

   `--dev`: publishes component on `@dev` version for development or test.

- **`serverless init xxx`**: downloads a specified template from the Registry by entering the name of the desired template after `init`, such as "$ serverless init fullstack".
  
    `sls init xxx --name my-app`: customizes project directory name.
	
	 `--debug`: lists log information during template download.

- **`serverless deploy`**: deploys component instance in cloud.

    `--debug`: lists log information such as deployment operations and status output by `console.log()` during component deployment.

    `---inputs publish=true`: publishes all function versions under project during deployment

    `---inputs traffic=0.1`: switches 10% traffic to the `$latest` function version during deployment and the rest traffic to the last published function version.

    >?The legacy command format `sls deploy --inputs.key=value` has been changed to `sls deploy --inputs key=value` since Serverless CLI v3.2.3. Legacy commands cannot be used in new versions of Serverless CLI. If you have upgraded Serverles CLI, please use the new commands.

- **`serverless remove`**: removes component instance from cloud.

    `--debug`: lists log information such as removal operations and status output by `console.log()` during component removal.

- **`serverless info`**: gets and displays information related to component instance.

   `--debug`: lists more `state` values.

- **`serverless dev`**: starts development mode ("DEV Mode") and automatically deploys changed information when component status changes are detected. In development mode, information such as execution logs, invocation information, and errors can be output on the command line in real time. In addition, it supports in-cloud debugging for Node.js applications.

   

