## Basic Features
You can quickly delete cloud resources by running the following command:

```sh
sls remove
```


## Advanced Features
- View specific log information during deletion:
```
sls remove --debug
```

- There are multiple Serverless instances in the application directory, and you want to delete the specified project only:
```
sls remove --target xxx
```
For example, in the project root directory, you can run the `sls remove --target ./cos` command to delete the COS instance only without affecting other instances.
```
.
├── src
│   ├── serverless.yml 
│   └── index1.js 
├── cos
│   └── serverless.yml 
├── db
│   └── serverless.yml 
└── .env 
```


## FAQs
#### What cloud resources will be removed when `sls remove` is executed?
  
Serverless Framework removes cloud resources according to the `.yml` configuration file. Resources created through the `.yml` file will be deleted, while imported existing resources will not. For example: 
- When deploying a function through the SCF component, if you choose to create an API Gateway trigger for deployment, then when you run the command for deletion, the created function and API Gateway resources will be deleted.
- If you select an existing API Gateway trigger for deployment, then only the function resources will be deleted, while the used API Gateway trigger will not.
