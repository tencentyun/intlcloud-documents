When creating or editing a function, you can add, delete, or modify environment variables for the function runtime environment by modifying the environment variables in the configuration.

The configured environment variables will be configured into the OS environment when the function is executed. The function code can read the system environment variables to obtain the specific values and use them in the code.

## Adding an environment variable
### Adding an environment variable in the console
When creating or editing a function, you can add environment variable input boxes by clicking **Environment Variable Configuration** > **Add an Environment Variable**.
Environment variables usually appear as key-value pairs. Enter the required environment variable key in the first input box, and the required value in the second box.

## Adding an environment variable locally
For local development, you can configure the `Environment` environment variable directly under the function in `template.yaml` and run the `scf deploy` command to deploy it to the cloud, as shown below:
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



## Viewing an environment variable

After configuring environment variables for the function, you can query the specific configured environment variables by viewing the function configuration, which are displayed in the form of `key=value`.

## Using an environment variable

The configured environment variables will be configured into the runtime environment when the function is executed. The code can read the system environment variables to obtain the specific values and use them in the code.
Assume that the key of the configured environment variable for a function is `key`. The following is the sample codes for reading and printing the value of this environment variable in different runtime environments.
In a Python runtime environment, the way to read the environment variables is:
```
import os
value = os.environ.get('key')
print(value)
```

In a Node.js runtime environment, the way to read the environment variables is:
```
var value = process.env.key
console.log(value)
```

In a Java runtime environment, the way to read the environment variables is:
```
System.out.println("value: "+ System.getenv("key"));
```

In a Golang runtime environment, the way to read the environment variables is:
```
import "os"
var value string
value = os.Getenv("key")
```

In a PHP runtime environment, the way to read the environment variables is:
```
$value = getenv('key');
```

## Use Cases

- Variable value extraction: Values that may change in the business can be extracted into environment variables, eliminating the need to modify the code when business changes.
- External storage of encrypted information: Keys related to authentication and encryption can be extracted from the code into environment variables, avoiding security risks if relevant keys are hard-coded in the code.
- Environment differentiation: The configuration and database information for different development stages can be extracted into environment variables, so you only need to modify the values of environment variables during different development and release stages, and execute the development environment database and release environment database separately.

## Use Limits

The following use limits apply to the environment variables of functions:
- The maximum number of environment variables for a single function is 128.
- For each entry, the maximum key size is 64 bytes, the maximum value size is 128 bytes, and value cannot be empty. 
- The key must begin with a letter (**[a-zA-Z]**) and can only contain alphanumeric characters and underscores (**[a-zA-Z0-9\_]**).
- The keys of reserved environment variables cannot be modified, including:
 - Keys beginning with SCF\_, such as SCF\_RUNTIME.
 - Keys beginning with QCLOUD\_, such as QCLOUD\_APPID.
 - Keys beginning with TECENTCLOUD\_, such as TENCENTCLOUD\_SECRETID.
