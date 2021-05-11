## Serverless Application

A serverless application consists of one or multiple component instances.

Each component involves a `serverless.yml` file, which defines certain parameters of the component. Such parameters are used to generate the instance information during deployment; for example, the `region` parameter defines the resource region.

Organization is an upper-layer concept of a serverless application and mainly used for management. For example, different departments developing serverless applications in a company can be configured with different organization names for subsequent permission management.

For example, the basic part of developing an Express application is to import the Express component, and some other Tencent Cloud services (such as COS) may also be involved; therefore, the directories of the entire application are as shown below:

![](https://main.qcloudimg.com/raw/2c3851a85c128fc7da66f68272ed7fbc.svg)

## serverless.yml File

The `serverless.yml` file defines the application organization description and the component's `inputs` parameters. During each deployment, resources will be created, updated, and orchestrated according to the configuration information in the `serverless.yml` file.

The following is a simple `serverless.yml` file:
```
# serverless.yml

org: xxx-department # Organization information. The default value is your Tencent Cloud `APPID`
app: expressDemoApp # Application name, which is the component instance name by default
stage: ${env:STAGE} # Parameter used to isolate the development environment, which is `dev` by default


component: express # Name of the imported component, which is required. The `express-tencent` component is used in this example
name: expressDemo # Name of the instance created by the component, which is required


inputs:
  src:
    src: ./ 
    exclude:
      - .env
  region: ap-guangzhou 
  runtime: Nodejs10.15
  functionName: ${name}-${stage}-${app}-${org} # Function name
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

Configuration information in the `.yml` file:

<table>
	<tr>
		<th colspan="2">Parameter</th>
		<th>Description</th>
	</tr>
	<tr>
		<td rowspan="3">Application information</td>
		<td> org</td>
		<td>Organization information, which is your Tencent Cloud `APPID` by default.</td>
	</tr>
	<tr>
		<td>  app</td>
		<td>Application name, which is the component instance name by default.</td>
	</tr>
		<tr>
		<td> stage</td>
		<td>Environment information, which is `dev` by default. You can define different `stage` values to provide independent runtime environments for development, testing, and release of the serverless application, respectively.</td>
	</tr>
	<tr>
		<td rowspan="2">Component information</td>
		<td> component</td>
		<td>Name of the imported component. You can run <code>sls registry</code> to query components available for import.</td>
	</tr>
	<tr>
		<td>  name</td>
		<td>Name of the created instance. An instance will be created when each component is deployed.</td>
	</tr>
		<tr>
		<td colspan="2">Parameter information</td>
		<td>The parameters under `inputs` are configuration parameters of the corresponding component. Different components have different parameters. To guarantee environment isolation and resource uniqueness, the component resource names are in the <code>${name}-${stage}-${app}-${org}</code> format by default.</td>
	</tr>
</table>


