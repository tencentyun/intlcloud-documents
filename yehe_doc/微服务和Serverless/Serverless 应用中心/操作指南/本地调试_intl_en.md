## Overview
With the local debugging capabilities of Serverless Framework, you can run code in your local simulation environment, send simulated test events, and get information such as execution logs of the function code.

## Prerequisites

The Node.js environment has been installed in your system.

>!
>- Currently, the commands are supported only for Node.js and Python runtimes. In order to ensure that the results of cloud-based deployment and local execution are consistent, we recommend you install the same runtime version locally and in the cloud. For example, if you use Node.js 12.x in the cloud, we recommend you install Node.js 12.x locally.
>- Currently, only the SCF component supports local debugging.
>- Local debugging is supported only for event functions. For web functions, please test them as instructed in [Cloud Test](https://intl.cloud.tencent.com/document/product/583/40689).

## Directions
The code can be triggered locally by running the `sls invoke local` command. The Serverless Framework CLI will run the corresponding code in the specified local directory according to the specified function template configuration file and then implement the execution in the local SCF simulation environment through the specified trigger event.

The related commands are as follows:
```shell
invoke local .................. Invoke the local function
    --function / -f ............ Function name (you can only specify a function name in the yml file in the unified directory)
    --data / -d ................ Serialized event data to be passed to the invoked function (String)
    --path / -p ................ Path to the event JSON file to be passed to the invoked function
    --context .................. Serialized context data to be passed to the invoked function (String)
    --contextPath / -x ......... Path to the context JSON file to be passed to the invoked function
    --env / -e ................. Overwrite environment variable information, such as --env VAR1=val1 --env VAR2=val2
    --config / -c ..............Path to serverless config file
```


## Directions
The following uses Node.js as an example to describe how to perform local debugging:

1. Run the following command to initialize the sample code.
```shell
sls init scf-nodejs && cd scf-nodejs
```
2. Create the test event template `test.json` in the directory. Below is an example:
```json
{
			"value": "test",
			"text": "Hello World event template",
			"context": {
				"key1": "test value 1",
				"key2": "test value 2"
		    }
}
```

3. Create a `.env` file and enter your permanent key. Below is an example:
```
# .env
TENCENT_SECRET_ID=xxxxxxxxxx # `SecretId` of your account
TENCENT_SECRET_KEY=xxxxxxxx # `SecretKey` of your account
```
>?You can also scan the QR code to deploy and get a temporary key to automatically generate the configuration file.
4. Run the following command to view the invocation result locally.
<dx-codeblock>
:::  plaintext
sls invoke local -p xxxx.json
:::
</dx-codeblock>
Below is a sample:
<dx-codeblock>
:::  plaintext
# sls invoke local -p test.json
Hello World
{
  value: 'test',
  text: 'Hello World event template',
  context: { key1: 'test value 1', key2: 'test value 2' }
}
undefined
{}
---------------------------------------------
Serverless: invocation succeeded

{
  value: "test",
  text: "Hello World event template",
  context: {
    key1: "test value 1",
    key2: "test value 2"
  }
}
:::
</dx-codeblock>

