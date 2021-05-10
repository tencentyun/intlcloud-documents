### What should I do if installation is too slow?
To ensure the installation speed and stability, we recommend you use cnpm for installation. Install cnpm first by running the command `npm install -g cnpm --registry=https://registry.npm.taobao.org`, and then replace all the npm commands used with cnpm commands.

### Why does an entered serverless command not take effect?
When initializing a project, you must ensure that there is no `serverless.yml` file in the current directory; otherwise, the CLI will deem that the current directory is already a serverless project and cannot initialize the application.
