When creating or editing a function, you can add, delete, or modify environment variables for the function runtime environment by modifying the environment variables in the configuration.

The configured environment variables will be configured into the OS environment when the function is executed. The function code can read the system environment variables to obtain the specific values and use them in the code.

## Adding Environment Variable
### Adding environment variable in console
1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. When creating or editing a function, you can add environment variables in "Environment Variable".
Environment variables usually appear as `key-value` pairs. Enter the required environment variable key in the first input box and the required value in the second one.

### Adding environment variable locally
For local development, you can configure the `Environment` environment variable directly under the function in `serverless.yml` and run the `sls deploy` command to deploy it to the cloud as shown below:
```yaml
component: scf # Component name, which is required. It is `scf` in this example
name: scfdemo # Component instance name, which is required

# Component parameter configuration
inputs:
  name: scfdemo # Function name, which is `${name}-${stage}-${app}` by default
  namespace: default
  # 1. Default format. Create a specifically named COS bucket and upload it
  src: ./src
  type: event # Function. Valid values: event - event-triggered (default), web - HTTP-triggered
  handler: index.main_handler # Entry (valid if the function is event-triggered)
  runtime: Nodejs10.15 # Runtime environment, which is Nodejs10.15 by default
  region: ap-guangzhou # Function region
  description: This is a function in ${app} application.
  memorySize: 128 # Memory size in MB
  timeout: 20 # Function execution timeout period in seconds
  initTimeout: 3 # Initialization timeout period in seconds
  environment: # Environment variable
    variables: # Environment variable object
      TEST1: value1
      TEST2: value2
```

## Viewing Environment Variable

After configuring environment variables for the function, you can query the specific configured environment variables by viewing the function configuration, which are displayed in the form of `key=value`.


## Using Environment Variable

The configured environment variables will be configured into the runtime environment when the function is executed. The code can read the system environment variables to get the specific values and use them in the code. It should be noted that **environment variables cannot be read locally**.
Suppose the key of the configured environment variable for a function is `key`. The following is the sample code for reading and printing the value of this environment variable in different runtime environments.
- In a Python runtime environment, the way to read the environment variables is as follows:
```
import os
value = os.environ.get('key')
print(value)
```
- In a Node.js runtime environment, the way to read the environment variables is as follows:
```
var value = process.env.key
console.log(value)
```
- In a Java runtime environment, the way to read the environment variables varies by temporary authorized fields and other fields:
 - For temporary authorized fields (including `TENCENTCLOUD_SESSIONTOKEN`, `TENCENTCLOUD_SECRETID`, and `TENCENTCLOUD_SECRETKEY`), the way to read the environment variables is as follows:
```
System.out.println("value: "+ System.getProperty("key"));
```
 - For other fields, the way to read the environment variables is as follows:
```
System.out.println("value: "+ System.getenv("key"));
```
- In a Go runtime environment, the way to read the environment variables is as follows:
```
import "os"
var value string
value = os.Getenv("key")
```
- In a PHP runtime environment, the way to read the environment variables is as follows:
```
$value = getenv('key');
```








## Use Cases

- **Variable value extraction**: values that may change in the business can be extracted into environment variables, eliminating the need to modify the code according to business changes.
- **External storage of encrypted information**: keys related to authentication and encryption can be extracted from the code into environment variables, avoiding security risks caused by the presence of relevant keys hard-coded in the code.
- **Environment differentiation**: the configuration and database information for different development stages can be extracted into the environment variables, so that in different stages of development and release, you only need to modify the environment variable values and execute the development environment database and release environment database separately.

## Use Limits

The following use limits apply to the environment variables of functions: 
- The key must begin with a letter (**[a-zA-Z]**) and can only contain alphanumeric characters and underscores (**[a-zA-Z0-9\_]**).
- The keys of reserved environment variables cannot be modified, including:
 - Keys beginning with SCF\_, such as SCF\_RUNTIME.
 - Keys beginning with QCLOUD\_, such as QCLOUD\_APPID.
 - Keys beginning with TENCENTCLOUD\_, such as TENCENTCLOUD\_SECRETID.


