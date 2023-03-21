When creating or editing a function, you can add, delete, or modify environment variables for the function runtime environment by modifying the environment variables in the configuration.

The configured environment variables will be configured into the OS environment when the function is executed. The function code can read the system environment variables to obtain the specific values and use them in the code.

## Adding an environment variable

### Adding an environment variable in the console

1.Log in to the [Serverless console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar
2. When creating or editing a function, you can add environment variables in "Environment Variable".
   Environment variables usually appear as `key-value` pairs. Enter the required environment variable key in the first input box and the required value in the second one. Note that the value of `key` or `value` can contain 2–64 bytes of letters, digits, and underscores and must begin with a letter.

## Adding an environment variable locally

For local development, you can configure the `Environment` environment variable directly under the function in `serverless.yml` and run the `scf deploy` command to deploy it to the cloud as shown below:

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

## Viewing an environment variable

After configuring environment variables for the function, you can query the specific configured environment variables by viewing the function configuration, which are displayed in the form of `key=value`.


## Using an environment variable

The configured environment variables will be configured into the runtime environment when the function is executed. The code can read the system environment variables to get the specific values and use them in the code. It should be noted that **environment variables cannot be read locally**.
Assume that the key of the configured environment variable for a function is `key`. The following is the sample codes for reading and printing the value of this environment variable in different runtime environments.

- **In a Python runtime environment**, the way to read the environment variables is as follows:
```python
import os
value = os.environ.get('key')
print(value)
```

- **In a Node.js runtime environment**, the way to read the environment variables is as follows:
```node.js
var value = process.env.key
console.log(value)
```

- **In a Java runtime environment**, the way to read the environment variables varies by temporary authorized fields and other fields:
    - For temporary authorized fields (including `TENCENTCLOUD_SESSIONTOKEN`, `TENCENTCLOUD_SECRETID`, and `TENCENTCLOUD_SECRETKEY`), the way to read the environment variables is as follows:
```
System.out.println("value: "+ System.getProperty("key"));
```
    - For other fields, the way to read the environment variables is as follows:
```
System.out.println("value: "+ System.getenv("key"));
```

- **In a Go runtime environment**, the way to read the environment variables is as follows:
```go
import "os"
var value string
value = os.Getenv("key")
```

- **In a PHP runtime environment**, the way to read the environment variables is as follows:
```php
$value = getenv('key');
```








## Overview

- **Variable value extraction**: Values that may change in the business can be extracted into environment variables, eliminating the need to modify the code according to business changes.
- **External storage of encrypted information**: Keys related to authentication and encryption can be extracted from the code into environment variables, avoiding security risks caused by the presence of relevant keys hard-coded in the code.
- **Environment differentiation**: The configuration and database information for different development stages can be extracted into the environment variables, so that in different stages of development and release, you only need to modify the environment variable values and execute the development environment database and release environment database separately.

## Use Limits

The following Use Limits apply to the environment variables of functions: 

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
<td nowrap="nowrap"> TENCENTCLOUD_SESSIONTOKEN </td>
<td>{Temporary SESSION TOKEN}</td>
</tr>
<tr>
<td> TENCENTCLOUD_SECRETID </td>
<td>{Temporary SECRET ID}</td>
</tr>
<tr>
<td> TENCENTCLOUD_SECRETKEY </td>
<td>{Temporary SECRET KEY}</td>
</tr>
<tr>
<td> _SCF_SERVER_PORT </td>
<td>28902</td>
</tr>
<tr>
<td> TENCENTCLOUD_RUNENV </td>
<td>SCF</td>
</tr>
<tr>
<td> USER_CODE_ROOT </td>
<td>/var/user/</td>
</tr>
<tr>
<td> TRIGGER_SRC </td>
<td>Timer (if a timer trigger is used)</td>
</tr>
<tr>
<td> PYTHONDONTWRITEBYTECODE </td>
<td>x</td>
</tr>
<tr>
<td> PYTHONPATH </td>
<td>/var/user:/opt</td>
</tr>
<tr>
<td> CLASSPATH </td>
<td>/var/runtime/java x:/var/runtime/java x/lib/*:/opt (`x` is 8 or 11)</td>
</tr>
<tr>
<td> NODE_PATH </td>
<td>/var/user:/var/user/node_modules:/var/lang/node x/lib/node_modules:/opt:/opt/node_modules (`x` is 16, 14, 12, 10, 8, or 6)</td>
</tr>
<tr>
<td> PHP_INI_SCAN_DIR </td>
<td>/var/user/php_extension:/opt/php_extension</td>
</tr>  
<tr>
<td> _ </td>
<td>/var/lang/python3/bin/python x (`x` is 37, 3, or 2)</td>
</tr>
<tr>
<td> PWD </td>
<td>/var/user</td>
</tr>
<tr>
<td> LOGNAME </td>
<td>qcloud</td>
</tr>
<tr>
<td> LANG </td>
<td>en_US.UTF8</td>
</tr>
<tr>
<td> LC_ALL </td>
<td>en_US.UTF8</td>
</tr>
<tr>
<td> USER </td>
<td>qcloud</td>
</tr>
<tr>
<td> HOME </td>
<td>/home/qcloud</td>
</tr>
<tr>
<td> PATH </td>
<td>/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin</td>
</tr>
<tr>
<td> SHELL </td>
<td>/bin/bash</td>
</tr>
<tr>
<td> SHLVL </td>
<td>3</td>
</tr>
<tr>
<td> LD_LIBRARY_PATH </td>
<td>/var/runtime/java x:/var/user:/opt (`x` is 8 or 11)</td>
</tr>
<tr>
<td> HOSTNAME </td>
<td>{host id}</td>
</tr>
<tr>
<td> SCF_RUNTIME </td>
<td>Function runtime</td>
</tr>
<tr>
<td> SCF_FUNCTIONNAME </td>
<td>Function name</td>
</tr>
<tr>
<td> SCF_FUNCTIONVERSION </td>
<td>Function version</td>
</tr>
<tr>
<td> TENCENTCLOUD_REGION </td>
<td>Region</td>
</tr>
<tr>
<td> TENCENTCLOUD_APPID </td>
<td>Account APPID</td>
</tr>
<tr>
<td> TENCENTCLOUD_UIN </td>
<td>Account UIN</td>
</tr>
<tr>
<td> TENCENTCLOUD_TZ </td>
<td>Time zone, which is UTC currently</td>
</tr>
</tbody></table>

