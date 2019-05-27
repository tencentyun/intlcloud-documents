When creating or editing a function, you can add, delete, or modify environment variables for the function runtime environment by modifying the environment variables in the configuration.

After that, the environment variables will be configured into the operating system environment when the function is executed. The function code can obtain the specific values configured by reading the system environment variables and use them in the code.

## Adding an Environment Variable

When creating or editing a function, you can bring out the environment variable input boxes by clicking **Environment variable configuration** > **Add an environment variable**.
Environment variables usually appear as key-value pairs. Enter the required environment variable key in the first input box, and the required environment variable value in the second input box.

## Viewing an Environment Variable

After configuring environment variables for the function, you can query the specific configured environment variables by viewing the function configuration, which are displayed in the form of `key=value`.

## Using an Environment Variable

The configured environment variables will be configured into the runtime environment when the function is executed. The code can read the system environment variables to obtain the specific values and use them in the code.
Assume that the key of the configured environment variable for a function is `key`. The following is the sample code for reading and printing the value of this environment variable in each runtime environment.
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

In a Go runtime environment, the way to read the environment variables is:
```
import "os"
var value string
value = os.Getenv("key")
```

In a PHP runtime environment, the way to read the environment variables is:
```
$value = getenv('key');
```

## Usage Scenario

- Variable value extraction: Values that may change in the business can be extracted into environment variables, eliminating the need to modify the code according to business changes.
- External storage of encrypted information: Keys related to authentication and encryption can be extracted from the code into environment variables, avoiding security risks caused by the presence of relevant keys hard-coded in the code.
- Environment differentiation: The configuration and database information for different development stages can be extracted into the environment variables, so that in different stages of development and release, you only need to modify the environment variable values and execute the development environment database and release environment database separately.

## Usage Restrictions

The following usage restrictions apply to the environment variables of functions:
- The maximum number of environment variables for a single function is 128.
- For each entry, the key size is up to 64 bytes, the value size is up to 128 bytes, and the value cannot be empty. 
- The key must begin with a letter (**[a-zA-Z]**) and can only contain alphanumeric characters and underscores (**[a-zA-Z0-9_]**).
- The keys of reserved environment variables cannot be modified, including keys beginning with SCF\_ such as SCF\_RUNTIME, with QCLOUD\_ such as QCLOUD\_APPID, and with TENCENTCLOUD\_ such as TENCENTCLOUD\_SECRETID.
