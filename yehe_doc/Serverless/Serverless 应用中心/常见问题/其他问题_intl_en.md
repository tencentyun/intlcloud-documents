### What should I do if Serverless Framework prompts that `"component" input is requires to run custom methods`?

When the Serverless Framework CLI is started, if a component is referenced in the `yaml` configuration file by default, you need to make sure that the folder is empty before you can run the component installation command properly.
Running the `serverless create` command again in an empty folder will not cause this error.

If you have any other questions or feedback, please visit [GitHub Repository Issues](https://github.com/serverless-components?q=tencent).
