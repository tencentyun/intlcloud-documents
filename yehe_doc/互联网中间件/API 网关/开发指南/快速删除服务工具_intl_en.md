## Operation Scenarios
To avoid business losses caused by accidental service deletion, you cannot directly delete a service if it contains APIs or activated services. You have to deactivate the service first, query its API list, batch delete the service APIs, and then delete the service, which is a complex process.

To cope with this problem, Tencent Cloud API Gateway team and Tencent Cloud Serverless Framework team have launched the Serverless Cleaner to quickly delete the API gateway service.

## Directions
1. Click [here](https://github.com/serverless-plus/serverless-cleaner) to download Serverless Cleaner.
2. Use CLI to go to the directory where Serverless Cleaner is located.
3. On the CLI, run the following commands to install dependencies.
```shell
$ npm install
```
4. After dependency installation, go to the directory where Serverless Cleaner is located, copy `config.example.js`, and rename it as `config.js`.
5. Modify `config.js` based on the information of the services to delete.
```JavaScript
module.exports = {
	tencent: {
		// Resource region. You can enter the following resource region if the region is not modified.
		region: 'ap-guangzhou',
		// Identity verification
		credentials: {
			SecretId: '',
			SecretKey: '',
		},
		apigwOptions: {
			// IDs of the services that you do not want to delete. Before you use Serverless Cleaner, add IDs of important services here to avoid affecting business.
			exclude: [],
			// IDs of the services that you want to delete. include has a higher priority than exclude. If the same service ID exists in exclude and include, the service will be deleted.
			include: [],
		},
		scfOptions: {
			// Specify this option when you delete SCF resources. When deleting only the API Gateway service, you do not need to specify this option.
			exclude: [],
			include: [],
		},
	},
};
```
6. On the CLI, run the following commands to delete the API Gateway service.
```shell
$ npm run clean
```
