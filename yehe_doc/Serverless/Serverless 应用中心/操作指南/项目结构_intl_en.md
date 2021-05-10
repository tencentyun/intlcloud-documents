Serverless Framework deploys applications based on the [Serverless components](https://github.com/serverless/components/blob/master/README.cn.md). There are no mandatory requirements for the local project structure, but for the ease of management and deployment, we recommend you organize your application in the following directory structure:

## Single-Function Application
For single-function applications, you can place your business code in the `src` directory and import this directory in the `serverless.yml` configuration file to achieve separate management of the project and the configuration file. Below is an example:

```
.
├── serverless.yml  # Configuration file
├── src
│   ├── package.json # Dependency file
│   └── index.js # Entry function
└── .env # Environment variable file
```

## Multi-Function/Multi-Resource Application
Serverless Framework not only supports deploying single-function projects, but also can implement unified deployment at the application level for multi-function projects. You should configure the corresponding configuration file for each function; therefore, we recommend the following directory structure:

```
.
├── package.json # Dependency file
├── function1
│   ├── serverless.yml # Configuration file of function 1
│   └── index1.js # Entry function 1
├── function2
│   ├── serverless.yml # Configuration file of function 2
│   └── index2.js # Entry function 2
└── .env # Environment variable file
```
Under this structure, you only need to run `sls deploy` in the root directory, and Serverless Framework will automatically traverse all the `.yml` configuration files in the directory to deploy resources.

Meanwhile, if you import the creation of other cloud resources in the function project, you can also use the same directory structure:
```
.
├── package.json # Dependency file
├── src
│   ├── serverless.yml # Function configuration file
│   └── index1.js # Entry function
├── cos
│   └── serverless.yml # COS bucket configuration file
├── db
│   └── serverless.yml # Database configuration file
└── .env # Environment variable file
```
