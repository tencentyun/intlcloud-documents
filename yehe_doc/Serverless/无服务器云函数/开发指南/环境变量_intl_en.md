When creating or editing a function, you can add, delete, or modify environment variables for the function runtime environment by modifying the environment variables in the configuration.

The configured environment variables will be configured into the OS environment when the function is executed. The function code can read the system environment variables to obtain the specific values and use them in the code.

## Adding Environment Variable
### Adding environment variable in console
1. Log in to the SCF console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. When creating or editing a function, you can add environment variables in "Environment Variable".
Environment variables usually appear as `key-value` pairs. Enter the required environment variable key in the first input box and the required value in the second one.

### Adding environment variable locally
For local development, you can configure the `Environment` environment variable directly under the function in `template.yaml` and run the `scf deploy` command to deploy it to the cloud as shown below:
```yaml
	test:
      Type: TencentCloud::Serverless::Function
      Properties:
        CodeUri: ./
        Type: Event
        Description: This is a template function
        Environment:
          Variables:
            ENV_FIRST: env1
            ENV_SECOND: env2
        Handler: index.main_handler
        MemorySize: 128
        Runtime: Nodejs6.10
        Timeout: 3
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

| Environment Variable Key | Specific Value or Value Source |
| --------------------------- | ------------------------------------------------------------ |
| `TENCENTCLOUD_SESSIONTOKEN` | {Temporary SESSION TOKEN}                                         |
| `TENCENTCLOUD_SECRETID`     | {Temporary SECRET ID}                                             |
| `TENCENTCLOUD_SECRETKEY`    | {Temporary SECRET KEY}                                            |
| `_SCF_SERVER_PORT`          | 28902                                                        |
| `TENCENTCLOUD_RUNENV`       | SCF                                                          |
| `USER_CODE_ROOT`            | /var/user/                                                   |
| `TRIGGER_SRC`               | timer (to use a timer trigger)                                    |
| `PYTHONDONTWRITEBYTECODE`   | x                                                            |
| `PYTHONPATH`                | /var/user:/opt                                               |
| `CLASSPATH`                 | /var/runtime/java8:/var/runtime/java8/lib/*:/opt             |
| `NODE_PATH`                 | /var/user:/var/user/node_modules:/var/lang/node6/lib/node_modules:/opt:/opt/node_modules |
| `_`                         | /var/lang/python3/bin/python3                                |
| `PWD`                       | /var/user                                                    |
| `LOGNAME`                   | qcloud                                                       |
| `LANG`                      | en_US.UTF8                                                   |
| `LC_ALL`                    | en_US.UTF8                                                   |
| `USER`                      | qcloud                                                       |
| `HOME`                      | /home/qcloud                                                 |
| `PATH`                      | /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin |
| `SHELL`                     | /bin/bash                                                    |
| `SHLVL`                     | 3                                                            |
| `LD_LIBRARY_PATH`           | /var/runtime/java8:/var/user:/opt                            |
| `HOSTNAME`                  | {host id}                                                    |
| `SCF_RUNTIME`               | Function runtime                                                   |
| `SCF_FUNCTIONNAME`          | Function name                                                       |
| `SCF_FUNCTIONVERSION`       | Function version                                                     |
| `TENCENTCLOUD_REGION`       | Region                                                         |
| `TENCENTCLOUD_APPID`        | Account `APPID`                                                    |
| `TENCENTCLOUD_UIN`          | Account `UIN`                                                      |
| `TENCENTCLOUD_TZ`           | Time zone, which is UTC currently                                              |