## Built-in Environment Variables

The `Key` and `Value` of built-in environment variables in the current runtime environment are as shown in the table below:


<table>
<thead>
<tr>
<th nowrap="nowrap">Environment Variable Key</th>
<th>Specific Value or Value Source</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap"><code>TENCENTCLOUD_SESSIONTOKEN</code></td>
<td>{Temporary SESSION TOKEN}</td>
</tr>
<tr>
<td><code>TENCENTCLOUD_SECRETID</code></td>
<td>{Temporary SECRET ID}</td>
</tr>
<tr>
<td><code>TENCENTCLOUD_SECRETKEY</code></td>
<td>{Temporary SECRET KEY}</td>
</tr>
<tr>
<td><code>_SCF_SERVER_PORT</code></td>
<td>28902</td>
</tr>
<tr>
<td><code>TENCENTCLOUD_RUNENV</code></td>
<td>SCF</td>
</tr>
<tr>
<td><code>USER_CODE_ROOT</code></td>
<td>/var/user/</td>
</tr>
<tr>
<td><code>TRIGGER_SRC</code></td>
<td>Timer (if a timer trigger is used)</td>
</tr>
<tr>
<td><code>PYTHONDONTWRITEBYTECODE</code></td>
<td>x</td>
</tr>
<tr>
<td><code>PYTHONPATH</code></td>
<td>/var/user:/opt</td>
</tr>
<tr>
<td><code>CLASSPATH</code></td>
<td>/var/runtime/java8:/var/runtime/java8/lib/*:/opt</td>
</tr>
<tr>
<td><code>NODE_PATH</code></td>
<td>/var/user:/var/user/node_modules:/var/lang/node6/lib/node_modules:/opt:/opt/node_modules</td>
</tr>
<tr>
<td><code>_</code></td>
<td>/var/lang/python3/bin/python3</td>
</tr>
<tr>
<td><code>PWD</code></td>
<td>/var/user</td>
</tr>
<tr>
<td><code>LOGNAME</code></td>
<td>qcloud</td>
</tr>
<tr>
<td><code>LANG</code></td>
<td>en_US.UTF8</td>
</tr>
<tr>
<td><code>LC_ALL</code></td>
<td>en_US.UTF8</td>
</tr>
<tr>
<td><code>USER</code></td>
<td>qcloud</td>
</tr>
<tr>
<td><code>HOME</code></td>
<td>/home/qcloud</td>
</tr>
<tr>
<td><code>PATH</code></td>
<td>/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin</td>
</tr>
<tr>
<td><code>SHELL</code></td>
<td>/bin/bash</td>
</tr>
<tr>
<td><code>SHLVL</code></td>
<td>3</td>
</tr>
<tr>
<td><code>LD_LIBRARY_PATH</code></td>
<td>/var/runtime/java8:/var/user:/opt</td>
</tr>
<tr>
<td><code>HOSTNAME</code></td>
<td>{host id}</td>
</tr>
<tr>
<td><code>SCF_RUNTIME</code></td>
<td>Function runtime</td>
</tr>
<tr>
<td><code>SCF_FUNCTIONNAME</code></td>
<td>Function name</td>
</tr>
<tr>
<td><code>SCF_FUNCTIONVERSION</code></td>
<td>Function version</td>
</tr>
<tr>
<td><code>TENCENTCLOUD_REGION</code></td>
<td>Region</td>
</tr>
<tr>
<td><code>TENCENTCLOUD_APPID</code></td>
<td>Account APPID</td>
</tr>
<tr>
<td><code>TENCENTCLOUD_UIN</code></td>
<td>Account UIN</td>
</tr>
<tr>
<td><code>TENCENTCLOUD_TZ</code></td>
<td>Time zone, which is UTC currently</td>
</tr>
</tbody></table>
